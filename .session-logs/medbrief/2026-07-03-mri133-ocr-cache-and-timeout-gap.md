---
date: 2026-07-03
project: /Users/Rowan.Reid/claude_code/projects/annotations
domain: medbrief
session: Made in-matcher OCR fast via a page-raster cache; diagnosed the bake-off render wall + an OCR-hang gap; banked the cache + two findings, deferred the broad re-run
type: handoff
tags: [mri-133, annotations, matchers, ocr, performance, content-arm, medbrief]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/annotations
    commit: 415a9ba4bffd6268cf01c7d6ee7d9a6fc68138b8
parent: 2026-07-03-mri133-twin-split-safe-queue.md
model_check: not-needed
---

## Session Summary

Content-address-cached the in-matcher OCR by page raster so each distinct page OCRs once (committed `b4172f9`, 300 tests) - the fix for re-OCR-ing the same rasters ~9x per bake-off run. Then diagnosed why the aggregate bake-off re-run is un-runnable: the real wall is per-page rendering in the matcher (~2 hr, not OCR), and 2 of 3 real image-only docs HANG OCR on a pathological speckled page (no per-page timeout). Banked the cache plus two findings (`[high]` OCR per-page timeout, `[med]` matcher-render caching) and deferred the broad confirmation behind the OCR-timeout fix, since both split retirements are already confirmed individually and are monotone-safe. Detail in the continuation prompt below.

## Continuation Prompt

## Continuation: MRI-133 — fix the OCR per-page-timeout, then the deferred broad confirmation + content-arm backlog

**Parent session:** 2026-07-03-mri133-ocr-cache-and-timeout-gap.md

### Context
MRI-133 PoC: cardinality-aware page reconciliation so annotations/redactions transfer when a medical-records bundle is re-sorted. The content-only arm (no durable stamp) is a primary goal. This session set out to run the parent's [high] "aggregate bake-off re-read" and instead banked an OCR perf cache and surfaced a blocking OCR robustness bug that defers the broad run.

### What was done this session
- Shipped a page-content-addressed OCR cache (`poc/src/mri133/io/ocr.py`, `b4172f9`): each distinct page raster OCRs once (sha1 of pix.samples), so the 8 resort mutations and repeat runs reuse it. 300 tests pass; validated on real salli-142257 (mutations 99-100% cache hits). ocr_dpi held at 200 to protect the split-detection signal.
- Diagnosed the bake-off's true cost: NOT OCR (now cached) but per-page RENDERING in the matcher (mupdf inflate/subsample), across 88 (doc,scenario) combos over 242-1344pp docs, so ~2 hr, render-bound. Logged `[med]` matcher-render caching.
- Found a blocking bug: the in-matcher OCR has NO per-page timeout, so a pathological speckled page pins Tesseract at 100% CPU with zero progress. 2 of 3 real image-only docs hang (bench-100200, salli-142257). Logged `[high]`.
- Corrected memory: pytesseract is a red herring (matcher OCR uses PyMuPDF `pdfocr_tobytes`, not pytesseract); there are 3 image-only docs, not 2 (bench-115132 is also image-only).
- Decision (Rowan): bank tonight, defer the fix - both split retirements are already confirmed individually and are monotone-safe, so the broad run is low marginal value.

### Current state
- Committed + pushed: annotations `b4172f9` (OCR cache) + `415a9ba` (findings) on `feat/coverage-graph-reframe`, origin in sync. Vault log `b8a4ef2` pushed.
- The OCR cache is validated (300 tests + raster probe). The broad bake-off confirmation did NOT complete - blocked by the OCR hang.

### Where we left off
The curated bake-off (salli-142257 + bench-115132 + collateral) stalled OCR-ing salli's pathological page (~page 202), the same symptom as bench-100200. Killed it and banked. Findings logged; fix deferred.

### Next steps
1. **[high] Fix the in-matcher OCR per-page timeout.** Subprocess-isolate `pdfocr_tobytes` (multiprocessing / concurrent.futures), join with a wall-clock timeout; on timeout terminate + skip the page (no text layer, degrade to today's behaviour, same shape as the existing error fail-safe). A `signal.alarm` won't interrupt the in-process C call. Add a test. Unblocks 2-3.
2. **[high, then unblocked] Broad bake-off confirmation** - after #1, run the curated (or full) clean bake-off to confirm zero silent SPLIT. Confirmatory only (monotone-safe), not a gate.
3. **[med] Degraded-population pass** (`--population degraded`) - also depends on #1 (real degraded docs are image-only).
4. **[med] Matcher-render caching** - cache the matcher's per-page render like OCR; full-corpus runs ~2hr to minutes.
5. **[high] Sequence/neighbour layer** - the real progress item: RESOLVE (not just safe-queue) near-identical / cross-section / exact-duplicate splits. opus/high architecture - model-check it.
6. **Decide: keep or drop the dormant REMOVED rule** (config `removed_*`, still off).
7. **[finding] Recommend OCR-at-ingestion to Deon** - 3 of his real docs arrive image-only; the platform isn't OCR-ing everything. (Could route to /check-commitments.)

Deferred this session to IDEAS: OCR per-page timeout [high], matcher-render caching [med] (under ## 2026-07-03 in docs/IDEAS.md); run `/whats-next` to rank.

### Key references
- Cache: `poc/src/mri133/io/ocr.py` (`_ocr_pixmap_cached`, `_PAGE_MEM`); persistent page cache at `poc/data/_ocr_cache/pages/eng-200/`. Bake-off: `poc/scripts/real_bakeoff.py` (`--sample-dir`, `--population`, `--cap-pages`); real corpus `poc/data/real-samples/_stamped/*.clean.pdf` (git-ignored PII, never log page content).
- Findings: `docs/IDEAS.md` (render cache + OCR timeout, under ## 2026-07-03). Memory updated: `mri133-cardinality-channels`, `mri133-real-data-container`.
- Commits: annotations `b4172f9` + `415a9ba` (pushed); vault log `b8a4ef2`. venv `poc/.venv`; tesseract via PyMuPDF `pdfocr` (NOT pytesseract).

### Notes for next session
- The bake-off is un-runnable at full scale until #1 (OCR timeout) or #4 (render cache); the OCR hang blocks even the curated run on salli.
- IDEAS.md is at the REPO ROOT (`../docs/` from `poc/`), not `poc/docs/`. macOS has no `timeout`/`gtimeout`; py-spy needs sudo - use `sample <pid>` for stack profiling.
