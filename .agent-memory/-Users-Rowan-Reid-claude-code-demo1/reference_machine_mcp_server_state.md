---
name: machine-mcp-server-local-state
description: "Local build state of MCP servers under ~/.claude/mcp-servers/ on this machine, as of 2026-07-16"
metadata: 
  node_type: memory
  type: project
  originSessionId: 3e6fd759-280e-4410-acfd-748905cee5a9
---

As of 2026-07-16, this machine (demo1) has `gdrive-semantic` (`.venv` built, `mcp==1.27.2` pinned per requirements) and `gdrive-mcp-server` (`npm install` + `npm run build`, `dist/` rebuilt) set up from scratch, plus `pptxgenjs` vendored for huble-pptx's Method B build scripts and `mmdc` (Mermaid CLI 11.16.0) installed globally for huble-docx diagrams.

**Why:** closing gaps `install.sh`'s new phases (`phase_huble_pptx_deps`, the mmdc/pptxgenjs verify checks) and a large config pull (~130 commits) surfaced. Done even though none of gdrive-semantic/gdrive-mcp-server/google-sheets is actually registered under `claude mcp list` on this account (registrations here are work/MedBrief-side: azure-devops, atlassian, HubSpot, Google Drive/Gmail/Calendar via claude.ai connectors) — Rowan confirmed none of these are in use here yet, but wanted the local build state caught up regardless.

**How to apply:** don't re-diagnose "is X built" for these on this machine; check here first. If gdrive-semantic/gdrive-mcp-server/google-sheets get registered later, the local build/venv side is already done — only registration (`claude mcp add ...` per `mcp-servers/REGISTRATION.md`) and, for google-sheets, a fresh OAuth consent (scope was narrowed upstream, re-auth declined here as unused) remain.

Update 2026-07-18: this machine also has no live `~/.claude/mcp.json`, which fails `tests/wiring/test-mcp-config.sh` on the primary checkout (linked-worktree runs SKIP the check). Recorded as a machine-local expected red in `tests/KNOWN-RED.local.md`; idea #qypmxb (register the servers and create mcp.json, clearing that entry) is on the central backlog.
