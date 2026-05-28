---
date: 2026-04-22
project: /Users/rowanreid/lexvision/claude_code/medbrief
session: Built structured Confluence map of MD/MDC/MEDBRIEF spaces + domain glossary; resolved SALLi vs DocSorter and "what are stacks"
type: wrap-up
tags: [confluence, atlassian-mcp, mapping, memory, medbrief, salli, docsorter, stacks]
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief
    commit: 0477595
  - path: /Users/rowanreid/.claude
    commit: ca2373e
parent: 2026-04-22-atlassian-mcp-transport-migration.md
domain: medbrief
---

## Session Summary

Built a structured Confluence map of the three in-scope MedBrief spaces (MD, MDC, MEDBRIEF) to support future free-form product Q&A. Explored in progressive ~10-call batches with check-ins, flagging ignored areas with reasons. Surfaced the key domain distinction: **SALLi** is the AI Sorting Assistant on Azure Container Apps; **DocSorter** is the human sorting UI inside the MedBrief app. Answered Rowan's motivating example — "what are stacks in DocSorter?" — by grepping the `medbrief/` sub-repo and reading `src/Model/SortingSession/StackModel.php`: a Stack is a grouping of Documents sharing a Clinical Section within a SortingSession (hierarchy `SortingSession → Category → Stack → Documents → Pages`). Captured the map at `confluence_map.md`, refined three memories (updated resources reference for Streamable HTTP transport and write-scope note, added exploration-cadence feedback, added Q&A-intent project memory), and gitignored the workspace's tool-owned `.claude/` and `.entire/` directories. Key learning embedded in the map: domain vocabulary lives in the `medbrief/` codebase, not Confluence.
