---
date: 2026-07-04
type: wrap-up
tags: [mri-133, annotations, medbrief, ocr, render-cache, performance, bake-off, confirmation]
repos:
  - annotations: 60540a5
parent: 2026-07-04-mri133-ocr-timeout-and-render-cache.md
model_check: fired-downgrade (model)
---

Disproved the parent session's "sliver -> 120s OCR timeout" diagnosis for the slow full-scale bake-off (real geometric slivers OCR in 0.4s; real scan pages 0.6-1.7s; only 2/8 scenarios split one page each; a 1-in-4 sample of the capped range hit 0 timeouts) and traced the real cost to uncached OCR-arm rendering - `_build_text_layer` re-rendered every text-less page fresh for the original + all 8 scenario variants (~9x redundancy). Fixed it by routing that render through the existing content-addressed render cache (`render_png_cached`, byte-identical by construction: `Pixmap(png).samples == get_pixmap.samples`; 5 new tests, 316 green; `60540a5`), then ran the full-corpus capped clean confirmation the parent aborted (56 min): the content arm is NOT OCR-regressed on SPLIT (4.5% silent vs the render/OCR-independent stamped arm's 36.4%), DoD MARGINAL (P99.9/R69/queue31). Honest caveat: the run's wall-clock is matcher-arm-dominated (~44 min of the 56), so the OCR fix is correct and removes real redundancy but was not the bottleneck; the sequence layer (RESOLVE near-identical/cross-section/exact-dup splits) is the next focused session.