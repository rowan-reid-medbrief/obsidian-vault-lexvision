---
tags: [gh-copilot, programme, worktree, implement-mode, harden-plan, merge-gate, security, red-first]
repos:
  - ~/.claude @ main (idea log #rf5ar4); branch gh-copilot @ 2433812 (s4 implement mode)
  - ObsidianVault (session log + memory mirror)
model_check: not-needed
---

# gh-copilot s4: implement mode (worktree isolation, lock, confirm gate)

Shipped s4 of the gh-copilot programme (M2): the isolated-worktree implement mode, built red-first (85 tests) then to green through the full conduct relay - `/harden-plan` (a 13-lens opus fan-out, 63 findings adjudicated), an independent red-author then green-builder, and a three-lens adversarial merge-gate that caught two plan-mandated defences missing behind the green suite (a cleanup pointer-tamper diff leak under `--force`, and an empty `effective_allowances` on the dry-run approval surface), both fixed and re-verified (the leak test was proven to bite against the unpinned code). Rowan deferred the `--allow-cmd` shell-allowance subsystem out of v1 (#rf5ar4). Lock lives in the dispatcher; the worktree module is pure git-over-git_scope with no subprocess. Committed on the branch (2433812); estate gate PASS; handing off before s5. All fan-outs ran on the opus fallback because the Fable burst is out of subagent credits on this machine.


## Continuation Prompt

## Continuation: gh-copilot programme - next session (s5)

**Parent session:** 2026-07-18-gh-copilot-s4-implement-mode.md

### Context
gh-copilot is a tracked programme (spine at `~/.claude/docs/programmes/gh-copilot.md`) building a policy-enforcing wrapper that lets Claude Code delegate bounded tasks to the GitHub Copilot CLI (MedBrief Copilot Business seat) through official interfaces only. It runs in-place on the `gh-copilot` branch, held in a linked worktree at `~/.claude/.claude/worktrees/programme/gh-copilot`, while the primary `~/.claude` checkout stays on main. M2 (build to green on the mock) is nearly done; s5 is its last spec.

### What was done this session
- Shipped **s4** (implement mode): the isolated-worktree module, per-repo lock 2x2, confirm/dry-run gate, and signal-handler lock teardown, built red-first (85 tests) then to green.
- Full conduct relay: `/harden-plan` (13-lens opus fan-out, 63 findings adjudicated), an independent red-author then green-builder, and a three-lens adversarial merge-gate.
- The merge-gate caught two plan-mandated defences missing behind green tests, both fixed and re-verified: the finding-46 `--git-dir`/`--work-tree` pin on cleanup's worktree reads (a tampered `.git` pointer could leak another repo's diff under `--force`; the new test was proven to bite), and an empty `effective_allowances` on the dry-run approval surface.
- Rowan deferred the `--allow-cmd` shell-allowance subsystem out of v1 (backlog `#rf5ar4`).

### Current state
- Branch `gh-copilot` tip `edd1c2a` (s4 SHIPPED ledger) over `2433812` (s4 code). Machine-local, unpushed by policy. Spine live copy is the worktree copy; `~/.claude` main is stale-by-design.
- Shipped: s1, s2, s3, s4. Ready: s5. Blocked: s6<-s5, s7<-s6.
- `~/.claude` main ahead of origin (config push opt-in/off): idea `#rf5ar4` committed locally (`5baa667`), not pushed.

### Next steps
1. In the fresh window, run **`/programme next`** for gh-copilot - it reads the live spine (s4 now SHIPPED) and emits the never-stale launch prompt for **s5**. Do NOT hand-brief from this snapshot; `/programme next` is the source of truth.
   - s5 = "Skill, references, estate wiring" (sonnet/high, attended, needs_subplan:false): SKILL.md (<500 lines, `disable-model-invocation: true`), references/modes.md, references/shakedown.md (STATUS: PENDING), gh-copilot.json.example, the .gitignore line, the EVAL-TAXONOMY.md record, the MAINTENANCE.md section, and tests/skills/gh-copilot/test-gh-copilot.sh. DoD: /gh-copilot discoverable; registry and taxonomy-sync checks green; full tests/run.sh green on the branch with zero new KNOWN-RED.
2. Fold two s4 carry-forwards into s5: the `envelope_version: 1` seam-doc reconciliation (credits_reported + task_id + the preflight-only fields), and confirm whether the s3 `${CLAUDE_SKILL_DIR}` pin was actually recorded (hardening finding 49) - if not, carry it as an s3 slip, not silently reassigned.

### Key references
- Spine: `~/.claude/docs/programmes/gh-copilot.md` (read sections 1-2 fresh at start).
- Plan of record: `/Users/Rowan.Reid/.claude/.claude/worktrees/programme/gh-copilot/docs/plans-archive/gh-copilot-delegation.md` (sections 4, 5, 7, 10).
- s4 sub-plan (ephemeral, still on disk): `~/.claude/plans/gh-copilot-s4.md`.
- Conduct loop: `~/.claude/skills/programme/references/conduct-loop.md`.
- Backlog `#rf5ar4` (deferred --allow-cmd); rank via `/whats-next --central`.

### Notes for next session
- **The Fable burst binding is out of subagent credits on this machine.** Every fan-out this session (hardening, build relay, merge-gate) had to be pinned to `model: 'opus'` explicitly, or it failed with "Usage credits are required for this model." Pin opus on any Agent/Workflow fan-out until the burst window is refreshed or closed.
- s5 is lighter (docs + estate wiring) and less fan-out-heavy than s4.
