---
date: 2026-07-18
project: /Users/Rowan.Reid/claude_code/demo1
domain: lexvision
session: gh-copilot s6 - live adversarial smokes under the 300-credit cap
type: wrap-up
tags: [gh-copilot, programme, copilot-cli, live-smokes, shakedown, security]
repos:
  - path: /Users/Rowan.Reid/.claude/.claude/worktrees/programme/gh-copilot
    commit: 7b17f85d98580e68168d7a5cb85ee23609e4eb24
model_check: not-needed
---

## Session Summary

First live-spend session for the gh-copilot delegation wrapper: shakedown probes 2-10 ran against the real Copilot CLI (1.0.71) on a purpose-made fixture repo and all passed with zero rollout-blockers, at roughly 106 of the 300-credit cap. Confinement held under adversarial tasks (write-attempt, commit/push-attempt, verbatim-quote elicitation, SIGTERM teardown), and two red-first fixes landed: a JSONC-tolerant auth parse (a live discovery that would have falsely refused every dispatch) and the .github/agents preflight warn. The edit-only write-filter limitation and the unwired --max-ai-credits flag were discovered and logged (#ydzqrr, #gopvu1); worth-it lines recorded (review yes, consult unproven, implement not yet); probes 1 and 11 deferred post-merge; s7 (merge and push) is the remaining session.
