# Next Up

## Now (Medbrief)

### Expert Sheet — Phase 2 dedup, pending USE_DB run + Chantel delivery
- **Last touched:** 2026-06-04
- **Status:** Phase 2 `scripts/detect_duplicates.py` built, validated, committed. Deterministic-only output exists (`data/outputs/experts_deduped_20260602_084115.xlsx`, 2,226 groups / 5,480 rows, no DB enrichment). `deliverables/chantel_update_phase2.docx` explains cols V–Z, match types, score, primary selection, next steps. Full AI adjudication (1,864 medium pairs) **intentionally gated on profile data** — Gemini has no new signal without specialty/location data. **Since (2026-06-04):** all 3 scripts gained shared `OUTPUT_MODE`/`WORKING_FILE` env flags (newfile default vs overwrite-in-place) + non-overlapping column blocks (P1 P–U, P2 V–Z, P1.5 moved V→AA; commit `06cb9b5`); deleted 4 superseded Phase-1 intermediate workbooks; project restructured flat-root → `scripts/` + `data/{raw,interim,outputs}` + `docs/` + `deliverables/`, with repo-root path anchoring so scripts run from any dir, plus new `README.md` + `requirements.txt` (commits `6a58c07` + `f6d3ddb`). Full detail: `docs/PHASE2_STATUS.md` + `docs/DECISIONS.md` (D1–D16). **Since (2026-06-04, pt 2, commit `effe70a`):** the 3 legacy outputs were consolidated into one canonical `data/outputs/experts_working.xlsx` via new `scripts/combine_outputs.py` (deduped file as base + profile block shifted 22–53 → 27–58 to match the current P–U / V–Z / AA–BF layout; verified row-aligned). All 3 phase scripts now default `WORKING_FILE`/`INPUT_FILE` to `experts_working.xlsx`. Project now works **on `main` only** (no feature branches — Rowan's preference).
- **Next action:** (0) Verify `experts_working.xlsx` looks right, then delete the 3 legacy Output workbooks (classified / with_profiles / deduped). (1) Run USE_DB=true deterministic pass — SSH tunnel open, command: `DEDUP_DRY_RUN=false DEDUP_ADJUDICATE=false DEDUP_USE_DB=true venv/bin/python3 scripts/detect_duplicates.py`. (2) Send `deliverables/chantel_update_phase2.docx` + classified xlsx (`data/outputs/…152155.xlsx`) to Chantel once done. (3) Confirm with Laura whether full profile generation is Rowan's scope — this gates the AI adjudication step. Also open: triage the 348 Phase-1 unknowns.

## Parked

## Done
