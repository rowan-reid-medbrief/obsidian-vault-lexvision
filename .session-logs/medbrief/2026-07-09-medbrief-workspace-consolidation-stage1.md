---
date: 2026-07-09
project: /Users/Rowan.Reid/claude_code/projects/apprise-viewer-rendering
domain: medbrief
session: Designed and began (Stage 1) consolidating MedBrief Claude work into one medbrief-work workspace nesting the product checkout
type: wrap-up
tags: [medbrief, mri-134, workspace-setup, harden-plan, project-structure, git, mutagen]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/apprise-viewer-rendering
    commit: d575161
  - path: /Users/Rowan.Reid/.claude
    commit: 340ea09
model_check: not-needed
---

## Session Summary

Decided to consolidate the scattered MedBrief Claude work into one vault-coupled `medbrief-work` workspace nesting the live GitHub product checkout as a gitignored `repo/`, then ran a full `/harden-plan` pass (eight parallel critics) that reshaped it: nesting alone does not stop stray tracking files leaking into the vendor repo (a `.git/info/exclude` guard does), annotations is excluded for good, and the checkout move must quiesce a live mutagen sync first. Stage 1 executed and verified (leak-guard applied to the checkout and proven, apprise committed and backed up to a bundle); Stages 2-5 (rename, move the checkout, re-point mutagen, fix pointers) are captured in `docs/MIGRATION-STATE.md` for a fresh neutral-cwd session, since they rename this session's own project root.
