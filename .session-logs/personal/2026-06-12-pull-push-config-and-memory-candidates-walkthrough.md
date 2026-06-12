---
date: 2026-06-12
project: /Users/Rowan.Reid/claude_code/demo1
domain: personal
session: Pulled + pushed the central ~/.claude config and walked the memory-candidates pipeline
type: wrap-up
tags: [config, git, memory-candidates, wrap-up, meeting-graph]
repos:
  - path: /Users/Rowan.Reid/.claude
    commit: wrap-up 2026-06-12 (config housekeeping commit)
parent:
---

## Session Summary

Pulled the central `~/.claude` config (already current, nothing new came down) and pushed the one unpushed local commit (`351beee`) to origin. Walked the `memory-candidates` pipeline on request: what the file is, how `/wrap-up` consumes it (tool-failure candidates script-consumed inside the lock; meeting-graph blocks reviewed in Step 1), that the surface-memory-candidates + candidates-file + wrap-up-promotion flow is custom-built on top of native memory, and diagnosed why the 17:15 wrap-up didn't surface today's Kumulus meeting-graph block (it was appended afterwards, so no wrap-up had run since). This wrap-up preserves the Kumulus block via the `~/.claude` commit; promoting it properly is deferred to `/graph-to-notes` + `/decision-log` in lexvision-poc, since it is lexvision/medbrief material, not demo1 memory.
