---
date: 2026-07-05
type: wrap-up
tags: [mri-133, annotations, medbrief, matchers, fusion-rule, median-rescue, safety-gate]
repos:
  - annotations: c6d2c98
parent: 2026-07-05-mri133-ceiling-harden-lever-b-cut.md
model_check: not-needed
---

# MRI-133: median-fusion Lever A failed its real-corpus safety gate; shipped a mean-primary/median-rescue hybrid instead

Built Lever A (median fusion) exactly as planned; its real-corpus safety gate caught a severe
regression (1 new silent error, recall/queue both worse, concentrated in PLAIN/REPAGINATION -
median inflates a wrong candidate's near-tie score on boilerplate-heavy docs as readily as the
right one's). Reverted the default and, per Rowan's call, redesigned as a mean-primary/
median-rescue hybrid (upgrade-only: only rescues pages mean already queues, never touches an
already-resolved page); its real-corpus gate passed clean (zero new silent, +48 pages resolved,
recall 0.673->0.676, queue 0.327->0.323). Also shipped the honest per-doc content-ceiling script
for Deon and fixed a run_bakeoff config-plumbing gap. DoD still MARGINAL, not GOOD; 331 tests
green, committed (c6d2c98) but not pushed.
