# Next Up

## Now (Medbrief)

### Expert Sheet — Phase 2 dedup, pending USE_DB run + Chantel delivery
- **Last touched:** 2026-06-04
- **Status:** Phase 2 `detect_duplicates.py` built, validated, committed (`ad04b09`). Deterministic-only output exists (`data/experts_deduped_20260602_084115.xlsx`, 2,226 groups / 5,480 rows, no DB enrichment). `chantel_update_phase2.docx` drafted and committed — explains cols V–Z, match types, score, primary selection logic, and next steps. Full AI adjudication (1,864 medium pairs) **intentionally gated on profile data** — Gemini has no new signal without specialty/location data. Full detail: `PHASE2_STATUS.md` + `DECISIONS.md`.
- **Next action:** (1) Run USE_DB=true deterministic pass — SSH tunnel open, command: `DEDUP_DRY_RUN=false DEDUP_ADJUDICATE=false DEDUP_USE_DB=true venv/bin/python3 detect_duplicates.py`. (2) Send `chantel_update_phase2.docx` + classified xlsx to Chantel once done. (3) Confirm with Laura whether full profile generation is Rowan's scope — this gates the AI adjudication step. Also open: triage the 348 Phase-1 unknowns.

## Parked

## Done
