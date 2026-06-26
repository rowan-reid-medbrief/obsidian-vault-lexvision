---
title: "MedBrief Q1 + Q2 2026 company updates ingested to vault"
type: session-log
domain: medbrief
created: "2026-06-26"
tags: [meeting-graph, process-meeting, transcript-to-insight, decision-log, medbrief, company-update]
repos: [ObsidianVault, ~/.claude]
model_check: fired-upgrade (model)
parent: null
---

# MedBrief Q1 + Q2 2026 company updates ingested to vault

Ingested both MedBrief quarterly company updates (Q1 March, Q2 June 2026) end to end via /process-meeting: two knowledge graphs (183n/333e and 160n/314e) under ~/meeting-graph-output/, two recaps in Resources/Summaries/medbrief/, each with summary.md, timeline.md, graph.html and named-speaker transcripts. Resolved diarisation over-clustering by hand against the recording (March 8 clusters to 7 speakers; June 10 to 8, Mike Lewis collapsed from 3 clusters), and logged March's two strategic decisions (EMI employee share scheme + MedBrief Match launch) via /decision-log.

Two recovery notes: a session usage-limit killed two of the June Pass-3 relationship subagents mid-fan-out, so chapters 03-04 were salvaged from a complete-but-unrenamed .tmp (115 edges) and chapters 07-08 (74 edges) were hand-authored inline from the transcript. Separately, the deep extraction passes (Pass 1-3) for both meetings ran while the session was on Sonnet, before a mid-session switch to Opus; the graph builds, both summary.md/timeline.md, and both vault recaps were authored on Opus. Stopped at RECAP for both (no promote-to-store). Open follow-ups (non-blocking): log Q2's three decision candidates, and optionally regenerate the hand-built 07-08 edges via subagent.
