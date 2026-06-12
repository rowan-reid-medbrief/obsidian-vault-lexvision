---
date: 2026-06-12
project: /Users/Rowan.Reid/claude_code/projects/lexvision-poc
domain: lexvision
session: Installed the HubleDigital hubspot-knowledge plugin and built the primers companion as a docx
type: wrap-up
tags: [kumulus, hubspot-kb, plugin, pandoc, docx, primers]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/lexvision-poc
    commit: primers-and-further-learning.docx
---

## Session Summary

Installed the HubleDigital `hubspot-knowledge` Claude Code plugin: the marketplace add failed over HTTPS (no non-interactive credentials, and the org is HubleDigital not RowanReid), so it switched to the SSH URL after confirming key access, then installed and reloaded. Its `/hskb-update` self-updater errored on a missing `HSKB_DATA_HOME` (the `HSKB_*` env is injected into the plugin's MCP server process, which `/reload-plugins` reported as 0 running, not into the shell), so the data-bundle update is left for a later pickup from inside the plugin's context. Separately, converted `docs/kumulus/deliverables/primers-and-further-learning.md` to a clean docx via pandoc: no table-of-contents field (so no "update fields" popup on open), styled headings, and all 64 links live and clickable.
