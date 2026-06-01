---
date: 2026-06-01
project: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
domain: medbrief
session: Built and test-ran generate_profiles.py (Phase 1.5 expert profile generation); corroborated the Expert Match pipeline; measured cost
type: handoff
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

## Continuation Prompt

## Continuation: Phase 2 — build detect_duplicates.py (dedup)

**Parent session:** 2026-06-01-expert-profile-generation.md

### Context
Project: `/Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing`. We process
Medbrief's 17,778-row expert master list so only genuine medical experts feed Expert Match.
Phase 1 (user-type classification) is done; Phase 1.5 (profile generation) was built and
test-run this session. **Phase 2 — duplicate detection — is the next and larger unbuilt
half.** A detailed interim plan exists at `~/.claude/plans/whats-next-for-this-cozy-whistle.md`;
adapt it with the notes below.

### What was done this session
- Built `generate_profiles.py` (committed, project `aabe7fe`): web-grounded profile
  generation reusing Laura's `gemini_file.py` Expert schema + prompt, `gemini-3.1-pro-preview`,
  Key Vault key. Appends Laura's Title-Case hand-off schema to a copy of the classified sheet
  (doubles as de-dup signal); strict EmailStr; stratified seeded selection; retry/backoff;
  grounding guard; JSONL checkpoint/resume.
- Ran a 30-row stratified test batch -> `data/experts_with_profiles_20260601_161909.xlsx`.
  19/30 scored >=8; 7 Gemini type-disagreements with our label; only ~6% grounded. Cost
  ~ $0.026/profile -> ~$26 for the 1,000-row pool (proxy pricing; thinking ~ 98% of spend).
- Corroborated the Expert Match pipeline end-to-end from the `expert_match` source repo
  (memory `reference-expert-match-pipeline`).

### Current state
- Committed: project `aabe7fe`, `~/.claude` `1fafdd2`, vault `2422ab3` (pushed).
- Phase 1 output (authoritative): `data/experts_classified_20260601_152155.xlsx`
  (cols A-U; P-U are our classification; col L is Chantel's, untouched).
- `data/*.xlsx`, `*.log`, `*.jsonl` are gitignored.

### Where we left off
Phase 1.5 profile-gen test batch complete. Phase 2 dedup not started — this is the next build.

### Next steps
1. Build `detect_duplicates.py` per the interim plan: normalise -> block -> score (rapidfuzz)
   -> group (union-find) -> Gemini adjudication on the medium tier -> write candidate columns
   V+. Output candidates for human review, never auto-merge.
2. Adaptations to the interim plan from this session:
   - **Input** = `data/experts_classified_20260601_152155.xlsx` (has Phase 1 cols), not the raw master.
   - **Profiles as an OPTIONAL corroborating signal**: for rows that have generated profiles
     (30 now; up to 1,000 if a fuller run happens), specialty/location/job-title agreement can
     confirm a pair. Keep name/email PRIMARY (available for all 17,778); never depend on profiles.
   - **Reuse `generate_profiles.py` patterns** too (openpyxl append-and-preserve, stratified/
     checkpoint, retry/backoff, Key Vault, model preflight) alongside `classify_users.py`.
   - **Budget the adjudication tier** with measured cost: a yes/no adjudication is cheaper than
     the ~$0.026 profile call; run a lighter model/prompt on only the medium tier.
   - **Column placement**: dedup writes V+ on the classified file (V+ free there). The profile
     output used V+ on a SEPARATE file — keep the two outputs separate for now.
   - **Validation**: use the 1,893 existing Column O links as a built-in recall test set.
3. In parallel (not blocking): send `chantel_update.docx` + upload classified xlsx to Chantel;
   **confirm with Laura whether running profile generation is in Rowan's scope** before any full
   profile run; triage the 348 unknowns later.

### Key references
- Interim plan: `~/.claude/plans/whats-next-for-this-cozy-whistle.md`
- Reuse-reference: `classify_users.py` (DB, normalise, openpyxl write `:843`/`:866`, Gemini
  batching `:687`, Key Vault `:1028`); `generate_profiles.py`; `reference_scripts/deduplicate_experts.ipynb`
  (LLM-adjudication prompt style only).
- Data: `data/experts_classified_20260601_152155.xlsx` (sheet `MASTER_260512`) -> `data/experts_deduped_{ts}.xlsx`.
- Memories: `project-profile-generation`, `reference-expert-match-pipeline`,
  `project-expert-sheet-data-processing`, `feedback-commenting-style-expert-sheet` (heavy comments required).
- People: Chantel (sheet owner), Laura (Expert Match / enrichment), Deon (DB access).
