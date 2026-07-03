---
date: 2026-07-03
type: wrap-up
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
