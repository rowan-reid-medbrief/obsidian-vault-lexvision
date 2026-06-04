---
date: 2026-06-04
project: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
domain: medbrief
session: Phase 2 dedup strategy + Chantel email — planned USE_DB=true run, gated AI adjudication on profiles, created chantel_update_phase2.docx
type: wrap-up
tags: phase2, duplicate-detection, expert-sheet, USE_DB, chantel-update, email-draft, score-calculation, primary-selection
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
    commit: af96ed3
---

## Session Summary

Continued Phase 2 duplicate detection work. Discussed the full pipeline mechanics — score calculation (composite of name similarity + email/domain signals; transparency number only, not the tier driver), primary selection logic (Column O primary respected first, then not-deleted, then most recent last_login, then lowest ID), and the key insight that full AI adjudication adds limited value without profile data since Gemini re-examines the same evidence the deterministic stage already used. Decided to run USE_DB=true before delivering to Chantel (SSH tunnel confirmed open) to get soft-delete-aware primary selection and any alt-email links, rather than firing the AI adjudication step now. Drafted and committed `chantel_update_phase2.docx` explaining Phase 2 to Chantel (cols V–Z, match types, score, comparison to Column O, next steps). Full AI adjudication is intentionally gated on profile data being available, which itself is gated on Laura confirming whether profile generation is Rowan's scope.
