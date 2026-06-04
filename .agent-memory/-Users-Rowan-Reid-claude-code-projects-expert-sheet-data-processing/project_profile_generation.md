---
name: project-profile-generation
description: "Phase 1.5 expert profile generation — generate_profiles.py, test-batch results, cost model, and the open Laura scope question"
metadata: 
  node_type: memory
  type: project
  originSessionId: 32ef5056-c8d8-4a67-9052-1763194c8825
---

## Expert profile generation (Phase 1.5)

> **Two later changes supersede details below.** (1) **Column partition** (2026-06-04, commit
> 06cb9b5): Phase 1.5 now appends from **column AA** (27), not V — so the three scripts don't
> overlap (Phase 1 P–U, Phase 2 V–Z, Phase 1.5 AA onward). (2) **Restructure** (2026-06-04, commits
> 6a58c07 + f6d3ddb): script is now `scripts/generate_profiles.py`; input/output xlsx live in
> `data/outputs/`; checkpoint in `data/interim/`. Also added `OUTPUT_MODE`/`WORKING_FILE` env flags
> (newfile default vs overwrite). See [[project-phase2-dedup]] and `docs/DECISIONS.md` D12–D16.

`scripts/generate_profiles.py` runs Laura's web-grounded profile research over the
medical experts our Phase 1 classifier surfaced. Built and test-run 2026-06-01.

### What it does
- Reuses the `Expert` pydantic schema + `base_prompt` verbatim from
  `reference_scripts/gemini_file.py` (Gemini + `google_search` tool, structured against the
  87-item common_utils specialities enum, plus `profile_score` 1-10 + `reason_for_score`).
- Model `gemini-3.1-pro-preview` (Laura's literal `gemini-3-pro-preview` is invalid in our
  env; verified via `models.list()` at startup, no silent swap). Key from Azure Key Vault
  `expertmarketplace-kv` / `GEMINI-API-KEY`, same as classify_users.py.
- Strict `EmailStr` kept (installed `pydantic[email]`); a returned email that fails
  validation → fallback row `profile_score=1`, `Status=not_found`.
- Input: corrected classified file `data/outputs/experts_classified_20260601_152155.xlsx`. Pool =
  `our user type == 'medical expert'` AND not in MM AND email+names = **1,000 rows**
  (High 439 / Med 341 / Low 220). Seeded (SEED=42) stratified test batch of 30 (15/10/5).

### Output design (Rowan's call)
- **Appends** columns to a copy of the Phase 1 sheet (openpyxl append-and-preserve, like
  `classify_users.py:866-911`) → new timestamped `data/experts_with_profiles_{ts}.xlsx`.
  Source never mutated; row colour-coding preserved.
- Appended cols from col AA (was V; see partition note above) = **Laura's exact Title-Case hand-off schema** (`First Name`,
  `Job Title`, `Specialty`, `Speciality1..7`, `Career History`, etc.) + audit cols
  (`profile_score`, `reason_for_score`, `source_pages`, `model_used`, `raw_json`). These
  serve BOTH the Expert Match hand-off AND the de-dup signal (same row as `id` +
  classification, so no separate file/sheet, no join).
- Two `email` columns is intentional (col F = Chantel's fos_user email; appended `email` =
  Laura's). pandas read suffixes the 2nd to `email.1` — harmless.
- `Status` is the clinician-QA gate; we NEVER auto-set `done` (only `not_found` for score-1,
  else blank/pending). Rows are shape-complete but wait at `filter_experts` until a clinician
  marks `done`.

### Test-batch results (30 rows, output `data/outputs/experts_with_profiles_20260601_161909.xlsx`)
- profile_score: 19/30 ≥8, 6/30 =1, 5 mid.
- **7 rows where Gemini's `type` disagreed with our 'medical expert' label** (6 other, 1
  agency) — useful Phase 1 cross-check, mostly org-inbox rows.
- **Grounding: only ~2/30 actually invoked Search** — most profiles answered from the model's
  own knowledge. Cheap, but a verifiability flag for medico-legal use (raise with Laura).

### Cost model (MEASURED tokens; PROXY pricing — gemini-3.1-pro-preview list price unconfirmed)
- Per profile: input ~460 tok, output incl. thinking ~2,500 tok (~70% thinking), total
  ~2,970 tok; ~34s wall-clock.
- Proxy rates (public Gemini 2.5 Pro: $1.25/M in, $10/M out; Search $35/1k): **~$0.026/
  profile**. → 30 ≈ $0.77; **1,000 ≈ $26** (~1-1.5h at 8x parallel); full ~12,385 ≈ ~$320.
  Output (thinking) ≈ 98% of spend — capping the thinking budget is the main cost lever.

### Open question / scope
Laura asked if Rowan has "generated the profiles." Distinction: USING existing profile data
(Rowan's Phase 1/2 scope) vs GENERATING new profiles (the front of Laura's enrichment
pipeline). **Confirm with Laura whether running generation is Rowan's scope before any full
run.** See [[reference-expert-match-pipeline]] and [[project-expert-sheet-data-processing]].
