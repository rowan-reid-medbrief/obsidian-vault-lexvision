---
date: 2026-04-24
project: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
session: Diagnose null batch_request_id pages and add batch-level has_split_pages to JSONL
type: wrap-up
tags: md-304, split-pages, jsonl, diagnostics, null-brid
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
    commit: 5bda08b
  - path: /Users/rowanreid/.claude
    commit: 745dd74
domain: medbrief
---

## Session Summary

Investigated null batch_request_id pages in the trust_filter_documents JSONL from the 2026-04-23T1952_limit500 run. Found that 97.5% of nulls are JPEG BatchDocuments created by the SplitPage service (expected and benign), 2.5% are cross-batch PDFs, and 0.01% are TIFFs. Discovered that the has_split_pages column in the CSV for that run was all-False because the run used an older notebook that predated the detection feature (commit faef910); the correct figure is ~71% of sessions in that limit500 run (most recent sessions, heavier SplitPage users) vs 33.5% for the full cohort. Added has_split_pages to each batch object in batches[] in the JSONL by calling get_split_batch_ids() inside build_documents_jsonl() alongside the existing session-level detection.
