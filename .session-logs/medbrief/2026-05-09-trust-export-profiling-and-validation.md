---
date: 2026-05-09
project: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
session: Trust filter export profiling and self-referencing validation
type: wrap-up
tags: medbrief, data-pipelines, trust-pipeline, data-analysis, data-quality, jsonl, csv
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
    commit: 5bda08b
  - path: /Users/rowanreid/.claude
    commit: d720df1
domain: medbrief
---

## Session Summary

Profiled both outputs from the 2026-04-24T1233_limit500 trust filter run: the CSV (205 sessions, 3,564 columns including 1,774 clinical section pivots) and the JSONL (365,474 pages across 79,071 sorted docs and 2,389 native documents, ~94 MB). Ran 17 self-referencing consistency checks covering ID uniqueness, batch and native-document cross-references, page number sequencing, date ordering, and CSV-JSONL field agreement — all critical references passed. Identified three non-critical findings: `sorted_document_id` is session-local (not globally unique, must use composite key), 9,811 null-provenance pages (pre-existing, expected behaviour from split pages), and 83 start_date > end_date inversions in sorted documents (upstream clinical data quality, not pipeline bugs). Validated page number fields: no duplicates, no out-of-range values; the 57,093 gap pages in `page_number_in_batch` are unsorted pages the clinician deliberately skipped (~13.5% of declared pages, consistent with the provenance invariants memory).
