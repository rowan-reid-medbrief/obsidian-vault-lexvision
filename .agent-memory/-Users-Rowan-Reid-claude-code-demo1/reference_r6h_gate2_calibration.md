---
name: reference_r6h_gate2_calibration
description: "First real-data R6/H + GATE-2 calibration of the meeting-pipeline verdict harvest (2026-06-13). Result, data locations, and what is still owed on Huble."
metadata: 
  node_type: memory
  type: reference
  originSessionId: 0147a065-5cfc-4d46-85ab-7ac7556139fa
---

First real-data calibration of the verdict-harvest instrument (R6/G), run 2026-06-13 on the Lexvision laptop. Seeded 5 real meetings oldest-first into an accumulating vault, write path `--apply --capture-verdicts` (no `--live-write`), across 2 projects: Kumulus/lexvision (kumulus-medbrief 05-28 -> data-engineering 06-01 -> kumulus-regroup 06-12) and Medbrief (mb-product-walkthrough 06-03 -> walkthrough-part2 06-08).

**Result.** R6/H: Recall@8 = 1.0, MRR = 0.392 over 147 measurable records (Recall@8=1.0 is partly structural; MRR is the informative signal). human_label_coverage = 1.0. GATE-2: 104 semantic-contradict signals fired, **0 genuine reversals (100% false-positive)**, failing in both directions (73 one-directional + 31 bidirectional, all skip); confirmed by 16 adversarial judges (12 unrelated-FP, 2 agreement, 2 refinement, 0 reversals). Headline: the one-directional semantic-contradict can't route to REVISION on its own in a sparse vault; it needs a precision gate. Graded honestly as a precision finding on a reversal-poor small-N corpus; does NOT unblock R7/R8.

**Data locations.** Harvest (802 records, 0600, git-ignored, machine-local): `{vault}/.meeting-graphs/.harvest/verdicts.jsonl`. The 5-graph promote store (kept): `{vault}/.meeting-graphs/{graph_id}/`. Conclusions / carry-back note for the Huble roadmap: `~/claude_code/demo1/r6h-gate2-calibration-conclusions.md`. Mis-placed-content cleanup list: `~/claude_code/demo1/calibration-misplaced-cleanup.md`.

**Vault state.** All generated NOTES were reverted (content belongs in lexvision-poc / medbrief-onboarding, not the strategic vault); only the hidden harvest + store remain. See [[reference_meeting_graph_outputs]].

**Still owed on the Huble machine** (not done here): the `--capture-verdicts --live-write` end-to-end test for the `revision-approved` disposition; and folding the GATE-2 precision-gate finding into the R-series roadmap.
