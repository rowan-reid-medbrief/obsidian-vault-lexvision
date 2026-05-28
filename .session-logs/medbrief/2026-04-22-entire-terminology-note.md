---
date: 2026-04-22
project: /Users/rowanreid/lexvision/claude_code/medbrief
session: Add "entire" → entire.io terminology note to global CLAUDE.md; recover orphaned artefacts from a prior wrap-up.
type: wrap-up
tags: claude-config, claude-md, terminology, entire-io, orphan-cleanup
repos:
  - path: /Users/rowanreid/.claude
    commit: 522c795
domain: medbrief
---

## Session Summary

Rowan asked me to run `entire enable` across the three MedBrief sub-repos. I did not recognise the command and asked for clarification. He explained it meant entire.io and asked me to add that to the global CLAUDE.md so future sessions resolve the bareword without friction. Researched entire.io: it's a git-native CLI (`entire`) that hooks into a repo to capture AI-agent coding sessions as checkpoints indexed alongside commits (supports Claude Code, Gemini CLI preview, and others). Added a new `## Terminology` section to `~/.claude/CLAUDE.md` with the note plus reference links to the site, GitHub repo, and commands docs.

Wrap-up also recovered uncommitted artefacts from a prior trust-pipeline wrap-up in the same working directory: its session log file, the corresponding INDEX.md entry, and the MedBrief-role memory file (which had been written to disk but never registered in the project's MEMORY.md index). Added the missing index line and committed those separately (544756c) before the terminology change (522c795). Did not actually run `entire enable` in the sub-repos yet; that's still pending for a future session once the terminology change is in place.
