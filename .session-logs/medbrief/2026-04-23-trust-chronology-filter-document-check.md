---
date: 2026-04-23
project: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
session: Replace chronologyRequest_id filter with document existence check (MD-304)
type: handoff
tags: [medbrief, data_pipelines, MD-304, trust-records, sql, validator]
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
    commit: c3d9d55
parent: 2026-04-23-trust-validator-session-limit-aware.md
domain: medbrief
---

## Session Summary

Replaced the inaccurate `chronologyRequest_id IS NOT NULL` filter in `trust_filter_cases.sql` with a check against the `document` table — confirming a chronology PDF actually exists (`filename LIKE '%chron%'`, `mime_type = 'application/pdf'`, `deletedAt IS NULL`). The old check only confirmed a chronology was requested, not produced. The commented reference in `trust_prod_cases.sql` and the validation SQL `scripts/validation_sql/chronology_coverage.sql` were updated in lockstep. Pipeline ran successfully with SESSION_LIMIT=1; the validator confirmed PASS on "Chronology available". Identified three remaining pre-existing validator FAILs (`ss.request_type` column reference bugs, `storeData` structure check) and a cosmetic label ("chronology batch" → "chronology document") to fix in the next session.

## Continuation Prompt

## Continuation: Fix pre-existing validator FAILs (MD-304)

**Parent session:** 2026-04-23-trust-chronology-filter-document-check.md

### Context
Working on the Trust-centre ML dataset pipeline (`data_pipelines/`, MD-304). The validator (`scripts/validate_trust_pipeline.py`) runs 30+ checks against the pipeline output. This session fixed the chronology filter in the SQL queries. Running the validator after that fix revealed several pre-existing FAILs unrelated to the chronology change.

### What was done this session
- Replaced `chronologyRequest_id IS NOT NULL` filter in `trust_filter_cases.sql` with a `document` table existence check (`filename LIKE '%chron%'`, `mime_type = 'application/pdf'`, `deletedAt IS NULL`)
- Updated the commented reference in `trust_prod_cases.sql` and the validation SQL `scripts/validation_sql/chronology_coverage.sql` in lockstep
- Pipeline ran successfully; validator confirmed PASS on "5. Chronology available"

### Current state
- Committed: `c3d9d55` on `main` in `data_pipelines/`
- `.env` has `SESSION_LIMIT=1` (set during testing — restore to desired value before a real run)

### Where we left off
Validator was run at SESSION_LIMIT=1 and returned these FAILs that need investigation:

1. `[FAIL] Sorter whitelist coverage: 1054 (42S22): Unknown column 'ss.request_type' in 'where clause'`
2. `[FAIL] Centre regex coverage: 1054 (42S22): Unknown column 'ss.request_type' in 'where clause'`
3. `[FAIL] request_type: 1054 (42S22): Unknown column 'request_type' in 'field list'` (DB cross-check, filter dataset)
4. `[FAIL] storeData structure: 0/1 rows have ['document', 'page', 'section', 'stack'] keys` (quality check on the filter CSV — may be a SESSION_LIMIT=1 data fluke or a genuine key mismatch)
5. (Cosmetic) Validator success message for check 5 still says "chronology **batch**" — should say "chronology **document**" since it now checks the `document` table

`request_type` is a column on `batchrequest`, not `sortingsession`, so FAILs 1-3 are likely `ss.request_type` references that should be `br.request_type`. Confirm by reading the relevant validator SQL files under `scripts/validation_sql/`.

### Next steps
1. Read `scripts/validate_trust_pipeline.py` and the SQL files in `scripts/validation_sql/` to identify all `ss.request_type` / `request_type` references that are causing the column errors
2. Fix the column references (likely `ss.request_type` → `br.request_type` or a subquery join)
3. Investigate the `storeData` structure FAIL — check what keys the actual storeData JSON contains vs what the validator expects; run at a higher SESSION_LIMIT to confirm if it's a data fluke or a real mismatch
4. Update the "chronology batch" label in `validate_trust_pipeline.py` to "chronology document"
5. Re-run the validator and confirm all DB cross-checks PASS

### Key references
- Validator: `scripts/validate_trust_pipeline.py`
- Validation SQL dir: `scripts/validation_sql/` (check files referencing `request_type`)
- Run validator: `.venv/bin/python3 scripts/validate_trust_pipeline.py --dataset filter`
- Run pipeline: `.venv/bin/python3 scripts/run_pipeline.py --no-progress`
- DB tunnel assumed live on `127.0.0.1:3310` (validator connects automatically)
- `request_type` lives on `batchrequest` (not `sortingsession`) — confirmed in `medbrief/src/Entity/BatchRequest.php`
