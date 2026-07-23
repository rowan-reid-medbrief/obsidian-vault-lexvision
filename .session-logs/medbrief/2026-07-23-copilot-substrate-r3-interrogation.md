---
session_id: [304e94b3-0b05-4dcf-b79e-dc2fbe776bba]
date: 2026-07-23
project: /Users/Rowan.Reid/claude_code/demo1
domain: medbrief
session: Frame-interrogated the Copilot-substrate plan twice (Fable + gpt-5.6-sol converged on the fifth premise); rewrote to r3; cleared three red eval suites and pushed the config repo
type: wrap-up
tags: [gh-copilot, harden-plan, copilot-substrate, frame-audit, model-diversity, eval-net]
repos:
  - path: /Users/Rowan.Reid/.claude
    commit: 79f9d05
parent: 2026-07-23-copilot-subagent-substrate-hardening.md
model_check: fired-downgrade (both; interrogation ran on fable/max as planned, execution handed to a sonnet/high session)
---

## Session Summary

Interrogated the r2 Copilot-substrate plan at frame level twice: a max-effort Fable pass and an out-of-family gpt-5.6-sol consult (57.1 credits, 69 s) independently converged on the same fifth premise (the orchestrator's beliefs enter the pass as context, never as content under test), and the consult added one verified catch (grounded-bucket verification is a read, not a grep). Rewrote the plan to r3: frame-audit leg adopted, claims manifest replaces the digest, the eleven-leg lens offload demoted to the thing the three-arm seeded bake-off must prove. Also cleared the three unlisted red suites (taxonomy, voice-reconcile, registry-index), pushed `~/.claude` (79f9d05), and handed execution to a fresh Sonnet/high session.
