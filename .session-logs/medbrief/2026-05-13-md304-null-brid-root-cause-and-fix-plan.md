---
date: 2026-05-13
project: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
session: Diagnosed null `batch_request_id` in Trust provenance JSONL, decomposed root causes against prod DB, and produced an implementation plan for a two-part fix.
type: handoff
tags: [MD-304, data-pipelines, jsonl, provenance, split-pages, mysql-connector, claude-opus]
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
    commit: 5bda08b
  - path: /Users/rowanreid/.claude
    commit: 3fcd51e
domain: medbrief
---

## Session Summary

Rowan flagged that the `2026-04-23T1952_limit500` filter JSONL contained sorted pages with `batch_request_id: null`. Built `scripts/diagnose_null_batch_pages.py` + `scripts/validation_sql/diagnose_null_batch_pages.sql` (a LEFT-JOIN classifier through `page → batchdocument → document`), ran it against the prod DB, and decomposed the 9,811 null-brid pages (2.68% of 365,474) into three categories:

- **97.5 %** clinician-produced split pages (`image/jpeg` BDs created by the `SplitPage` service, dropped by the `d.mime_type = 'application/pdf'` filter in `trust_pages_in_batch.sql`).
- **2.5 %** cross-cohort pages — BatchRequests belonging to the session in the DB but excluded from the cohort by `trust_filter_cases.sql` (so they never appear in `batches[]`).
- **<0.01 %** `image/tiff`, same mechanism as JPEG.
- Zero soft-deleted BDs, zero FK orphans, zero missing rows. The filter explains the bucket completely.

DB spot-checks confirmed the classification: page 10177329 (session 343) → BD 499016 → document `640ee65c…jpg` (image/jpeg); BR 77114 is in session 343's batchrequests, so the page was just non-PDF-filtered. Cross-batch case spot-check (session 7321, page 25220036 → BR 139628) confirmed the BR belongs to the session in the DB but isn't in the JSONL's `batches[]`.

Verified via Explore agent against the `medbrief/` sibling repo that the schema tracks **zero provenance link** from a split-image BD back to the source PDF page: `SplitPage::split()` creates a new BD/Document/Page chain with no `sourcePage`, `parentPage`, or equivalent FK. This forced the "treat non-PDFs as standalone atoms" decision and ruled out adding any split-source field.

Agreed a two-part fix with Rowan: (1) enrich non-PDF pages in place with `batch_request_id`, `batch_document_id`, `mime_type`, `document_native_filename`, `document_project_id` (drop the `application/pdf` filter, add columns, partition PDF cumcount in Python so `page_number_in_batch` stays byte-identical for PDFs); (2) union cross-cohort BRs into `batches[]` with `source: "cohort" | "cross_cohort_reference"`, seeded via a small `batchrequest.centrename` pre-query so image-only BRs aren't silently dropped. Validator gets a new "Null batch_request_id rate" check (PASS=0%, WARN>0%, FAIL>1%). README documents the new fields. Applied uniformly to filter and prod JSONLs.

Detailed plan written to `~/.claude/plans/let-s-start-with-approach-precious-firefly.md` covering all 10 edge cases (NULL `batchDocument_id`, soft-deleted BDs, missing page rows, empty cohorts, BRs with only non-PDFs, etc.). Plan not yet executed — handoff prepared so implementation continues in a fresh session.

Side observation captured to memory: `mysql-connector-python 9.6` now negotiates SSL by default and fails against the SSH tunnel with "wrong version number"; `ssl_disabled=True` is the workaround. Existing scripts don't have the flag — may need patching when they're next run.

## Continuation Prompt

## Continuation: MD-304 null `batch_request_id` fix — implement the plan

**Parent session:** 2026-05-13-md304-null-brid-root-cause-and-fix-plan.md

### Context

In the previous session, we diagnosed why 9,811 pages (2.68 %) in the `2026-04-23T1952_limit500` Trust filter JSONL had `batch_request_id: null` and produced a two-part fix plan. Diagnostic + memory work is committed. The implementation has not yet been written.

### What was done previous session

- Built `scripts/diagnose_null_batch_pages.py` + `scripts/validation_sql/diagnose_null_batch_pages.sql` (committed in `fd1dbe2`).
- Ran the diagnostic against prod; decomposed null-brid into: 97.5 % `image/jpeg` split pages, 2.5 % cross-cohort, <0.01 % `image/tiff`, 0 % anything else.
- Verified via the `medbrief/` repo that the DB tracks zero split provenance.
- Rowan landed a parallel commit `5bda08b` adding `has_split_pages` per-batch in `batches[]`.
- Updated `project_split_pages.md` to record the no-provenance constraint and created `project_db_ssl_workaround.md` for the `mysql-connector` SSL flag.
- Wrote the implementation plan to `~/.claude/plans/let-s-start-with-approach-precious-firefly.md`.

### Current state

- `data_pipelines` HEAD: `5bda08b [MD-304] Add has_split_pages to each batch object in JSONL`. Working tree clean.
- `~/.claude` memory commit: `3fcd51e`.
- No implementation work has been written. The plan file is gitignored (lives in `~/.claude/plans/`).

### Where we left off

Plan approved by Rowan after a round of clarifying questions (filename column → `document_native_filename` only; BD id → new `batch_document_id` field, keep `native_document_id` PDF-only; `batches[]` source enum → `"cohort"` / `"cross_cohort_reference"`; validator thresholds → PASS=0% / WARN>0% / FAIL>1%). Next step is to execute the plan.

### Next steps

1. Read `~/.claude/plans/let-s-start-with-approach-precious-firefly.md` end-to-end. The plan is the single source of truth for this work.
2. Edit `data_pipelines/trust_pages_in_batch.sql` — remove the `application/pdf` filter, add `d.mime_type`, `d.nativeFilename AS document_native_filename`, `d.project_id AS document_project_id` columns. Keep `bd.deletedAt IS NULL` and the ORDER BY.
3. Edit `data_pipelines/eda.ipynb` cell 11 (`build_documents_jsonl`):
   - Add the cross-cohort BR discovery pre-query against sorted page_ids (chunk at 50k).
   - Add a `batchrequest.centrename` pre-query that seeds `batch_info[bid]` for every BR in `all_batch_ids`.
   - Partition cumcount to PDF rows (`mime_type == 'application/pdf'`).
   - Enrich `page_info` and the per-page output records with `batch_document_id` / `mime_type` / `document_native_filename` / `document_project_id`.
   - Tag `batches[]` entries with `source: "cohort" | "cross_cohort_reference"` against per-session cohort `batch_ids`.
   - Update the reporting log lines (split into "resolved", "non-PDF (pnib null by design)", "unresolved").
4. Edit `data_pipelines/scripts/validate_trust_pipeline.py` — add the null-brid rate check beside `validate_trust_pipeline.py:789`, and extend the schema-conformance check to know about the new fields.
5. Edit `data_pipelines/README.md` (lines 47–97 + 171) — document the new page fields, the `source` enum, and the new validator check.
6. Use `mysql.connector.connect(..., ssl_disabled=True)` in any **new** Python that opens a DB connection. Existing scripts (`eda.ipynb`, `validate_trust_pipeline.py`, `build_page_verification_manifest.py`) are out of scope for this work — only touch their SSL line if they break.
7. Verify per the plan's "Verification" section: smoke at `SESSION_LIMIT=10`, PDF-cumcount parity diff against `preprocessed_data/2026-04-23T1952_limit500/trust_filter_documents_2026-04-23T1952_limit500.jsonl`, then full `SESSION_LIMIT=500` run.
8. After full-run success: re-run `scripts/diagnose_null_batch_pages.py` against the new JSONL (expect ~0 null-brid), update `project_provenance_invariants.md` to reframe the null-brid decomposition as pre-fix historical behaviour.

### Key references

- Plan: `~/.claude/plans/let-s-start-with-approach-precious-firefly.md`
- Edit target repo: `/Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines`
- Baseline JSONL for cumcount-parity diff: `preprocessed_data/2026-04-23T1952_limit500/trust_filter_documents_2026-04-23T1952_limit500.jsonl`
- Diagnostic for regression check: `scripts/diagnose_null_batch_pages.py`
- Existing builder code: `eda.ipynb` cell 11 (the `build_documents_jsonl` definition)
- Existing validator: `scripts/validate_trust_pipeline.py:789` (null-pnib check, sits next to where the new null-brid check goes)
- DB tunnel: `127.0.0.1:3310`, env vars `PROD_DB_USER` / `PROD_DB_PASSWORD` / `PROD_DB_NAME` in `.env`. Use `ssl_disabled=True`.
- Memory entries to read first: `project_provenance_invariants.md`, `project_split_pages.md`, `project_db_ssl_workaround.md`, `project_db_mysql_version.md`.

### Notes for next session

- No learnings were queued to `~/.claude/learnings.md` this session.
- Auto mode was on for most of the session; Rowan exited auto mode mid-stream and re-entered plan mode for the implementation design. Default to asking a clarifying batch via `AskUserQuestion` if anything in the plan looks ambiguous after a fresh read.
- The plan deliberately preserves the cumulative-sum contract on `batches[].native_documents[]` (PDF-only). Don't be tempted to add image BDs to `native_documents[]` — that breaks the merged-PDF page-number arithmetic.
