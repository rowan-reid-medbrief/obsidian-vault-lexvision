---
session_id: [304e94b3-0b05-4dcf-b79e-dc2fbe776bba]
date: 2026-07-23
project: /Users/Rowan.Reid/claude_code/demo1
domain: medbrief
session: Frame-interrogated the Copilot-substrate plan twice (Fable + gpt-5.6-sol converged on the fifth premise); rewrote to r3; cleared three red eval suites and pushed the config repo
type: handoff
tags: [gh-copilot, harden-plan, copilot-substrate, frame-audit, model-diversity, eval-net]
repos:
  - path: /Users/Rowan.Reid/.claude
    commit: 79f9d05
parent: 2026-07-23-copilot-subagent-substrate-hardening.md
model_check: fired-downgrade (both; interrogation ran on fable/max as planned, execution handed to a sonnet/high session)
---

## Session Summary

Interrogated the r2 Copilot-substrate plan at frame level twice: a max-effort Fable pass and an out-of-family gpt-5.6-sol consult (57.1 credits, 69 s) independently converged on the same fifth premise (the orchestrator's beliefs enter the pass as context, never as content under test), and the consult added one verified catch (grounded-bucket verification is a read, not a grep). Rewrote the plan to r3: frame-audit leg adopted, claims manifest replaces the digest, the eleven-leg lens offload demoted to the thing the three-arm seeded bake-off must prove. Also cleared the three unlisted red suites (taxonomy, voice-reconcile, registry-index), pushed `~/.claude` (79f9d05), and handed execution to a fresh Sonnet/high session.

## Continuation Prompt

## Continuation: Copilot substrate r3: execute the build (steps 1-3)

**Parent session:** 2026-07-23-copilot-substrate-r3-interrogation.md

### Context
The Copilot-as-sub-agent-substrate plan is at r3 after two independent frame interrogations
(a max-effort Fable pass, then a gpt-5.6-sol consult through the wrapper itself; both converged
on the same fifth premise: the orchestrator's beliefs entered the pass as context, never as
content under test). The frame-audit leg is adopted now; the eleven-leg lens offload stays
unproven until the seeded bake-off. This session executes the build. Run it on Sonnet at high
effort: it is standard, careful coding work, and the house rule keeps Fable off mechanical
builds.

### What was done this session
- Fable frame interrogation of r2: fifth premise named; the hygiene-sweep-fails-condition-1
  contradiction caught; deny-path read-scoping found undocumented in CLI help 1.0.73.
- Out-of-family check: one consult (gpt-5.6-sol requested, 57.1 credits, 69 s) independently
  converged on the same premise, added one verified catch (grounded-bucket verification is a
  read, not a grep; harden-plan SKILL.md steps 3-4), and proposed the same three-arm test.
  Ledger line appended to offload-policy.md.
- Plan rewritten to r3 at `~/.claude/plans/copilot-as-subagent-substrate.md` (machine-local,
  gitignored; read it in full before building, it is the whole brief).
- Housekeeping: the three unlisted red eval suites cleared (delegation-scout taxonomy record;
  voice frozen snapshot 66 to 70; registry regenerated); `~/.claude` pushed clean.

### Current state
- `~/.claude` at 23a01f2, pushed, net gate green. Vault at d7cf67d, pushed. demo1 clean.
- Plan: r3, twice-interrogated, pre-execution. Nothing built yet. Nothing time-pressured.
- gh-copilot's shakedown stamp is knowingly behind (2026-07-18 vs changes dated 2026-07-23);
  accepted at wrap-up, to be re-run and restamped as part of this build.

### Where we left off
r3 approved for execution; this is the build session.

### Next steps (in order; the plan's Sequencing section is the authority)
1. Sequencing step 1: the cooldown config keys (`cooldown_max_dispatches`,
   `cooldown_window_seconds`) per plan section 8: optional-key pattern, explicit bool and zero
   rejection, `_resolve_cooldown` at both call sites, tests red before green (the list is in
   the plan), five prose sites plus the `.example` and MAINTENANCE.md.
2. Sequencing step 2: the read-scope deny grammar test FIRST on a fixture repo (path scoping is
   documented for write() only in `copilot help permissions` on 1.0.73); then `--add-dir` on
   consult and review scoped to per-run directories; deny-paths per the grammar outcome; the
   preflight secret scan. File the untrack-and-rotate key remediation on the MedBrief backlog.
3. Sequencing step 3: the offload-policy sub-agent-dispatch clause with the two-use split
   (frame diversity adopt-now; lens capacity test-first); split the ledger to its own file
   first.
4. Re-run the gh-copilot shakedown checklist (`references/shakedown.md`) against a real run and
   update `metadata.last_shakedown` (clears the accepted-behind stamp from this wrap-up).
5. Then stop. Steps 5 to 8 (the seeded synthetic plan, the blind arms, adjudication) are
   separate sessions by design: the seeding session must end to preserve blindness.

### Key references
- The plan (the whole brief): `~/.claude/plans/copilot-as-subagent-substrate.md` (r3)
- Wrapper source: `~/.claude/skills/gh-copilot/scripts/` (delegate, profiles, worktree, tests)
- Flag truth: `~/.claude/skills/gh-copilot/references/modes.md`; policy + ledger:
  `references/offload-policy.md`
- First caller: `~/.claude/skills/harden-plan/SKILL.md`
- Learning: `~/.claude/learnings/k3mq7w.md`

### Notes for next session
- A tooling-reflection item (the wrap-up scan's undocumented `<project-cwd>` argument) sits in
  the queue and will surface at that session's own wrap-up; route it then.
- The consult envelope and audit text live only in this session's scratchpad; the durable
  record is the offload-policy ledger line and the plan's r3 delta section.
