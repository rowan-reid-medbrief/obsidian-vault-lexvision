---
session_id: [6f63d4c7-4e81-4b0a-88f7-1d1e0e1338d1]
title: "Copilot as a sub-agent substrate: plan + 12-agent hardening"
type: wrap-up
domain: medbrief
created: "2026-07-23"
parent: null
tags: [session-log, medbrief, gh-copilot, harden-plan]
---

# Copilot as a sub-agent substrate: plan + 12-agent hardening

## Session summary

Designed and hardened a plan to route sub-agent work onto the GitHub Copilot CLI whenever Claude would otherwise fan out, with `/harden-plan` as the first caller. A 12-agent Claude fan-out produced ~60 findings, including three that killed parts of the draft: the target MedBrief repo has private keys tracked in git and reachable by Copilot's read tool, `harden-plan` has no `Bash` in `allowed-tools` so it cannot dispatch at all, and a failed Copilot leg was indistinguishable from a leg that found nothing. Rowan then caught four further flaws the fan-out missed, all of them premises seeded into the grounding digest, which is the session's most durable finding (#k3mq7w).
