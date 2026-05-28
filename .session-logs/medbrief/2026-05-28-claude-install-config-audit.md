---
date: 2026-05-28
project: /Users/Rowan.Reid/claude_code/demo1
domain: medbrief
session: Config audit comparing .claude.backup to new install; restored two lost CLAUDE.md sections
type: wrap-up
tags: [config, setup, migration, medbrief, ms365, CLAUDE.md]
repos:
  - path: /Users/Rowan.Reid/.claude
    commit: 8611831
---

## Session Summary

Ran a comparison of the pre-install backup (`.claude.backup.1779952115`) against the new `~/.claude` setup created by the install script. Found that all project memories, MCP server configs, and permissions transferred cleanly. The only meaningful losses were two sections from the old global CLAUDE.md: the MS365/Teams read-only restriction and the Medbrief context pointer to the onboarding project. Both were added back to `~/.claude/CLAUDE.md` and committed to the shared config repo. Voice mode and dark theme settings from the backup were noted but not restored (user opted to skip those).
