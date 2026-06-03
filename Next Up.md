# Next Up

## Now (Medbrief)

### Expert Sheet — Phase 2 dedup built + validated, full AI run held
- **Last touched:** 2026-06-02
- **Status:** Phase 2 `detect_duplicates.py` built and validated end-to-end (Engineer mode), committed to `main` (`ad04b09`). Recall ~98% vs Column O known duplicates / 100% vs Column N; high-tier precision tuned (token_sort_ratio over WRatio, generic role-mailbox stoplist, phonetic Soundex blocking). Deterministic-only output written (`data/experts_deduped_20260602_084115.xlsx`, 2,226 groups / 5,480 rows). A 160-pair adjudication sample confirmed `gemini-2.5-flash` quality (7/8 on known positives). Full medium-tier adjudication (1,864 pairs) **NOT run — held by Rowan**. Phase 1 + 1.5 done earlier (classified file `…152155.xlsx`; `generate_profiles.py` 30-row test batch). Full detail: `PHASE2_STATUS.md` + `DECISIONS.md`.
- **Next action:** Run the full adjudication when ready — `DEDUP_DRY_RUN=false venv/bin/python3 detect_duplicates.py` (~35–50 min background, trivial flash cost), then review cols V–Z in the new output workbook. Optional first: surface flash-rejected borderline pairs ("AI: likely different" flag); get threshold/label sign-off from Chantel (labels) / Laura (model + match quality). Carry-overs still open: send `chantel_update.docx` + upload the classified xlsx to Chantel; confirm with Laura whether profile generation is Rowan's scope; triage the 348 Phase-1 unknowns.

## Parked

## Done
