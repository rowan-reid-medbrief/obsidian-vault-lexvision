---
date: 2026-06-05
project: /Users/Rowan.Reid/claude_code/demo1
domain: medbrief
session: Fetched two MedBrief course videos and built meeting-graph knowledge graphs from both; fixed three meeting-graph skill bugs found along the way
type: wrap-up
tags: [meeting-graph, fetch-video, medbrief, knowledge-graph, skill-fix]
repos:
  - path: /Users/Rowan.Reid/.claude
    commit: d197c6f
---

## Session Summary

Used /fetch-video to pull lessons 1 ("Beyond Vibe Coding") and 9 ("Vibe Coding vs SDD") of the MedBrief intranet course "Vibe Coding to Spec-Driven Development" (both behind Microsoft SSO, retrieved with Chrome session cookies), then ran the full /meeting-graph pipeline on each, producing two typed knowledge graphs with chapters, vision-described slides, summaries and timelines (66 nodes/122 edges and 78 nodes/150 edges; single unidentified narrator each, so person:unknown-speaker). Found and fixed three meeting-graph bugs in the process: the built venv sat at helpers/.venv while common.sh expects scripts/.venv (relocated it), SKILL.md's H variable still pointed at the old helpers/ path, and extract_audio.sh did not create its output parent dir. Graph outputs live under ~/meeting-graph-output/ (outside any repo); no vault notes written yet (next step would be /graph-to-notes or /transcript-to-insight if the content warrants it).
