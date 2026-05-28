---
date: 2026-04-22
project: /Users/rowanreid/lexvision/claude_code/medbrief
session: Configured Atlassian Remote MCP for MedBrief Confluence (read-only OAuth), scoped to three spaces; exploration deferred to next session.
type: handoff
tags: [mcp, confluence, atlassian, medbrief, setup, read-only-oauth]
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief
    commit: d8a3076
  - path: /Users/rowanreid/.claude
    commit: c4f910d
parent: 2026-04-22-medbrief-workspace-setup.md
domain: medbrief
---

## Session Summary

Rowan offered Confluence access to give `data_pipelines` work more context, and after weighing MCP vs paste-based, chose MCP. Installed the Atlassian Remote MCP (SSE, `https://mcp.atlassian.com/v1/sse`) in the workspace's `.mcp.json` (project-scoped so it doesn't pollute other workspaces) with read-only OAuth scopes to be selected at consent time. Three spaces were agreed as the only in-scope areas: `MEDBRIEF`, `MDC`, `MD`. Updated `reference_medbrief_resources.md` to replace the prior "paste-based (no MCP)" note. Session ended before OAuth completed, so the actual Confluence crawl hasn't started; handed off so the next session can pick up exploration and progressively build a knowledge map.

## Continuation Prompt

## Continuation: MedBrief Confluence exploration + knowledge map

**Parent session:** 2026-04-22-confluence-mcp-setup.md

### Context
MedBrief workspace at `/Users/rowanreid/lexvision/claude_code/medbrief`. Rowan wants me to progressively explore three Confluence spaces and build a structured knowledge map so future sessions know what's where. Confluence access was just set up via the Atlassian Remote MCP (read-only OAuth).

### What was done last session
- Installed Atlassian Remote MCP in this workspace's `.mcp.json` (SSE endpoint `https://mcp.atlassian.com/v1/sse`). Project-scoped, not global.
- Committed: `d8a3076` (`.mcp.json`), `6bd8421` (CLAUDE.md Trust-centre status update), `c4f910d` in `~/.claude` (memory additions).
- Updated reference memory `reference_medbrief_resources.md` to reflect MCP availability (previously said "paste-based (no MCP)").
- Confirmed with Rowan: three in-scope spaces only (`MEDBRIEF`, `MDC`, `MD`). Do not browse other spaces without asking.

### Current state
- `.mcp.json` is committed. Rowan needs to have approved the MCP server and completed the OAuth flow (read-only scopes) before this session can call any Atlassian tools. **Verify Atlassian MCP tools are available before starting any exploration.** If not available, ask Rowan to complete the OAuth flow.
- `data_pipelines/` has uncommitted Trust-centre pipeline files (Rowan's work in progress; don't touch unless asked).

### Where we left off
MCP configured but exploration hasn't started. Waiting for OAuth to complete, then begin the progressive space crawl.

### Next steps
1. Confirm Atlassian MCP tools are loaded and OAuth is complete. If not, ask Rowan.
2. Ask Rowan upfront: any topics to prioritise (e.g. Trust-centre dataset context, clinical schema definitions, v2 dataset plan)? Any pages to avoid (confidential, legal, HR)?
3. For each space (`MEDBRIEF`, `MDC`, `MD`): list top-level pages and any "overview" / "home" / "start here" content. Get the shape before drilling down.
4. Read the highest-signal pages first: landing pages, architecture overviews, data dictionaries, recent updates. Do NOT speculatively crawl.
5. Progressively build a reference map at `~/.claude/projects/-Users-rowanreid-lexvision-claude-code-medbrief/memory/confluence_map.md`. One file, type `reference`. Structure: per-space purpose, load-bearing pages with 1-line summaries, source-of-truth notes, gotchas. Add a pointer to it in `MEMORY.md`.
6. Check in with Rowan periodically rather than reading everything in one go. Ask before pulling more than ~10 pages at a time.

### Key references
- `.mcp.json`: `/Users/rowanreid/lexvision/claude_code/medbrief/.mcp.json`
- Confluence site: `https://medbrief.atlassian.net`
- In-scope spaces: `MEDBRIEF`, `MDC`, `MD` (space keys)
- Memory file with resource pointers: `/Users/rowanreid/.claude/projects/-Users-rowanreid-lexvision-claude-code-medbrief/memory/reference_medbrief_resources.md`
- Project CLAUDE.md (workspace rules, Trust-centre pipeline status): `/Users/rowanreid/lexvision/claude_code/medbrief/CLAUDE.md`
- Data pipelines run on-demand only. See `project_data_pipelines_cadence.md`.
