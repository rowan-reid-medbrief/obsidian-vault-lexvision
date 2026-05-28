---
date: 2026-05-09
project: /Users/rowanreid/lexvision/claude_code/medbrief
session: MedBrief Q&A — Trust pipeline SQL filters, Page vs Unitised Document, JSONL split analysis
type: wrap-up
tags: medbrief, data-pipelines, trust-pipeline, domain-concepts, data-analysis
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief
    commit: 1c036df
  - path: /Users/rowanreid/.claude
    commit: d720df1
domain: medbrief
---

## Session Summary

Short Q&A session on the MedBrief workspace. Reviewed the SQL filters in trust_filter_cases.sql (strict training cohort: date >= 2023-01-01, 5 named sorters, Trust centre identification via centretype=1 or four name regexes, chronology requirement, project-not-deleted, destroyed-batch exclusion) and trust_prod_cases.sql (relaxed: date + Trust centre only, sorter/chronology/deletion filters commented out). Explained the Page vs ProcessedDocument (Unitised Document) distinction from the medbrief/ entity model: a Page is a single physical scanned sheet, a ProcessedDocument is a semantically coherent clinical record assembled from one or more pages by the preprocessing model. Analysed the April 2026 JSONL export (205 records: 154 train / 40 val / 11 test) to identify 143 projects with split pages and 62 without, and listed the 62 project IDs.
