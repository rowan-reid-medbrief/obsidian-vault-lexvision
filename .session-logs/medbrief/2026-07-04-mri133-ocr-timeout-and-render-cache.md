---
tags: [mri-133, medbrief, ocr, render-cache, performance, bake-off]
repos:
  - annotations: feat/coverage-graph-reframe @ b2621bf
parent: 2026-07-03-mri133-ocr-cache-and-timeout-gap.md
model_check: not-needed
type: handoff
---

# MRI-133: OCR per-page timeout + matcher render cache

Shipped two backlog items on `feat/coverage-graph-reframe` (both pushed): the in-matcher OCR per-page wall-clock timeout (`2804882`, retires the pathological-page hang via a killable spawn subprocess that SIGTERMs + skips a page exceeding `ocr_page_timeout_s`, degrading to no-text-layer) and a content-addressed matcher render cache (`0505505`, ~x8 warm and byte-identical, keyed by a cheap pre-render fingerprint of the page's raw streams so identical rasters render once across the 8 resort scenarios). A curated clean bake-off confirmed the OCR timeout works in-situ (hit the pathological page, timed out, skipped, completed) and that neither change regresses split silent-errors - the render/OCR-independent stamped-arm control shows the same 2/10 silent SPLIT. The full-corpus zero-silent-SPLIT reconfirmation is deferred behind a new `[high]` finding: at scale the SPLIT scenarios make many distinct thin-strip sliver pages, each paying a full 120s OCR timeout (`_PAGE_SKIP` dedupes only identical rasters), so the full clean run is impractically slow (>1hr). 311 tests green.

## Continuation Prompt

## Continuation: MRI-133 - fix the sliver OCR-timeout blowup, then the full-corpus confirmation + sequence layer

**Parent session:** 2026-07-04-mri133-ocr-timeout-and-render-cache.md

### Context
MRI-133 PoC: cardinality-aware page reconciliation so annotations/redactions transfer when a
medical-records bundle is re-sorted. The content-only arm (no durable stamp) is the primary goal.
This session shipped two infrastructure fixes and ran a confirmation that surfaced a new scaling wall.

### What was done this session
- **Shipped the in-matcher OCR per-page timeout** (`2804882`): each text-less page OCRs in a killable
  `spawn` subprocess bounded by `config.ocr_page_timeout_s` (120s); on timeout the child is SIGTERM'd
  (SIGKILL fallback) and the page skipped, routed into the existing `except: continue` fail-safe (degrade
  to no-text-layer, monotone-safe). `_PAGE_SKIP` caps a pathological raster to one timeout per run. 4 new
  tests incl. a deterministic proof `_terminate` reclaims a CPU-pinned worker.
- **Shipped a content-addressed matcher render cache** (`0505505`): `io/render.py::render_image_cached`
  keyed by `_render_fingerprint` (geometry + dpi + raw compressed content/image/xobject streams + font
  metadata, no inflate), stable across the 8 resort scenarios (xref numbers not hashed). `perceptual.
  signature` + `split_visual._gray` use it, gated by `config.render_cache_enable` (default True).
  Byte-identical; ~x8 warm on real bench-100200. 7 new tests. 311 total green.
- **Curated confirmation completed** (exit 0): OCR timeout works in-situ. Split silent-errors (2/10)
  appear in the render/OCR-INDEPENDENT stamped arm too, so it is a subset-composition property, NOT a
  regression from tonight's changes.
- **Full 11-doc confirmation aborted** (~55min): the SPLIT scenarios make many DISTINCT thin-strip
  slivers, each paying a full 120s OCR timeout (`_PAGE_SKIP` dedupes only identical rasters). Logged
  `[high]` (`b2621bf`).

### Current state
All committed + pushed on `feat/coverage-graph-reframe`: `2804882`, `0505505`, `b2621bf`; origin in sync;
`main` untouched; 311 tests green. The full-corpus zero-silent-SPLIT reconfirmation is NOT done (blocked
by the sliver blowup).

### Where we left off
Killed the full 11-doc confirmation run (impractically slow) and wrapped with the two items shipped +
validated (OCR timeout in-situ; no regression via the stamped-arm control). The sliver blowup is the
immediate blocker for any full-scale bake-off run.

### Next steps
1. **[high] Fix the sliver OCR-timeout blowup.** A pre-emptive degenerate-page skip in `io/ocr.py::
   _build_text_layer`: before OCRing a text-less page, skip if the rendered pixmap is below a min-dimension
   threshold (a 1-2px sliver cannot hold OCRable text). First CONFIRM whether the slivers are whole-page
   (geometric crop, thin mediabox, caught by a dimension check) or thin-content-in-a-normal-page (needs an
   ink-bbox check or a shorter timeout) by reading the split MUTATION generator. Monotone-equivalent to
   the timeout-skip (same no-text-layer outcome, no 120s wait). Add a test. Unblocks all full-scale runs.
2. **[high, then unblocked] Full-corpus clean confirmation.** After #1 the full run is fast (render cache
   + no sliver timeouts). Confirm zero silent SPLIT vs the parent's baseline; rules out the one regression
   vector the stamped arm cannot (OCR-skip re-introducing a content split error).
3. **[med] Degraded-population pass** (`--population degraded`), also unblocked by #1. Note: the
   corpus-degrade renders (`scanning.degrade_file`) are NOT yet cached (a logged follow-up).
4. **[high] Sequence/neighbour layer** - the real content-arm progress: RESOLVE (not just safe-queue)
   near-identical / cross-section / exact-duplicate splits. opus/high architecture; model-check and likely
   `/harden-plan` first, ideally its own focused session.
5. Decide: keep or drop the dormant REMOVED rule (config `removed_*`, still off).
6. **[finding]** Recommend OCR-at-ingestion to Deon (3 real docs arrive image-only).

Deferred this session to IDEAS (under ## 2026-07-04 in `docs/IDEAS.md`): sliver OCR-timeout blowup
`[high]`, render-cache tuning (cold-path PNG-encode + unbounded memo) `[low]`, font-program closure
`[low]`, extend the render cache to corpus-degrade `[low]`. Run `/whats-next` to rank.

### Key references
- OCR timeout: `poc/src/mri133/io/ocr.py` (`_ocr_pixmap_subprocess`, `_ocr_worker`, `_terminate`,
  `_PAGE_SKIP`), `config.ocr_page_timeout_s`; tests `poc/tests/test_ocr.py`.
- Render cache: `poc/src/mri133/io/render.py` (`render_image_cached`, `_render_fingerprint`, `_RENDER_MEM`),
  `config.render_cache_enable`; tests `poc/tests/test_render_cache.py`; disk cache `poc/data/_render_cache/`
  (git-ignored).
- Bake-off: `poc/scripts/real_bakeoff.py` - full run `--sample-dir data/real-samples/_stamped --population
  clean --cap-pages 200 --by-case`. `build_real_corpus` globs ALL `*.clean.pdf` (no subset flag; symlink a
  curated dir for a subset). Real corpus is git-ignored PII: never log page content.
- Findings `docs/IDEAS.md` (## 2026-07-04). Memory updated: `mri133-cardinality-channels`. Commits
  `2804882`, `0505505`, `b2621bf`.

### Notes for next session
- venv at `poc/.venv`; Bash cwd resets each call, use absolute paths. tesseract via PyMuPDF `pdfocr`
  (NOT pytesseract). macOS has no `timeout`/`gtimeout`; use a background monitor with an until-loop.
- Scripts that spawn multiprocessing MUST guard `if __name__ == "__main__"` (spawn re-imports `__main__`;
  an unguarded validation script fork-bombed this session). All repo entry scripts are already guarded.
- The full bake-off is render-bound AND now sliver-OCR-bound; #1 unblocks it. The confirmation is
  confirmatory (monotone-safe), not a gate.
- IDEAS.md is at the REPO ROOT (`../docs/` from `poc/`), not `poc/docs/`.
