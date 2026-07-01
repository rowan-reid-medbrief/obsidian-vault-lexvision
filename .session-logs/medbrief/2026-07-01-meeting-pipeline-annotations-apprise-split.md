---
date: 2026-07-01
project: /Users/Rowan.Reid/claude_code/demo1
domain: medbrief
session: Fetched and fully ingested the 2026-07-01 Deon/Rowan catch-up through the meeting pipeline, split across two project homes
type: wrap-up
tags: [meeting-graph, graph-to-insight, distribute-meeting, transcript-to-insight, promote-graph, scaffold-project, medbrief, annotations, mri133]
repos:
  - path: /Users/Rowan.Reid/.claude
  - path: /Users/Rowan.Reid/ObsidianVault
  - path: /Users/Rowan.Reid/claude_code/projects/annotations
  - path: /Users/Rowan.Reid/claude_code/projects/apprise-viewer-rendering
model_check: fired-upgrade (effort)
---

## Session Summary

Downloaded a gated SharePoint recording of Deon and Rowan's catch-up (cookie retry + DASH-stream fallback), then ran it end to end: meeting-graph (96 nodes/187 edges, 9 chapters) -> promote-graph -> graph-to-insight -> distribute-meeting, splitting the meeting's 80 deltas across the existing `annotations` project (PDF page-matching research: matcher bake-off, stamped-ID conclusion, DocSorter/redaction decision) and a newly-scaffolded `apprise-viewer-rendering` project (Deon's separate date-range PDF rendering ask), plus the shared vault layer. Corrected a Person/Artifact mis-extraction (Sally -> SALLI, MedBrief's sorting system) mid-pipeline and caught + fixed a chapter-9 home-routing oversight before dispatch. Finished with two scoped `/transcript-to-insight` recaps (one per project) since the recap layer has no multi-home distribute equivalent yet. Also fixed a meeting-graph P5 vision-merge path-matching bug and recorded distribute-meeting's first live shakedown.
