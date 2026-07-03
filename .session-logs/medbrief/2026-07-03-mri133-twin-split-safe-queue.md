---
date: 2026-07-03
project: /Users/Rowan.Reid/claude_code/projects/annotations
domain: medbrief
session: Safe-queued the exact-duplicate twin split (MRI-133 silent error #3) - the last real silent SPLIT retired
type: handoff
tags: [mri-133, annotations, matchers, split, coverage-graph, content-arm, medbrief]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/annotations
    commit: 95f0e265e37ac73d84c11fbf6d74e6eb8a2b8fa0
parent: 2026-07-03-mri133-in-matcher-ocr-image-only.md
model_check: not-needed
---

## Session Summary

Retired the last real silent SPLIT error (bench-115132's exact-duplicate twin) by proving it information-theoretically unresolvable on page-local content - the split page and its surviving duplicate are byte-identical in text AND geometry - and shipping a monotone-safe safe-queue rule (`twin_split_abstain`, default on) that flags it for review instead of guessing, after measuring that the naive "let the split compete" approach merely relocated the error. 300 tests pass; committed + pushed `95f0e26`. The aggregate bake-off re-read (confirmatory only) kept getting killed on OCR and is carried into the handoff.

## Continuation Prompt

## Continuation: MRI-133 aggregate bake-off + the deferred content-arm backlog

**Parent session:** 2026-07-03-mri133-twin-split-safe-queue.md

### Context
MRI-133 PoC: cardinality-aware page reconciliation so annotations/redactions transfer correctly when a medical-records bundle is re-sorted. The content-only arm (no durable stamp) is a primary goal - make it as strong as possible. The 11-doc real corpus surfaced 3 silent SPLIT errors; this session-arc retired all three (2 via in-matcher OCR, the 3rd via a safe-queue rule).

### What was done this session
- **Diagnosed + fixed the 3rd/last real silent SPLIT** (`bench-115132` under `composed_resort`): a split page whose EXACT duplicate survives whole was silently MATCHED to the duplicate.
- **Proved it irreducible on page-local content**: the split page (171) and its twin (85) are byte-identical in text (`sha 33f29ec9f7f4`) AND geometry (split residual `0.00000`). Measured that the naive "let the split compete" merely RELOCATED the error (scored silent 1->1); rejected it.
- **Shipped `twin_split_abstain`** (default on): a confirmed split reconstruction coinciding with a CONTESTED full holder routes to AMBIGUOUS (review), removing the silent error without relocating it. Gated on a confirmed reconstruction so plain duplicates aren't queued (surgical: real bench silent 1->0, ZERO collateral). Monotone-safe (only ever emits AMBIGUOUS). Pinned off in the neutrality oracle (golden fixture byte-identical), like OCR.
- **300 tests pass**; committed + pushed `95f0e26`. Updated DESIGN-NOTES, IDEAS (twin item done), and the cardinality-channels memory (corrected the false "zero silent both populations" claim).

### Current state
- **Committed + pushed:** annotations `95f0e26` on `feat/coverage-graph-reframe` (origin in sync). Vault session log `429dce06` (pushed).
- The throwaway probe scripts were deleted; the analysis lives in DESIGN-NOTES 2026-07-03.

### Where we left off
The twin fix is done and validated (units, neutrality oracle, scored real-bench probe). The **aggregate bake-off re-read did NOT complete** - it kept getting killed in salli's OCR phase (a 1.5hr no-output run, then a capped re-run killed mid-OCR). It's confirmatory only (the pieces are each validated in isolation), not a correctness gate.

### Next steps
1. **[high] Aggregate bake-off re-read** - confirm zero silent SPLIT on the enlarged corpus (OCR retires 2 + safe-queue the 3rd). It keeps dying on OCR: run with the giants capped small (`--cap-pages 40`), or fix the OCR perf first (#3). Bench (the twin case) runs full regardless of cap.
2. **[med] Degraded-population pass** (`--population degraded`) - now OCR + twin are wired.
3. **[med] OCR confidence-gate + caching/perf** - the root cause the bake-off is un-runnable (per-match OCR on image docs, esp. the 1344pp trust doc). A persistent/ingestion cache is the real fix.
4. **Decide: keep or drop the dormant REMOVED rule** (config `removed_*`, still 0.0/off; fixes 0 of the 3 real silent errors).
5. **[high finding] Recommend OCR-at-ingestion to Deon** - 2 of his real docs arrived image-only, so the platform isn't OCR-ing everything.
6. **[high] Sequence/neighbour layer** - to RESOLVE (not just safe-queue) near-identical / cross-section / exact-duplicate splits. The common lever behind all three open "resolve" gaps.

### Key references
- Fix: `poc/src/mri133/matchers/coverage_graph.py` (`_contested` + the reconstruction-gated abstain in `_classify`); dial `twin_split_abstain` in `config.py`; pinned off in `tests/test_output_neutrality.py`; coverage `tests/test_split_vs_twin.py`.
- Bake-off: `poc/scripts/real_bakeoff.py` (`--cap-pages`, `--population`). Real corpus: `poc/data/real-samples/_stamped/*.clean.pdf` (git-ignored patient data - never log page content).
- Write-ups: `docs/DESIGN-NOTES.md` 2026-07-03 (twin entry); `docs/IDEAS.md` (twin done + the deferred items).
- Commits: annotations `95f0e26` (pushed); vault log `429dce06`. venv: `poc/.venv`. tesseract installed; pytesseract NOT.

### Notes for next session
- Bash cwd resets each call - use absolute paths.
- The real bake-off is OCR-bound and keeps getting killed on the image doc - cap the giants (`--cap-pages 40`) or budget/fix OCR perf before a full run.
- `twin_split_abstain` is monotone-safe: it can only ever send a page to review, never create a silent error - so the aggregate re-read is confirmatory, not a gate.
