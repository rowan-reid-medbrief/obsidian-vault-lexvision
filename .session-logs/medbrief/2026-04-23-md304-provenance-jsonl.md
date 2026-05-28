---
date: 2026-04-23
project: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
session: Added document-level provenance JSONL to the MD-304 Trust pipeline
type: handoff
tags: [MD-304, trust-pipeline, provenance, jsonl, mysql-5.7, validation, data-pipelines]
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
    commit: 694c236
  - path: /Users/rowanreid/.claude
    commits: [4eeb08a, 6fda619]
domain: medbrief
---

## Session Summary

Built a new **document-level provenance JSONL** output for the MedBrief Trust-centre pipeline (`trust_filter_documents.jsonl` + `trust_prod_documents.jsonl`). Each record is one sorting session with nested `batches[]` (ordered PDF `BatchDocument`s with page counts + filenames + centre name) and `sorted_documents[]` whose pages carry `batch_request_id` + `page_number_in_batch`. Consumers derive `(native_document_id, page-within-native)` for any page by cumulative-summing `batches[].native_documents[].page_count`, no pipeline round-trip needed.

Two SQL queries were added at the repo root (`trust_pages_in_batch.sql`, `trust_batch_native_docs.sql`) plus a validation SQL (`scripts/validation_sql/page_in_batch_coverage.sql`). Both files match the app's `Page::getOriginalAbsolutePageNumber()` + `BatchRequest::getBatchDocumentsPdfOnly()` semantics (PDF only, non-soft-deleted, ordered `sortOrder ASC, bd.id ASC, p.id ASC`). All three are MySQL 5.7 compatible: no CTEs, no window functions. Page numbering is done in Python via `groupby('batch_request_id').cumcount() + 1`.

The notebook gained a `build_documents_jsonl` function that walks `storeData`, runs the two bulk queries, assembles session-level records, and writes dual (timestamped + canonical) outputs. The validation harness grew 12 new JSONL checks per cohort — including a live-DB cross-check that re-queries 1 000 sampled pages and compares `page_number_in_batch` — plus README, `.env.example`, and JSONL-shape documentation.

Smoke test with `SESSION_LIMIT=10` produced valid JSONLs for both cohorts; validator reports **55 PASS / 8 WARN / 0 FAIL**. Manual spot-check confirmed the cumulative-sum arithmetic resolves correctly across a sorted doc spanning 9 BatchDocuments.

**Key discoveries:**
1. **Prod DB is MySQL 5.7.44** — forced SQL rewrite away from CTEs/window functions. Saved as project memory.
2. **The "one BatchRequest per sorted doc" invariant is not strict** — 11/10,934 (0.10 %) of sorted docs legitimately span multiple BatchRequests. `batch_request_id` moved from sorted-doc level to per-page level; cross-batch docs surface as a WARN info metric, not FAIL.
3. **~17 % of storeData pages are not in any sorted doc** (sorter leftovers); omitted from JSONL.
4. **`batchdocument.sortOrder` is NULL for 98.6 %** of rows — added `bd.id ASC` as deterministic tiebreaker.

Rowan flagged at wrap-up that he wants next session to focus on comprehensive tests for this new output, possibly including MD5 hashes of individual PDF pages or visual/OCR checks to prove the derived `(native_document, page-within-native)` actually points to the correct source page.

## Continuation Prompt

## Continuation: Build deep correctness tests for the provenance JSONL

**Parent session:** 2026-04-23-md304-provenance-jsonl.md

### Context

Last session I added a document-level provenance JSONL output to the MedBrief Trust pipeline (MD-304). Each sorted-doc page carries `batch_request_id` + `page_number_in_batch`, and consumers derive `(native_document_id, page-within-native)` by cumulative-summing `batches[].native_documents[].page_count`. The new validator section reports 55 PASS / 8 WARN / 0 FAIL on a 10-session smoke test, and a DB cross-check on 1 000 sampled pages returns 1 000/1 000 matches.

BUT Rowan is not yet convinced the page numbering is actually correct. The existing checks only prove internal consistency (pipeline agrees with itself, pipeline agrees with its own re-query of the DB). They do NOT prove the numbering points at the right physical page in the source PDF. This session: design and implement tests that prove end-to-end correctness by reaching into the actual PDF bytes.

### Non-negotiables

- The tests must be able to catch a bug where, for example, our `page_number_in_batch = 17` actually points to page 16 or page 18 of the source PDF (off-by-one or mis-ordered BatchDocuments).
- The tests should work at scale (thousands of pages sampled) but can sub-sample if exhaustive is infeasible.
- The tests must be reproducible and run alongside `scripts/validate_trust_pipeline.py`.

### Strategies to consider (Rowan's suggestions + mine)

1. **MD5 of physical page** — for a sampled page, fetch the source PDF from storage, split it page-by-page (e.g. `pypdf` / `pdftk`), MD5 the Nth page where N = our derived `page_within_native`, and compare to the MD5 of the Page record's `pdfFile` asset (the per-page PDF the app stores). If they match, the numbering is provably correct.
2. **Visual / image hash** — render the Nth page of the source and the corresponding Page.pdfFile, compare via perceptual hash (`imagehash`) or pixel diff. More tolerant than MD5 (handles re-encoding) but needs image tooling.
3. **OCR text match** — extract text from both pages (`pdftotext` / `tesseract`), compare. Robust to re-encoding but expensive and noisy.
4. **App-side API call** — if MedBrief exposes a per-page asset URL indexed by our IDs, compare hashes on the rendered result.
5. **Doctrine-equivalent re-numbering** — re-implement `Page::getOriginalAbsolutePageNumber()` via Doctrine from a small PHP script and compare numbers, as a sanity check that our SQL ordering matches the app's collection order (especially the `sortOrder` NULL-tiebreaker case).

MD5 is cheapest and most definitive if the asset URLs / blob paths are accessible. Start there.

### Investigation to do first

- **How are source PDFs stored?** Likely Azure Blob Storage via Flysystem (mentioned in the workspace CLAUDE.md). Need to find the blob path for a `Document` row (look at `Document` entity + `Upload` entity + Flysystem config in `medbrief/`). Read access only — confirm before any code.
- **What is `Page.pdfFile`?** Per-page PDF asset (column on `page` table — look at `src/Entity/Page.php`). If every Page has its own 1-page PDF blob, MD5-ing it and comparing to the Nth page of the source PDF is the cleanest test.
- **Does `Document` (the `Document` entity, the full uploaded PDF) have its own blob path separate from `Page.pdfFile`?** Likely yes — `Document::nativeFilename` or similar.
- **What's needed to pull blobs locally?** Azure CLI / `azcopy` / the app's storage config. Check `.env` and Flysystem setup in `medbrief/`.

### Proposed test design (draft — refine after investigation)

A new script `scripts/validate_page_provenance_deep.py` that:
1. Takes `--sample-size N` (default 100), `--cohort filter|prod`.
2. Samples N `(session, sorted_document, page)` rows from the JSONL.
3. For each: derives `(native_document_id, page_within_native)` from `page_number_in_batch` + `batches[].native_documents[].page_count`.
4. Fetches the native PDF (blob download, cached locally per native_document_id).
5. Extracts page `page_within_native` from the native PDF (using `pypdf` or similar).
6. Fetches `Page.pdfFile` (the per-page asset for the same Page).
7. Compares: MD5, OR perceptual image hash, OR OCR text.
8. Reports: N passed / failed, example failures with page IDs and both MD5 values.

Wire it into the existing harness (`validate_trust_pipeline.py`) behind a `--deep` flag so it can be opt-in (blob downloads are slow).

### Current state

- Pipeline commit (`694c236` on `data_pipelines/`): everything compiles and passes the existing validator. Two JSONL files live at `preprocessed_data/trust_filter_documents.jsonl` and `preprocessed_data/trust_prod_documents.jsonl` (10 sessions, `SESSION_LIMIT=10` smoke test).
- Existing validator is at `scripts/validate_trust_pipeline.py`; `check_documents_jsonl` and `check_documents_jsonl_db_sample` are the JSONL sections. Deep tests should complement, not replace.
- `.env` has the four new env vars wired up. No blob-storage creds yet — that's part of the investigation.

### Where we left off

Wrap-up committed. No deep-correctness tests exist yet; Rowan flagged this as the main worry before the pipeline can be trusted for production training data. Two new memories capture the domain facts (MySQL 5.7, provenance invariants) to save time in the new session.

### Next steps

1. Investigate blob storage access (start with `medbrief/` repo; look for Flysystem adapter, Azure config, `Upload` entity).
2. Pull one test PDF locally as a spike to confirm access works and pypdf can split it.
3. Pick the cheapest viable comparison (MD5 first; fall back to image hash if the app re-renders).
4. Write the deep-test script, start with 10 pages as proof, scale up.
5. Decide where in the harness it plugs in (`--deep` flag or separate script).
6. Once it's green on a handful of pages, run against 1 000+ samples.

### Key references

- `/Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines/trust_pages_in_batch.sql` — the page-numbering SQL whose correctness we're testing.
- `/Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines/eda.ipynb` cell 11 — `build_documents_jsonl` function.
- `/Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines/scripts/validate_trust_pipeline.py` — `check_documents_jsonl_db_sample` is where the existing shallow check lives.
- `/Users/rowanreid/lexvision/claude_code/medbrief/medbrief/src/Entity/Page.php:849` — `getOriginalAbsolutePageNumber()` (the authoritative algorithm).
- `/Users/rowanreid/lexvision/claude_code/medbrief/medbrief/src/Entity/BatchRequest.php:1941` — `getBatchDocumentsPdfOnly()`.
- `/Users/rowanreid/lexvision/claude_code/medbrief/medbrief/src/Entity/Document.php` — source PDF metadata, `mime_type`, `original_filename`, probably blob path.
- `/Users/rowanreid/.claude/session-logs/2026-04-23-md304-provenance-jsonl.md` — this session's log.
- Project memories: `project_db_mysql_version.md` (MySQL 5.7 gotcha), `project_provenance_invariants.md` (empirical invariants).
- MD-304 Jira: https://medbrief.atlassian.net/browse/MD-304.
