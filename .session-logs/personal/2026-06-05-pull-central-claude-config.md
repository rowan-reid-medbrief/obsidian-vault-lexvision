---
date: 2026-06-05
project: /Users/Rowan.Reid/claude_code/demo1
domain: personal
session: Pull latest central ~/.claude config; resolve rebase conflict and push
type: wrap-up
tags: [config-maintenance, git, claude-config]
repos:
  - path: /Users/Rowan.Reid/.claude
    commit: c156ce3
---

## Session Summary

Pulled the latest central `~/.claude` config via `git pull --rebase`. A local unpushed commit (the python-docx "paragraphs exclude tables" profile rule) conflicted with incoming changes in `profile/INDEX.md`; resolved by keeping both index lines, completed the rebase, then pushed the commit to `origin/main`. The working tree's only remaining change is the volatile `settings.json` model line, which is intentionally left uncommitted.
