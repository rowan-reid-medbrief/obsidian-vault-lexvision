---
date: 2026-07-04
project: /Users/Rowan.Reid/claude_code/medbrief
domain: medbrief
session: "MRI-134: root-caused the whole-document viewer's dev-VM 500 (Azure blob 403), committed the XOD page-subset branch, then reviewed the parked PDF-split branch"
type: wrap-up
tags: [mri-134, apryse, xod, page-subset, azure, performance, medbrief]
repos:
  - path: /Users/Rowan.Reid/claude_code/medbrief
    commit: ad3897467406aa65347c21bf29d4357c2134ad97
model_check: not-needed
---

## Session Summary

Debugged why the plain (non-subset) whole-document viewer 500'd on the dev VM: live SSH/log inspection traced it to the dev VM's Azure Blob Storage credentials returning 403, a pre-existing gap since `streamOcrXodAction` (unlike the new page-subset endpoint) has no local fallback. Added then, on explicit request, reverted a TEMPORARY dev-only fallback; also deleted `docs/SDD/codingStandards.md` (accidental branch carryover). Re-verified and settled the XOD zip-surgery throughput figures for Rowan to quote to Deon (~65ms/page steady-state after a ~4s fixed source-open cost, ~15.4 pages/sec, versus ~3.5 pages/sec for the rejected on-the-fly re-conversion path). Committed `feature/MRI-134-page-subset-extraction` as `5be7c41b7` (local only, not pushed), confirmed the three related MRI-134 branches and the single git worktree, then switched to and reviewed the parked `feature/MRI-134-pdf-split-approach` branch. Logged an idea (permanent Azure blob-fallback for `streamOcrXodAction`, committed `ad389746`) via `/close-out`.
