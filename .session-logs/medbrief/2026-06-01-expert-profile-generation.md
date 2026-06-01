---
date: 2026-06-01
project: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
domain: medbrief
session: Built and test-ran generate_profiles.py (Phase 1.5 expert profile generation); corroborated the Expert Match pipeline; measured cost
type: wrap-up
tags: [expert-sheet, gemini, profile-generation, expert-match, cost-analysis, medbrief]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
    commit: aabe7fe
  - path: /Users/Rowan.Reid/.claude
    commit: 1fafdd2
---

## Session Summary

Built `generate_profiles.py` for Phase 1.5: web-grounded expert profile generation that
reuses Laura's `gemini_file.py` schema and prompt verbatim, running `gemini-3.1-pro-preview`
(Laura's literal `gemini-3-pro-preview` is invalid in our env) with the Key Vault key. The
key design call, made with Rowan over several plan iterations, was the output shape: instead
of separate files, the script appends Laura's exact Title-Case hand-off schema to a copy of
the Phase 1 classified sheet (openpyxl append-and-preserve), so the same columns both feed
Expert Match and serve as the Phase 2 de-dup signal; both `email` columns are kept on purpose.

Ran a 30-row seeded stratified test batch (15/10/5 across confidence): 19/30 scored ≥8, 6
were identity-not-found, and 7 rows had Gemini disagree with our "medical expert" label (a
useful Phase 1 cross-check). Only ~6% of calls actually invoked Search (most answered from
parametric knowledge), a verifiability flag to raise with Laura. Measured cost ≈ $0.026/
profile (thinking tokens are ~98% of spend) → ~$26 for the 1,000 medical-experts-not-in-MM
pool, low hundreds for the full set; pricing is a labelled proxy since the preview model's
list price is unconfirmed.

Separately corroborated the full Expert Match pipeline from the `expert_match` source repo
(generate → filter → clinician QA → transform → storage_init → SQL + vector index → search
service). Handing off to Phase 2: build `detect_duplicates.py`, adapting the interim plan at
`~/.claude/plans/whats-next-for-this-cozy-whistle.md`. Open item: confirm with Laura whether
running profile generation is in Rowan's scope before any full run.
