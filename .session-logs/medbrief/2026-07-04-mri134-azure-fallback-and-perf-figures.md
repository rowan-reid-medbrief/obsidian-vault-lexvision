---
date: 2026-07-04
project: /Users/Rowan.Reid/claude_code/medbrief
domain: medbrief
session: "MRI-134: root-caused the whole-document viewer's dev-VM 500 (Azure blob 403), added a temporary local fallback, flagged a stray branch-carryover doc, and settled the throughput figures to quote to Deon"
type: wrap-up
tags: [mri-134, apryse, xod, page-subset, azure, performance, medbrief]
repos:
  - path: /Users/Rowan.Reid/claude_code/medbrief
    commit: dd0154a881f67e8cc8be001e591e51aefa2df50f
model_check: not-needed
---

## Session Summary

Debugged why the plain (non-subset) whole-document viewer 500'd on the dev VM: live SSH/log inspection traced it to the dev VM's Azure Blob Storage credentials returning 403, a pre-existing gap since `streamOcrXodAction` (unlike the new page-subset endpoint) has no local fallback. Added a clearly-marked TEMPORARY dev-only fallback to unblock testing, and flagged `docs/SDD/codingStandards.md` as likely accidental carryover from an earlier backup commit on a sibling branch rather than genuine work. Also re-verified and settled the performance figures for the chosen XOD zip-surgery method (~65ms/page steady-state after a ~4s fixed source-open cost, ~15.4 pages/sec) against the rejected on-the-fly re-conversion path (~3.5 pages/sec), for Rowan to quote to Deon. Branch remains entirely uncommitted per standing preference; that preference was also reinforced in memory this session.
