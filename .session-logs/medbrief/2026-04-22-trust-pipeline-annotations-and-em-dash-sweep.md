---
date: 2026-04-22
project: /Users/rowanreid/lexvision/claude_code/medbrief
session: Trust pipeline [vs GP] annotations, per-repo git identity for medbrief sub-repos, em-dash sweep across session logs.
type: wrap-up
tags: trust-pipeline, vs-gp-annotations, git-identity, em-dashes, entire-io, data-pipelines, medbrief
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
    commit: 005b32e
  - path: /Users/rowanreid/.claude
    commit: 10b3678
domain: medbrief
---

## Session Summary

Clarified that "entire" means entire.io (a terminology note had been added to global CLAUDE.md earlier today). Verified only data_pipelines was enabled; salli and medbrief sub-repos remain context-only. Added a .gitignore entry in data_pipelines mirroring ee_data_migration's pattern: ignore .entire/ entirely, track .claude/ but ignore settings.json, settings.local.json, plans/. Committed together with the agents/entire-search.md that entire.io generated.

Set per-repo git user.name and user.email to rowan.reid@medbrief.co.uk for all three medbrief sub-repos (was unset, defaulting to the hostname identity). Amended the prior commit that had used the hostname.

Annotated the Trust pipeline (trust_filter_cases.sql, trust_prod_cases.sql, eda.ipynb) with [vs GP] markers on each delta from the salli GP template: new request_type=0 filter, 5-sorter subset, Trust centre identification, new isDestroyed exclusion, v1-no-whitelist stance, observed-section logging, and the dropped Computerised GP Records plot. Committed, then caught em-dash violations of the global writing-style rule and amended to restructure without them.

Swept em dashes from all 14 session logs plus INDEX.md (59 em dashes restructured). Started scoping a broader sweep of ~/.claude (memory files, skills, templates) but Rowan asked to stop and move to higher-priority work. That broader sweep remains pending for a future session.
