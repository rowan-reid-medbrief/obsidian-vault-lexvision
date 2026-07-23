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

## Continuation Prompt

## Continuation: Mass Matter Import - build the first local version

**Parent session:** 2026-07-23-mass-matter-import-hardening.md

### Context
A one-off bulk import of the client Higgs' matters plus radiology/hospital records into MedBrief, built as a Symfony console command in the product checkout (`repo/`). This session hardened the plan (14 Claude critics + 11 out-of-family Copilot lens legs) and three premises the whole project rested on turned out FALSE. The plan was re-targeted to a small local goal, and a fresh `LOCAL-BUILD.md` written. Your job is to build it.

### What was done this session
- Ran a full `/harden-plan` pass. Consolidated 64 findings in `~/.claude/plans/.harden-runs/mass-matter-import/CONVERGENCE.md`.
- Corrected three false premises in DESIGN-NOTES (all verified by hand against source, twice, after two earlier claims accepted on a citation-check alone turned out false):
  1. **`setManager()` IS sufficient** for both record-tree access (`ProjectVoter:411-422`) and listing (`UserRestrictableQueriesTrait:180-183`, "Always show projects where the user is the Manager"). The "access-role gap", the project's headline finding, was not real.
  2. **Create ONE Collection (Private), not four.** `Project::__construct()` already makes Records + Unsorted Records; copying the deprecated `createAction` orphans three rows per matter.
  3. **Importers already exist**: `ImportMattersController`, a broken-in-prod `ProjectFactory`, and a non-deprecated `ImportRadiologyCommand`. The old search globbed `*MatterImport*` and missed `ImportMatters*`.
- Wrote `docs/mass-matter-import/LOCAL-BUILD.md`, the current plan.

### Current state
- `medbrief-work` @ `1dcd383` (main): all mmi doc corrections + `LOCAL-BUILD.md` committed.
- `~/.claude` @ `9290110`: three ideas + a learning + the lens-fan-out ledger line, committed LOCALLY only (the config push was blocked by the eval-net gate; it will push from a later session).
- Vault: this session's log written and pushed.
- No code written yet. `repo/` is the MedBrief product checkout (Symfony/PHP), synced to the dev VM by mutagen.

### Where we left off
LOCAL-BUILD.md is complete and current. One decision is deliberately left open at the top of it, and it should be settled before building the write path.

### Next steps
1. **Settle the one open decision (do this first): drop the `ROLE_PROJECT_{id}_PROJECTMANAGER` grant, or keep it?** `setManager()` alone now suffices, so the recommendation (DESIGN-NOTES section 16.1a) is to drop it: it is the only write touching pre-existing shared rows, cannot be undone, and carries a duplicate-append bug and a concurrency hazard. It was Rowan's ruling originally, so ask him.
2. Build `LOCAL-BUILD.md` step 1 onward, test-first: command skeleton then account resolution then the check framework (with `scope` and the severity map from the start) then sheet parser then tree walk then the local checks then the report then the write path. Steps 1 to 3 need nothing external.
3. The highest-value test, named in the plan: assert a no-`--commit` run leaves row counts unchanged (dry-run and `--commit` share one code path).
4. Apply the section 16.2 ruling: resolve the fee earner SCOPED to account 296, hard-stop outside it, and widen `fee_earner.is_account_manager` to report the broadest `ROLE_ACCOUNT_296_*` held (Higgs' `default_role` is ADMINISTRATOR).
5. Design around the five verified defects in LOCAL-BUILD.md (the `wrapInTransaction` EntityManager-close is the one that will bite first).
6. Optional 10-minute check Rowan wanted: is Copilot `implement` really edit-only? The claim came from policy prose, never verified against the wrapper source. If new files work (or the scaffold-then-fill route works), much of the build could be offloaded.
- Deferred this session to IDEAS: harden-plan needs a "redraw not patch" branch (as docs/ideas/p9k3wm.md via /log-idea); run `/whats-next --central` to rank.

### Key references
- `docs/mass-matter-import/LOCAL-BUILD.md` - THE plan. Start here.
- `docs/mass-matter-import/DESIGN-NOTES.md` section 16 - the corrections and rulings. Section 11.5 is marked do-not-build-from.
- `~/.claude/plans/.harden-runs/mass-matter-import/CONVERGENCE.md` - all 64 findings with citations.
- `docs/mass-matter-import/copilot-briefs/mmi-reuse-decision.task` + its answer in the run dir's `legs/reuse-decision.answer.md` - the reuse matrix (Q1/Q3/Q4 not yet read).
- Product code: `repo/` (Symfony/PHP). Line citations accurate as of 2026-07-23; re-verify.

### Notes for next session
- **The load-bearing lesson: a citation-check is not a control-flow check.** Every claim accepted by verifying the cited lines said what was claimed was false (there were four); every one re-verified by reading the surrounding control flow held. When a consult or a single critic asserts a mechanism, read the enclosing block and the callers, not just the cited span. Idea `k7q2vn` captures this.
- Real Higgs data cannot leave the VM (D7), so local runs use synthetic fixtures and prove the framework, not correctness against the real shape. Fixtures need a database half (four checks read live estate state); `doctrine/data-fixtures` is already in require-dev.
- Consider `/model sonnet` + `/effort high` for the build: it is standard coding against a settled plan, and it stretches the Claude budget.
- The Friday 10:30 Deon catch-up now has a real question batch: the role-grant decision, the environment/production target (Phase 6 currently lands nowhere the client can use), the estate bug in `ProjectFactory`, severities, `CLAIM_CATEGORY_OTHER`, sizing.
