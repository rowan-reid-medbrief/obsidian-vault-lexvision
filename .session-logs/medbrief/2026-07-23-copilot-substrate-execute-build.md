---
session_id: [602fca14-d0be-4d68-b01e-6eb29b7532ce]
tags: [gh-copilot, shakedown, read-scope, wrap-up, copilot-substrate]
repos:
  - "~/.claude: 9e2afb2"
  - "medbrief-onboarding: 0164633"
parent: 2026-07-23-copilot-substrate-r3-interrogation.md
model_check: not-needed
---

Executed r3 sequencing steps 1-4 of the Copilot sub-agent substrate: cooldown config keys, the read-scope controls, the offload sub-agent clause with the ledger split out, and the operator artefacts. Both read-scope probes were dispatched and returned (--add-dir grants reads under the deny-first profile, cwd confinement holds, a scoped read() deny is wholesale), so the --add-dir plumbing was built on evidence and proven end-to-end at shakedown. Shakedown probes 4-10 re-run PASS for 40.63 credits and refuted a load-bearing s6 pin: shell execution is gated by path, not by the tool allow-list, though a bare write deny still blocks every write route. Three commits in ~/.claude, net gate green, unit suite 132; last_shakedown held at 2026-07-18 pending one fresh-session check.
