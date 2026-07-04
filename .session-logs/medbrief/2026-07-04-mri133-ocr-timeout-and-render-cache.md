---
tags: [mri-133, medbrief, ocr, render-cache, performance, bake-off]
repos:
  - annotations: feat/coverage-graph-reframe @ b2621bf
parent: 2026-07-03-mri133-ocr-cache-and-timeout-gap.md
model_check: not-needed
type: wrap-up
---

# MRI-133: OCR per-page timeout + matcher render cache

Shipped two backlog items on `feat/coverage-graph-reframe` (both pushed): the in-matcher OCR per-page wall-clock timeout (`2804882`, retires the pathological-page hang via a killable spawn subprocess that SIGTERMs + skips a page exceeding `ocr_page_timeout_s`, degrading to no-text-layer) and a content-addressed matcher render cache (`0505505`, ~x8 warm and byte-identical, keyed by a cheap pre-render fingerprint of the page's raw streams so identical rasters render once across the 8 resort scenarios). A curated clean bake-off confirmed the OCR timeout works in-situ (hit the pathological page, timed out, skipped, completed) and that neither change regresses split silent-errors - the render/OCR-independent stamped-arm control shows the same 2/10 silent SPLIT. The full-corpus zero-silent-SPLIT reconfirmation is deferred behind a new `[high]` finding: at scale the SPLIT scenarios make many distinct thin-strip sliver pages, each paying a full 120s OCR timeout (`_PAGE_SKIP` dedupes only identical rasters), so the full clean run is impractically slow (>1hr). 311 tests green.
