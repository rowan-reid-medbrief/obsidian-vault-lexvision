---
tags: [mri-133, medbrief, poc, bakeoff, reporting, redaction-demo, copilot-audio]
repos: [claude_code/projects/annotations]
model_check: not-needed
---

# 2026-07-01 - MRI-133: visual bake-off report + audio walkthroughs

Deep-dive session on the MRI-133 matching PoC, delivered largely as narrated audio under co-pilot audio mode: a ~35-min system walkthrough, an explainer of how precision / recall / abstention-correctness / queue relate (each is the same page-split seen through a different denominator), and a per-matcher strengths write-up (`docs/matcher-strengths.md`) whose headline is that splitting defeats every matcher, pointing at lineage rather than matching. Built a self-contained visual bake-off HTML report (`poc/src/mri133/scoring/report_html.py`, wired into `mri133 run` and `report --html`) that renders every percentage with its named complement: a master page-split bar (confident-correct / silent-error / safe-abstain / over-abstain) plus one bar per metric against its own denominator, a one-line "how it works" under each matcher, and a scenario glossary; also narrated a guided tour of the b2 redaction-safety demo page. Exposed raw bucket counts in `report.board()`; 22 report tests green.

A concurrent session was active in the same repo (touching demo/relocate/dod files and adding two project memories); committed only the report-visualisation files and left the rest alone.
