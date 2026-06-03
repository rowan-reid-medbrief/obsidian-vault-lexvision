---
date: 2026-06-02
project: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
domain: medbrief
session: "Phase 2 duplicate detection — built and validated detect_duplicates.py; full AI adjudication held"
type: wrap-up
tags: [expert-sheet, phase2, duplicate-detection, dedup, rapidfuzz, soundex, gemini, gemini-2.5-flash, engineer-mode, medbrief]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
    commit: ad04b09
parent: 2026-06-01-expert-profile-generation.md
---

## Session Summary

Built Phase 2 of the Expert Sheet project: `detect_duplicates.py`, a duplicate detector over the
17,778-row classified expert list. Pipeline: normalise → block (surname / email-local /
non-free-domain / phonetic Soundex) → score + tier → Gemini medium-tier adjudication → union-find
grouping → write candidate columns V–Z. Output is candidates for human review, never an auto-merge,
and reconciles with (does not contradict) the existing Column O links. Worked in Engineer mode with
a `DECISIONS.md` log (D1–D11).

Most of the session was validation and tuning against the real data, which surfaced three real
issues fixed in-session: (1) a 68k-pair medium tier dominated by generic role mailboxes (`info@`,
`admin@`) — fixed with a stoplist, cutting the medium tier to ~1.9k with zero recall loss; (2) false
auto-merges in the high tier from rapidfuzz `WRatio` rewarding a shared first name (e.g. "Nick
Parkhouse" vs "Nick Todd") — fixed by switching to `token_sort_ratio` plus a surname-compatibility
gate; (3) surname spelling variants (andersen/anderson) split across blocks — fixed with phonetic
Soundex blocking. Final recall ≈98% vs Column O / 100% vs Column N. The deterministic-only path was
run to validate grouping + the writer (cols A–U preserved byte-for-byte; 2,226 groups / 5,480 rows).

A 160-pair stratified sample of the Gemini adjudication validated `gemini-2.5-flash` quality: 7/8 on
known-positive Column O pairs (the one miss a defensible conservative call), well-reasoned yes/no.
Rowan then chose to HOLD the full 1,864-pair adjudication run. Everything was documented in
`PHASE2_STATUS.md` (state + resume guide) and committed (`detect_duplicates.py`, `DECISIONS.md`,
`PHASE2_STATUS.md`) to `main` (`ad04b09`). Outstanding: the full adjudication run, Chantel/Laura
threshold sign-off, an optional surface-rejected-pairs feature, and the parent-session carry-overs
(Chantel update, Laura profile-gen scope question, 348 Phase-1 unknowns).
