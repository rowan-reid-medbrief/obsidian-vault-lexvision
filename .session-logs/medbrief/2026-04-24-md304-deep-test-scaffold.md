---
date: 2026-04-24
project: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
session: Added JSONL cross-algorithm, uniqueness, and sortOrder-mix validator checks; scaffolded stage 1 of the MD-304 deep page-provenance test
type: wrap-up
tags: [MD-304, trust-pipeline, provenance, validation, deep-test, azure-blob, data-pipelines]
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
    commit: e5b3645
  - path: /Users/rowanreid/.claude
    commit: 41de430
parent: 2026-04-23-md304-provenance-jsonl.md
domain: medbrief
---

## Session Summary

Continued from the provenance-JSONL handoff with the goal of building deep correctness tests that verify each sorted-doc page's derived `(native_document_id, page_within_native)` actually resolves to the correct physical page of the native PDF.

**Key finding that pivoted the plan:** the MedBrief app does not serve document/page PDFs via Azure Blob — those specific Flysystem adapters (`document_native_fs`, `page_pdf_fs`) are LOCAL, reading from `{kernel.project_dir}/data/document/natives/{project_id}/...` and `.../data/page/pdf/{project_id}/...`. Backed by Azure Files in prod but accessible only via some external route we don't have. A mid-session jump-box/SSHFS idea was then ruled out; Rowan later learned the real access path will be an **Azure Blob connection string** (download → process → delete pattern), but the connection string isn't in hand yet. Also discovered that `Page.pdfFile` is re-encoded by PDFTron (`SDFDoc::e_linearized`, optional flatten > 10× avg page size), so byte-level MD5 against a `pypdf` extract will never match — deep comparison has to be image-hash or text-extraction.

Given the access blocker, split the deep test into three stages and landed the non-access-dependent parts:

1. **Three new JSONL validator checks** wired into `scripts/validate_trust_pipeline.py`:
   - `(batch_request_id, page_number_in_batch)` uniqueness within each session (pure-JSONL, catches cumcount duplication / off-by-one).
   - Independent-algorithm DB cross-check (`scripts/validation_sql/page_in_batch_independent.sql`) — correlated `COUNT(*)` subquery recomputes `page_number_in_batch` with the same ordering rules but a different mechanism; catches algorithmic bugs in the pipeline's cumcount path.
   - Per-BatchRequest sortOrder distribution diagnostic (`scripts/validation_sql/sortorder_distribution.sql`) — categorises each referenced BR and WARNs when the `bd.id` tiebreaker matters. Found 22 mixed-sortOrder BRs in the 205-session filter cohort.
   All pass on the current JSONLs (500/500 independent-algo match per cohort; zero duplicate pairs).

2. **Stage 1 manifest builder** (`scripts/build_page_verification_manifest.py`) — DB-only via the existing 127.0.0.1:3310 tunnel. Samples pages from a provenance JSONL, derives `page_within_native` by cumulative-summing `batches[].native_documents[].page_count`, joins `document.nativeFilename` / `document.project_id` / `page.pdfFilename` / `batchrequest.project_id`, and emits a manifest JSONL with pre-computed `native_path_relative` and `page_path_relative`. Supports `--only-mixed-sortorder` to target the ordering edge case. Smoke-tested on the filter cohort (10/10 sampled, 100/100 mixed-sortOrder sampled — all pass bounds).

Stages 2 (image-hash verifier) and 3 (reporter into `--deep` validator flag) are deferred until Rowan has the Azure Blob connection string. The manifest schema is the stable contract between stages, so when the string is available stage 2 plugs straight in without re-touching stage 1.

Also confirmed an earlier SQL ordering concern was a false alarm: `BatchRequest.$batchDocuments` carries `@ORM\OrderBy({"sortOrder"="ASC"})` (missed on first grep; line 491). Our SQL's `sortOrder ASC, bd.id ASC, p.id ASC` correctly matches Doctrine's hydration semantics at all three levels.

**Commits:**
- `cce2058` [MD-304] Add JSONL cross-algorithm, uniqueness, and sortOrder-mix validator checks
- `e5b3645` [MD-304] Scaffold deep page-provenance manifest builder

Four new project memories captured: PDF storage model, PDFTron splitter behaviour, Doctrine @OrderBy semantics, and deep-test stage status. Two updates: SESSION_LIMIT usage pattern (no longer strictly progressive) and provenance invariants (mixed-sortOrder BR count).
