---
name: project-phase2-dedup
description: "Phase 2 duplicate detection — detect_duplicates.py built & validated, full AI adjudication held; status + resume pointers"
metadata: 
  node_type: memory
  type: project
  originSessionId: 6a7dae9f-f7e9-4179-8d53-7a9324b87a99
---

## Phase 2 — duplicate detection (built & validated 2026-06-02)

> **Path note (restructured 2026-06-04, commit 6a58c07):** scripts moved to `scripts/`, data to
> `data/{raw,interim,outputs}`, docs to `docs/`, deliverables to `deliverables/`. So:
> `scripts/detect_duplicates.py`, input `data/outputs/experts_classified_20260601_152155.xlsx`,
> checkpoints/sample in `data/interim/`, `docs/PHASE2_STATUS.md`, `docs/DECISIONS.md`. Scripts
> anchor paths to repo root, so they run from any dir. See [[project-expert-sheet-data-processing]].

`scripts/detect_duplicates.py` is the Phase 2 duplicate detector over the 17,778-row
classified sheet (`data/outputs/experts_classified_20260601_152155.xlsx`). Built and validated
end-to-end (Engineer mode). **Authoritative detail is in the repo: `docs/PHASE2_STATUS.md` (state +
resume guide) and `docs/DECISIONS.md` (D1–D16).** This memory is the load-into-context pointer.

### Pipeline
normalise (`normalise_name`) → block (surname / email-local / non-free-domain / phonetic Soundex)
→ score+tier (high/medium/low; rule-driven, `token_sort_ratio` NOT WRatio) → Gemini medium-tier
adjudication (`gemini-2.5-flash`, yes/no, batched + checkpointed) → union-find grouping → write
cols **V–Z** (group id, match type, score, matched ids, suggested primary/action). Candidates for
human review, never auto-merge; reconciles with (doesn't contradict) existing Column O links.

### Validation
- Recall vs the built-in test set: **Column O ≈98% any-tier, Column N 100%**. Cols O/N are the
  ground truth; Cols C/G COUNTIFs read **empty** (the Phase 1 openpyxl save dropped Excel's cached
  formula values), so we compute our own name/email frequency.
- High-tier precision tuned during validation: fixed WRatio false-merges (use `token_sort_ratio`),
  generic role-mailbox noise (medium tier 68k→1.9k), cross-domain first-name mailboxes; added
  phonetic blocking for surname spelling variants.
- Deterministic-only output written: `data/outputs/experts_deduped_20260602_084115.xlsx` (2,226
  groups / 5,480 rows). **Consolidated into `data/outputs/experts_working.xlsx` (2026-06-04); that
  standalone file plus the other two legacy outputs were deleted 2026-06-05 — `experts_working.xlsx`
  is now the sole canonical workbook (verified: P1 cols Q–U 2,810 rows, P2 cols V–Z 5,480 rows,
  P1.5 cols AA–BF ~30-row test batch only).**
- 160-pair adjudication sample confirmed flash quality: 7/8 on known-positive Column O pairs,
  well-reasoned yes/no.

### Outstanding (as of 2026-06-05)
- **Chantel docx substantially finalised (2026-06-05):** `deliverables/chantel_update_phase2.docx`
  rewritten in Rowan's voice — added a single side-by-side user-type model-comparison table
  (1 June `gemini-2.5-flash` vs 4 June `gemini-3.1-pro-preview`: the newer model is more cautious,
  348 unknowns vs 252, +134 law firm, fewer experts; both runs cover the same 2,810 rows). Replaced
  the "How my results compare to Column O" section with a plain "Summary" (row-numbered real examples,
  e.g. rows 2531/2538 Dr Rufus Cartwright). Replaced "Next steps" with a "Profiles" section (targeted
  test batch, Laura's format, run-a-limited-set proposal). Removed the pasted dup-score/keep scratch
  + CLI artefacts from below the sign-off. **Remaining polish before send (Rowan to decide):** broken
  sentence in the dup-detection intro ("…but since it focusses on… I wrote the script also catch…");
  dangling "more on this below" in the Medium-tier bullet (its target section was removed); pre-existing
  bold inconsistencies; `[SharePoint link]` placeholder. Backup of the pre-rewrite docx at
  `/tmp/chantel_update_phase2_backup_104514.docx`.
- **Immediate next step:** Run USE_DB=true deterministic pass (SSH tunnel confirmed open 2026-06-04):
  `DEDUP_DRY_RUN=false DEDUP_ADJUDICATE=false DEDUP_USE_DB=true venv/bin/python3 scripts/detect_duplicates.py`
  Adds alt-emails from `linkedemailaddress` + soft-delete-aware primary selection (`deleted_at`).
- **Deliverable to Chantel** is now the single `data/outputs/experts_working.xlsx` (no separate
  classified xlsx — it was deleted) plus the finalised docx.
- **Full AI adjudication (1,864 medium pairs) intentionally held** — Gemini re-examines the same
  name/email/domain evidence the deterministic stage already used and adds limited value. Gated on
  profile data being available: once Phase 1.5 runs at scale (specialty + location + employer),
  profile data can pre-filter medium pairs deterministically (same specialty+city → high; conflicting
  → low) before Gemini handles the remainder with genuinely new signal.
- **Laura scope question still open:** confirm whether running full profile generation (~12,385 rows)
  is Rowan's scope or Laura's before proceeding. See [[project-profile-generation]].
- Threshold/label sign-off with Chantel (labels) / Laura (model + match quality) — all `TODO(review)`.
- Optional: surface flash-rejected borderline pairs with an "AI: likely different" flag.
- **Pytest recall gate implemented (2026-06-05, commit `a4d6721`):** `pytest.ini` + `tests/test_recall.py` (Column O + N any-tier recall ≥95% asserted, skips if workbook absent) + `tests/test_scoring.py` (D10/D11 scoring cases). 18/18 passing. D5/D6 lift from L0 to L1. Side-note: `_names_compatible` docstring claims nick/nicholas are compatible but "nicholas".startswith("nick") = False (h≠k at pos 4); docstring is aspirational, pipeline meets targets without it.

See [[project-expert-sheet-data-processing]], [[project-profile-generation]],
[[reference-expert-match-pipeline]], [[feedback-commenting-style-expert-sheet]].
