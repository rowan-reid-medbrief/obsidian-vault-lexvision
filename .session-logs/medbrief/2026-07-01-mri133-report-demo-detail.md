---
date: 2026-07-01
project: /Users/Rowan.Reid/claude_code/projects/annotations
domain: medbrief
session: Deepened the MRI-133 bake-off report and demo index for the live Deon walkthrough
type: wrap-up
tags: [mri-133, medbrief, bake-off, report, demo, redaction]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/annotations
    commit: 2f59e71cf7ef42b9147dcac6c8f3387fa92984fc
model_check: not-needed
---

## Session Summary

Deepened the MRI-133 bake-off report and demo for the live Deon walkthrough. Report: added an always-on per-scenario "worst silent-error" callout plus a `--by-case` table (the headline `exact_hash` 5.6% silent hides 100% on SPLIT / 33% on REMOVED), hid the conformal block and header alpha behind `--conformal` for a cleaner demo, and neutralised the DoD note to "pending decision" (removed all Deon references). Demo `index.html` gained a page-correspondence view (per-scenario original->re-sorted table + per-image origin captions) so which re-sorted page is which original is legible, driven from the ground-truth mapping the demo already computed. Commit 2f59e71 also swept up a concurrent session's uncommitted `report_html.py` (complement-named HTML report, `--html`), `docs/matcher-strengths.md`, and a relocate ABSTAIN-queue path for DUPLICATE annotations; 231 poc tests green. Captured the clean-only bake-off gap (degraded corpus generated but never matched) as a project memory + a docs/IDEAS.md item.
