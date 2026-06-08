---
date: 2026-06-08
project: /Users/Rowan.Reid/claude_code/demo1
domain: medbrief
session: meeting-graph runs for Data Engineering Discussion and Kumulus Vendor Proposal meetings with full Phase B recall recovery
type: wrap-up
tags: [meeting-graph, medbrief, kumulus, data-engineering, phase-b, knowledge-graph, vtt-parsing, entity-extraction, pseudonymisation, nice-api]
repos:
  - path: /Users/Rowan.Reid/.claude
    commit: HEAD
---

## Session Summary

Ingested two Medbrief meetings via the meeting-graph skill with full Phase B recall recovery enabled (gapfill, grounded_admit, chunk_budget, anchors, validate_repair, gleaning_passes=2). Fixed a Teams VTT parsing bug (UUID cue identifiers appended as text + missing voice span speaker extraction). DE Discussion (37 min): 115 nodes, 51 substantive, 205 edges, 15 gap-fill nodes across 2 gleaning passes. Kumulus Vendor Proposal (62 min): 152 nodes, 53 substantive, 334 edges, 7 gap-fill nodes with NLI gate active (4 rejected). Both meetings produced meeting.json, summary.md, timeline.md, graph.html, and graph.graphml at ~/meeting-graph-output/. Two skill learnings queued: extraction subagents return lowercase types that build_graph.py rejects (normalizer workaround used), and Phase B multi-pass gleaning has a flat-file mismatch between the spec and dedup_gapfill.py.
