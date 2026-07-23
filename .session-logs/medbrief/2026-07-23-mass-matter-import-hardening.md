---
session_id: [73610914-7242-4b20-81bc-efbb120a49d7]
tags: [medbrief, mass-matter-import, harden-plan, gh-copilot, hardening]
repos:
  - medbrief-work: 1dcd383
parent: 2026-07-22-mass-matter-import-briefing-and-design.md
model_check: fired-downgrade
type: handoff
---

# Mass Matter Import: hardening pass and re-target on a local goal

Resolved the three carried blockers (account = Higgs LLP 296, verified against pre-staging; access-role and transactions designed), settled a first-class dry-run + declarative-check-framework design, then ran a full /harden-plan pass (14 Claude critics + 11 out-of-family Copilot lens legs, 907.6 Copilot credits across the day) that found the plan was built on three false premises: setManager() is actually sufficient for access and listing, the bootstrap should create one Collection not four, and two existing importers were missed by a bad search glob. Wrote a fresh short LOCAL-BUILD.md for the near-term goal Rowan ruled (a local dry run and a local committing run with discs left pending), and parked the long-form plan for redraw. The recurring lesson, now logged: a citation-check is not a control-flow check.
