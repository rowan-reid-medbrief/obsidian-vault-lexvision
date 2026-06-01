---
date: 2026-06-01
project: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
domain: medbrief
session: Expert sheet Phase 1 — output format revamped with P–U audit columns
type: wrap-up
tags: expert-sheet, classification, phase1, openpyxl, medbrief, gemini
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
    commit: 3df89ee
parent: 2026-05-29-expert-sheet-run-complete.md
---

## Session Summary

Conversation-heavy session focused on understanding the data and codebase before re-running the script. Identified that Laura's `expert_data_collection_v2_07-25.xlsx` is a separate AI-enriched profile collection file (the raw input to `production_main.py`), distinct from Chantelle's master classification list. Confirmed via DB query that `roleinvitation` roles are per-case (format: `ROLE_PROJECT_<id>_EXPERT`), explaining the high invitation counts. Changed the output format so column L (Chantelle's existing classifications) is never touched — all script output now goes to new columns P–U covering source, our user type, confidence, reasoning, DB roles, and DB user type. Added checkpoint backfill logic so old checkpoint files are enriched with DB fields on load. Re-ran the script cleanly with no Gemini calls (all 2,810 rows loaded from checkpoint); new output at `data/experts_classified_20260601_120322.xlsx`. Next: review 427 unknowns and plan Phase 2 deduplication.
