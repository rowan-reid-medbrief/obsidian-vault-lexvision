---
date: 2026-07-04
type: handoff
tags: [mri-133, annotations, medbrief, ocr, render-cache, performance, bake-off, confirmation]
repos:
  - annotations: 60540a5
parent: 2026-07-04-mri133-ocr-timeout-and-render-cache.md
model_check: fired-downgrade (model)
---

Disproved the parent session's "sliver -> 120s OCR timeout" diagnosis for the slow full-scale bake-off (real geometric slivers OCR in 0.4s; real scan pages 0.6-1.7s; only 2/8 scenarios split one page each; a 1-in-4 sample of the capped range hit 0 timeouts) and traced the real cost to uncached OCR-arm rendering - `_build_text_layer` re-rendered every text-less page fresh for the original + all 8 scenario variants (~9x redundancy). Fixed it by routing that render through the existing content-addressed render cache (`render_png_cached`, byte-identical by construction: `Pixmap(png).samples == get_pixmap.samples`; 5 new tests, 316 green; `60540a5`), then ran the full-corpus capped clean confirmation the parent aborted (56 min): the content arm is NOT OCR-regressed on SPLIT (4.5% silent vs the render/OCR-independent stamped arm's 36.4%), DoD MARGINAL (P99.9/R69/queue31). Honest caveat: the run's wall-clock is matcher-arm-dominated (~44 min of the 56), so the OCR fix is correct and removes real redundancy but was not the bottleneck; the sequence layer (RESOLVE near-identical/cross-section/exact-dup splits) is the next focused session.

## Continuation Prompt

## Continuation: MRI-133 - the sequence/neighbour layer (content-arm DoD-MARGINAL -> PASS)

**Parent session:** 2026-07-04-mri133-render-fix-and-clean-confirmation.md

### Context
MRI-133 PoC: cardinality-aware page reconciliation so annotations/redactions transfer when a
medical-records bundle is re-sorted. The content-only arm (no durable stamp) is the PRIMARY goal.
The prior leg shipped OCR + render-cache infrastructure; this leg corrected a wrong diagnosis,
shipped the real fix, and completed the confirmation. The substantive content-arm work (the
sequence layer) is now the front of the queue and wants its own focused session.

### What was done this session
- DISPROVED the parent's "sliver -> 120s OCR timeout" diagnosis three empirical ways: real
  geometric slivers OCR in 0.4s, real scan pages 0.6-1.7s, only 2/8 scenarios split (one page
  each), and a 1-in-4 sample of the capped range hit 0 timeouts. The proposed min-dimension
  "sliver skip" was a non-fix and was NOT built.
- Found the real bottleneck: `_build_text_layer` (io/ocr.py) re-rendered every text-less page
  fresh (`get_pixmap(dpi=200)`) for the original + all 8 scenario variants (~9x redundancy),
  bypassing the content-addressed render cache.
- Shipped the fix (60540a5): `render.render_png_cached` (a PNG-returning sibling of
  `render_image_cached`, sharing fingerprint + memo + disk store); routed the OCR arm through it,
  gated by `render_cache_enable`. Byte-identical (verified `Pixmap(png).samples ==
  get_pixmap.samples`). Per-scenario OCR-arm cost ~3.8s -> ~1.3s. 5 new tests, 316 green.
- Ran the full-corpus capped clean confirmation the parent aborted (56 min, exit 0): content-arm
  ensemble NOT OCR-regressed on SPLIT (4.5% silent / 45.5% queue vs the render/OCR-independent
  stamped arm's 36.4% silent), so no OCR-induced content-split regression. Ensemble DoD MARGINAL:
  P99.9 / R69.0 / queue31.0.
- Corrected the [high] sliver entry in docs/IDEAS.md; logged two [med] follow-ups.

### Current state
- Committed 60540a5 on `feat/coverage-graph-reframe` (NOT on `main`). 316 tests green. Vault pushed.
- The full capped clean confirmation numbers are in `data/real-bakeoff.json` / `.html`.
- Wall-clock finding: the 56-min run is matcher-arm-dominated (~44 min matching + ~12 min degrade
  build); the OCR fix helped its slice but was NOT the dominant cost.

### Where we left off
Confirmation done and the diagnosis corrected. Stopped before the sequence layer, which is the real
content-arm progress and was deliberately deferred to a fresh, focused opus/high session.

### Next steps
1. [high] SEQUENCE / NEIGHBOUR LAYER - the real content-arm progress. RESOLVE (not just safe-queue)
   near-identical / cross-section / exact-duplicate splits that today route to review (the 45.5%
   SPLIT queue). This is the lever that moves the content arm from DoD-MARGINAL to PASS (recall
   69->70+, queue 31->sub-30). opus/high architecture; run the model-check and likely /harden-plan
   first; ideally its own session. See mri133-cardinality-channels memory for the three open gaps
   this unifies (cross-section, exact-dup twin, gp's blank child).
2. [med] Degraded-population pass (`--population degraded`), now unblocked by the render fix.
3. [med] `--skip-degrade` flag for clean-only runs (~12 min/run) + [med] profile the matcher arm
   (the real 44-min wall-clock) before further OCR-arm perf. Both logged under ## 2026-07-04 in
   docs/IDEAS.md (the PROJECT backlog); run /whats-next to rank.
4. Decide: keep or drop the dormant REMOVED rule (config `removed_*`, still OFF).
5. [finding] Recommend OCR-at-ingestion to Deon (3 real docs arrive image-only).

### Key references
- The fix: poc/src/mri133/io/render.py (`render_png_cached`, `_cached_png_lookup`, `_publish_png`),
  poc/src/mri133/io/ocr.py (`_build_text_layer` render routing); tests poc/tests/test_render_cache.py
  (+4), poc/tests/test_ocr.py (+1, `test_render_cache_routing_is_ocr_neutral`).
- Confirmation: `.venv/bin/python scripts/real_bakeoff.py --population clean --cap-pages 200 --by-case`
  (56 min; use PYTHONUNBUFFERED=1 for live progress). Output data/real-bakeoff.json/.html.
- Backlog docs/IDEAS.md (## 2026-07-04); memory mri133-cardinality-channels (updated with the
  confirmation numbers + the sliver correction). Commit 60540a5.

### Notes for next session
- venv at poc/.venv; Bash cwd resets each call (it persists at .../annotations/poc), use absolute
  paths. tesseract via PyMuPDF pdfocr. macOS has no timeout/gtimeout; use a background monitor.
- Scripts that spawn multiprocessing MUST guard `if __name__ == "__main__"` (spawn re-imports).
- The full bake-off is matcher-arm-bound (~44 min), NOT OCR-bound - profile the matcher arm before
  any further OCR-arm optimisation. The confirmation is confirmatory (monotone-safe), not a gate.
- IDEAS.md is at the REPO ROOT (../docs/ from poc/), not poc/docs/.