---
date: 2026-06-12
project: /Users/Rowan.Reid/claude_code/projects/lexvision-poc
domain: lexvision
session: meeting-graph on the Kumulus Regroup, then a hardened 3-tier fix to the meeting-graph and meeting-graph-eval skills
type: wrap-up
tags: [meeting-graph, meeting-graph-eval, kumulus, harden-plan, skill-fixes, diarization]
repos:
  - path: /Users/Rowan.Reid/.claude
    commit: meeting-graph + meeting-graph-eval skill fixes
---

## Session Summary

Ran `/meeting-graph` on the Kumulus Regroup recording (Rowan presenting his Kumulus research to Deon Kuhn and Laura Gongas), fetched from SharePoint via Chrome cookies; produced a 170-node / 336-edge graph after resolving pyannote over-clustering (4 clusters resolved to Rowan/Laura/Deon by inspecting longest turns) and patching 6 cross-verified misses surfaced by `/meeting-graph-eval` (recall lower-bound ~48% against a hair-split 320-item reference; the leniency gate PASSED on an independent adversarial pass, so the number is trustworthy as a floor; true substantive coverage is well above it).

Then hardened (via `/harden-plan`: an 8-lens grounded fan-out that caught a path-double-nesting bug the draft would have shipped) and implemented a 3-tier fix to the `meeting-graph` and `meeting-graph-eval` skills: a shared `align.py` `speaker_stats.json` feeding guarded Person-timing stamping in `build_graph.py` and a one-row-per-speaker `analytics.py` table (closing the triple-count and the n/a-timing bug, resolving learning #60), Chapter `frame_ids`/`representative_frame_id` in the `visual:NNNN` node-id space, the `eval_report.py` string-`ts` crash (coerced at ingest), the `diarize.py` wrong-interpreter message, a new `merge_batches.py` helper plus the leniency-gate run-both-passes wiring, and a new `inspect_clusters.py` diagnostic. Verified every fix against the retained fixture (over-clustering sum, a synthetic two-same-first-name guard, frame-id resolution, the diarisation honesty negative-path, file-absent back-compat, and all downstream consumers). Logged 2 out-of-scope follow-ups (SCHEMA_VERSION producer/consumer drift; promote-graph dangling timeline images).
