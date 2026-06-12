---
date: 2026-06-12
project: /Users/Rowan.Reid/claude_code/demo1
domain: medbrief
session: Meeting-graph re-run staleness review across 7 runs; DE Discussion re-run (byte-equivalent, no net change); Phase B auto-detection assessment
type: wrap-up
tags: [meeting-graph, phase-b, recall-recovery, data-engineering, medbrief, fable-5, model-selection]
repos:
  - path: /Users/Rowan.Reid/.claude
  - path: /Users/Rowan.Reid/ObsidianVault
---

## Session Summary

Reviewed all 7 local meeting-graph runs for re-run-worthiness against skill changes since each ran: only the Data Engineering Discussion clearly qualified, having been processed about 3 hours before the 07-Jun `build_graph.py` fix (edge-weighted relevance gate plus unknown-speaker floor). Re-ran DE with Phase B on, but the rebuild came out byte-equivalent to the original (115 nodes / 205 edges / 51 substantive; the fix's 5 extra edges were stripped by the shared repair stage and `stale_lone_speaker` was already false), confirming the original build was sound and that "7 participants" was a memory error rather than a graph one (the 3 attendees were always correct; the other 4 names are mentioned people). Concluded Phase B auto-detection should be a documented operator heuristic rather than a density-floor gate (the four-run evidence shows substantive density varies about 2x by meeting type, so a floor cannot separate under-extracted from naturally sparse) and logged it centrally; corrected the DE project memory to 3 participants plus a full 7-run inventory; also advised on Fable 5 fit (worth its premium only for overnight agentic runs and deep multi-source synthesis).
