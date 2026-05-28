---
date: 2026-04-24
project: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
session: Investigate split pages in MedBrief DB and add has_split_pages column to Trust pipeline
type: wrap-up
tags: MD-304, data-pipelines, split-pages, db-investigation, csv-output, jsonl, validator
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
    commit: faef910
  - path: /Users/rowanreid/.claude
    commit: 188a74d
domain: medbrief
---

## Session Summary

Investigated what "split pages" means in the MedBrief Trust pipeline: a clinician splits a source page during unitisation, producing JPEG BatchDocuments (mime_type='image/jpeg', uniqid hex filenames, always 1 page per BD, created in consecutive pairs at the same timestamp). DB queries against the production database confirmed 33.5% of Trust filter sessions contain split pages (2,521/7,534), with 2.35% of total pages being split pages. Added a boolean `has_split_pages` column to both the filter/prod CSVs and the JSONL session records, detected via a single supplementary query per cohort in `preprocessing()`. Also fixed `_observed_sections()` to require a matching `_docs` column so the new column name (ending in `_pages`) isn't misidentified as a clinical section — a defensive fix that benefits the pipeline generally.
