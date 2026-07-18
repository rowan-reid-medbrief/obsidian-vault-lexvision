---
date: 2026-07-18
project: /Users/Rowan.Reid/claude_code/demo1
domain: medbrief
session: gh-copilot post-merge shakedown closed (probes 1+11 PASS) and the propose-and-paste offload spotter shipped
type: wrap-up
tags: [gh-copilot, shakedown, allowed-tools, copilot-offload, harden-plan, workflow, ideas]
repos:
  - path: /Users/Rowan.Reid/.claude
    commit: a15c3cf
parent: 2026-07-18-gh-copilot-s7-merge-acceptance.md
model_check: not-needed
---

## Session Summary

Closed the gh-copilot shakedown in the fresh post-merge session: probes 1 and 11 both PASS (probe 11 positive, with the discovery that compound Bash commands defeat scoped permission grants), scoped `allowed-tools` adopted (SKILL.md v1.1, `last_shakedown: 2026-07-18`), programme worktree removed. Then planned, hardened (12-critic pass), and shipped the propose-and-paste offload spotter for this machine: Claude spots MedBrief offload chunks and hands over paste-ready `/gh-copilot` commands, MedBrief-only egress, ledger plus review checkpoint (`a15c3cf`). Deferred-architecture triggers logged as #0t0i70 (cloud agent) and #4nxpy3 (SDK server).
