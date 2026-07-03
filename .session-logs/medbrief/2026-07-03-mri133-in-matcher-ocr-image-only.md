---
date: 2026-07-03
type: handoff
tags: [mri-133, medbrief, matchers, ocr, image-only, split, corpus-expansion, silent-error]
repos:
  - annotations (feat/coverage-graph-reframe)
parent: 2026-07-03-mri133-coverage-graph-reframe-and-corpus-expansion.md
model_check: fired-downgrade (model)
---

# MRI-133: corpus expansion surfaces 3 silent SPLIT errors; in-matcher OCR retires 2

Expanded the real corpus 3->11 docs and ran the enlarged clean bake-off (the two giants capped to
200pp), which surfaced 3 silent SPLIT errors the 3-doc corpus had hidden, correcting the earlier
"zero silent SPLIT" claim. Diagnosed them as 2 image-only (one pure-scan doc, salli-142257, read as
a confident REMOVED on a split) plus 1 text-twin (bench-115132); on Rowan's reframe, built and
verified in-matcher OCR (io/ocr.py: detect text-less pages, OCR just those, no-op otherwise, stamps
preserved, cached, fail-safe) that retires the 2 image-only errors (296 tests green, salli-142257
split silent -> CONFIDENT_CORRECT end-to-end through the wired path). The twin case, a degraded
re-read now that OCR is wired, and the deprioritised dormant-REMOVED rule remain open; full detail in
the continuation prompt below.

## Continuation Prompt

## Continuation: MRI-133 in-matcher OCR done; re-read bake-off, twin case, push still open

**Parent session:** `2026-07-03-mri133-in-matcher-ocr-image-only.md`

### Context
MRI-133 PoC: cardinality-aware page reconciliation so annotations/redactions transfer correctly when a medical-records bundle is re-sorted. This session expanded the real corpus 3->11 docs, which surfaced 3 silent SPLIT errors the small corpus had hidden, and built in-matcher OCR to retire the 2 caused by image-only pages.

### What was done this session
- **Stamped all 11 real docs** (`poc/scripts/stamp_real_samples.py`, reproducible/idempotent) and **wired `real_bakeoff.py`** to source all 11, with a `--cap-pages` flag capping the 2 giants (trust 1344pp, salli-142257 342pp) to 200pp for tractable runs.
- **Ran the enlarged clean bake-off** (giants capped): it surfaced **3 silent SPLIT errors** (a regression vs the 3-doc "zero silent" claim). Decomposed: **2** = one pure-scan image-only doc (`salli-142257`, 342/342 text-less) read as a confident REMOVED on a split; **1** = a text doc (`bench-115132`) confidently matched to a near-identical surviving **twin** under composed re-sort.
- **Proved no cheap matcher fix works** (best-floor no separation, visual guard useless, blunt "never REMOVE text-less" costs 4/10 real REMOVEDs, dormant rule catches none).
- **Built + verified in-matcher OCR** (`poc/src/mri133/io/ocr.py`, `ensure_text_layer`): detect text-less pages, OCR just those (pymupdf+tesseract), true no-op when nothing gains text (blank pages untouched -> synthetic golden fixture stays neutral), stamps preserved per-page, cached, fail-safe. Wired via `base`/`ensemble` `_prep_paths`; dials `ocr_image_only_enable`/`ocr_dpi`. **296 tests green**; neutrality oracle pinned OCR-off (byte-identical); `salli-142257` split silent -> **CONFIDENT_CORRECT** end-to-end through the wired path. New tests: `test_ocr.py`, `test_ocr_fixes_image_only.py`.
- **Killed the degraded pass** (deferred; variants built, resumable via `--population degraded`).
- **Logged ideas** to `docs/IDEAS.md` under `## 2026-07-03`.

### Current state
- **Committed:** annotations `ad0f125` (the OCR feature + IDEAS append) - **LOCAL only, on `feat/coverage-graph-reframe`, NOT pushed** (wrap-up doesn't push project repos). Vault session log `3b988d4` (pushed).
- A **parallel session** is live on the same branch (the "content-arm-viability-and-split-gap" session): it committed `f5cbfaa` (cross-section split IDEAS) and is editing the `mri133-cardinality-channels` memory. My OCR commit is disjoint (`poc/` files) and stacks on `f5cbfaa`.
- Degraded variants built, resumable.

### Where we left off
OCR feature done, verified, committed locally. The isolated end-to-end verify passes, but the **full clean bake-off has not been re-read with OCR wired** - the silent-error numbers above are pre-OCR.

### Next steps
1. **[high] Push the annotations OCR commit** (`ad0f125`) to the GitHub remote - pull-rebase first (parallel session on the branch); the commit is disjoint so it stacks cleanly.
2. **[high] Re-read the clean bake-off with OCR wired** - confirm the enlarged clean corpus now shows 2 fewer silent SPLITs at bake-off level, not just in the isolated verify.
3. **[high] Error #3: `bench-115132` split-vs-twin disambiguation** - the remaining silent error (not OCR, not the dormant rule; the twin's margin is thick so the margin rule can't catch it).
4. **[med] Run the degraded pass** (`--population degraded`) now the OCR-collapse fixture bug is fixed and OCR is wired.
5. **[med] OCR confidence-gate + caching/perf** - esp. the 1344pp trust doc (a per-match OCR pass is tens of minutes).
6. **Decide: keep the dormant REMOVED rule or drop it** (fixes 0 of the 3 real silent errors).
7. **DESIGN-NOTES.md writeup** of the OCR feature + corpus-expansion findings.
8. **[finding] Recommend OCR-at-ingestion to Deon** - 2 of his real docs arrived image-only, so the platform isn't OCR-ing everything.
9. **Memory:** fold the OCR finding + correct the now-false "zero silent SPLIT" claim into `mri133-cardinality-channels` (skipped this session due to the parallel-session live-edit).
- Logged this session to IDEAS (under `## 2026-07-03` in `docs/IDEAS.md`): in-matcher OCR (DONE), split-vs-twin `[high]`, Deon upstream-OCR `[high]`, OCR confidence-gate `[med]`; run `/whats-next` to rank.

### Key references
- Feature: `poc/src/mri133/io/ocr.py`; wiring `matchers/base.py` + `matchers/ensemble.py` (`_prep_paths`); dials `config.py`.
- Prep: `poc/scripts/stamp_real_samples.py`, `real_bakeoff.py` (`--cap-pages`, `LARGE_DOCS`).
- Tests: `test_ocr.py`, `test_ocr_fixes_image_only.py`, `test_output_neutrality.py` (OCR-off pin).
- Real corpus: `poc/data/real-samples/_stamped/*.clean.pdf` (git-ignored patient data - never log page content).
- Commits: annotations `ad0f125` (local), vault `3b988d4` (pushed); parallel `f5cbfaa`.
- `venv`: `poc/.venv`. tesseract 5.5.2 installed; pytesseract NOT installed.

### Notes for next session
- Bash cwd resets each call - use absolute paths.
- The full real bake-off is slow (~2.5-3hrs uncapped); OCR adds time on image-only docs. Cap the giants or budget for it.
- The parallel session may have folded its own corrections into `mri133-cardinality-channels`; check its state before editing (step 9).
