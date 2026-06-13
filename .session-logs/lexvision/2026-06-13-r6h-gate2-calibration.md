---
date: 2026-06-13
domain: lexvision
tags: [calibration, r6h, gate2, meeting-graph, graph-to-insight, verdict-harvest, kumulus, medbrief]
repos: [~/.claude, ObsidianVault]
parent:
---

# R6/H + GATE-2: first real-data calibration of the verdict harvest

Ran the first real-data calibration of the meeting-pipeline verdict-harvest instrument: seeded 5 real meetings oldest-first into an accumulating vault (3 Kumulus/lexvision: kumulus-medbrief 05-28 -> data-engineering 06-01 -> kumulus-regroup 06-12; 2 Medbrief: walkthrough 06-03 -> part2 06-08) via promote -> graph-to-insight (GTI_SEMANTIC=1) -> apply, write path `--apply --capture-verdicts` with NO `--live-write` (dropped after a /harden-plan pass showed it was unused scope and the only prior-note-mutation path). Filled an 802-record harvest; human_label_coverage 1.0.

**Result.** R6/H: Recall@8 = 1.0 / MRR = 0.392 over 147 measurable records (Recall@8=1.0 is partly structural; MRR is the real signal). GATE-2: 104 semantic-contradict signals fired, **0 genuine reversals (100% false-positive)**, failing in both directions (73 one-directional + 31 bidirectional, all skip); confirmed by a 16-judge adversarial workflow (12 unrelated-FP, 2 agreement, 2 refinement, 0 reversals). Headline carried to the Huble roadmap: the one-directional semantic-contradict can't route to REVISION on its own in a sparse vault; it needs a precision gate. Graded as a precision finding on a reversal-poor small-N corpus; does not unblock R7/R8.

**Process.** Plan hardened via /harden-plan (11-critic fan-out + pre-mortem) which caught a real bug: the draft promoted without `--valid-at`, so both Kumulus meetings would have collapsed to the same slug date and the oldest-first chain would have failed silently. Fixed a genuine `promote.py` robustness bug (count_quotes crashed on the DE graph's dict-shaped edge provenance). Worked around a zsh job-control quirk (heavy pipeline steps run from a script file) and a slice_select subprocess that wedged across an overnight laptop sleep (learning #68).

**Vault disposition.** All generated NOTES were reverted at Rowan's request - the meeting content belongs in the projects (Kumulus/DE -> lexvision-poc, walkthroughs -> medbrief-onboarding), not the strategic vault. Kept only the hidden harvest (git-ignored) and the 5-graph promote store. Conclusions + cleanup list left as local working notes in `~/claude_code/demo1/`.

**Owed on Huble:** the `--capture-verdicts --live-write` revision-approved end-to-end test, and folding the GATE-2 precision-gate finding into the R-series roadmap.

See [[reference_r6h_gate2_calibration]] (memory) and `~/claude_code/demo1/r6h-gate2-calibration-conclusions.md` (carry-back).
