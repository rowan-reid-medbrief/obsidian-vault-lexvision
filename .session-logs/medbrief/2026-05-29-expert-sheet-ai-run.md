---
date: 2026-05-29
project: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
domain: medbrief
session: Expert sheet Phase 1 — Gemini batching, key verified, full AI run (partial)
type: wrap-up
tags: expert-sheet, gemini, classification, phase1, batching, medbrief
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
    commit: 13dff9b
parent: 2026-05-28-expert-sheet-classification-script.md
---

## Session Summary

Verified the new Gemini API key in Key Vault and discovered `gemini-2.0-flash` is no longer available to new users — updated the script to `gemini-2.5-flash`. Identified that the single-row Gemini call approach would take ~4 hours for 2,728 rows; implemented batching (20 rows per call) for a ~20x speedup. Ran the full classification — got to 2,300/2,728 rows before the run stalled overnight due to Gemini connection resets and the DB tunnel dropping. Checkpoint is intact at `data/classification_checkpoint.xlsx`. Paused before resuming to review output quality and consider prompt improvements (e.g. 325 unknowns, inconsistencies between law firm vs non-medical expert for legal professionals).
