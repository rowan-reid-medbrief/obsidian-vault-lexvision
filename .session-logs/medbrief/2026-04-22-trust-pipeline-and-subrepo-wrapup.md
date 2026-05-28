---
date: 2026-04-22
project: /Users/rowanreid/lexvision/claude_code/medbrief
session: Build initial Trust-centre dataset pipeline (MD-304) in data_pipelines, and extend the wrap-up skill to detect and commit sub-repos.
type: wrap-up
tags: medbrief, data-pipelines, trust-pipeline, md-304, salli, wrap-up-skill, sub-repo-detection, confluence-brief, notebook
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief
    commit: d8a3076
  - path: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
    commit: 88b3deb
  - path: /Users/rowanreid/.claude
    commit: b0f430f
domain: medbrief
---

## Session Summary

Built the Trust-centre dataset pipeline from scratch in `data_pipelines/` (MD-304, per Deon Kuhn's *Sorting Data - Trust Records* Confluence brief), mirroring `salli-dataset-creation/` structurally: two SQL queries (`trust_filter_cases.sql`, `trust_prod_cases.sql`), a Jupyter notebook (`eda.ipynb`) for unitisation + EDA + 70/20/10 stratified split, and the standard supporting files. Trust-specific differences from the GP variant: `centreType = 1` plus four known Trust name wildcards for centre identification, `request_type = 0` as a new filter (Initial request type only, required by the brief and not present in GP), batch-level `isDestroyed()` exclusion in the aggregate, and a 5-sorter whitelist (Shard, Wilderspin, Wysocka, Dermott, Gutteridge, a subset of the GP list). Shipped v1 without a clinical-section whitelist so EDA can reveal what Trust data actually contains; a v2 whitelist will be codified from observed section labels. Confirmed with Rowan's AI team that salli and data_pipelines are run on-demand when training data is needed, not scheduled. This shaped the decision to match salli's notebook pattern rather than productionise.

Also extended `/wrap-up` Step 3 to scan one level below the working directory for sub-repo `.git` directories, treating each with uncommitted changes as its own commit target (separate message + Co-Authored-By). Step 4 now records sub-repos in the session log's `repos` field. Tested live in this wrap-up across four repos (workspace root, `data_pipelines/`, `medbrief/`, `salli-dataset-creation/`) plus `~/.claude/`.
