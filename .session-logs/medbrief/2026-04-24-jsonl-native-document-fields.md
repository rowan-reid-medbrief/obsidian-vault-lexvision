---
date: 2026-04-24
project: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
session: Add native_document_id, native_document_filename, page_number_in_native_document to JSONL page objects
type: wrap-up
tags: [MD-304, jsonl, data-pipeline, trust-centre, provenance]
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
    commit: 283e1ce
domain: medbrief
---

## Session Summary

The AI team consuming the Trust-centre JSONL outputs requested three new fields on every page object within sorted_documents: native_document_id (the BatchDocument primary key), native_document_filename (document.original_filename), and page_number_in_native_document (1-indexed position within the source PDF). All three were derivable from data already fetched by the two existing SQL queries, requiring only a second groupby-cumcount in Python and a filename lookup dict — no SQL changes. Four targeted edits were made to the build_documents_jsonl() function in eda.ipynb (cell 11). A SESSION_LIMIT=5 run confirmed the new fields are correctly populated and that page_number_in_native_document resets to 1 at each native document boundary. Full validation passed 59 checks; the single FAIL (fewer than 100 sessions) is an expected artefact of the small test run.
