---
name: project-phase2-dedup
description: "Phase 2 duplicate detection — detect_duplicates.py built & validated, full AI adjudication held; status + resume pointers"
metadata: 
  node_type: memory
  type: project
  originSessionId: 6a7dae9f-f7e9-4179-8d53-7a9324b87a99
---

## Phase 2 — duplicate detection (built & validated 2026-06-02)

`detect_duplicates.py` (project root) is the Phase 2 duplicate detector over the 17,778-row
classified sheet (`data/experts_classified_20260601_152155.xlsx`). Built and validated end-to-end
this session (Engineer mode). **Authoritative detail is in the repo: `PHASE2_STATUS.md` (state +
resume guide) and `DECISIONS.md` (D1–D11).** This memory is the load-into-context pointer.

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
- Deterministic-only output written: `data/experts_deduped_20260602_084115.xlsx` (2,226 groups /
  5,480 rows).
- 160-pair adjudication sample confirmed flash quality: 7/8 on known-positive Column O pairs,
  well-reasoned yes/no.

### Outstanding (as of 2026-06-02)
- **Full medium-tier adjudication (1,864 pairs) NOT run — held by Rowan.** Ready to fire:
  `DEDUP_DRY_RUN=false venv/bin/python3 detect_duplicates.py` (~35–50 min background, trivial cost;
  resumable via `data/dedup_adjudication_checkpoint.jsonl`).
- Threshold/label sign-off with Chantel (labels) / Laura (model + match quality) — all `TODO(review)`.
- Optional: surface flash-rejected borderline pairs with an "AI: likely different" flag.
- Optional `USE_DB` path (alt-emails + `deleted_at`; needs SSH tunnel port 3310) untested live.

See [[project-expert-sheet-data-processing]], [[project-profile-generation]],
[[reference-expert-match-pipeline]], [[feedback-commenting-style-expert-sheet]].
