---
date: 2026-07-18
project: /Users/Rowan.Reid/claude_code/demo1
domain: medbrief
session: gh-copilot s7 - merge to main, push, acceptance sweep; programme complete
type: handoff
tags: [gh-copilot, programme, copilot-cli, merge, acceptance-sweep, estate-tests]
repos:
  - path: /Users/Rowan.Reid/.claude
    commit: 0627086
model_check: fired-downgrade (model)
---

## Session Summary

Programme gh-copilot closed at s7: clean revert rehearsed and recorded, branch merged to main
(`0627086`) and pushed, section 10 acceptance sweep recorded through a three-lens merge-gate. The
post-merge estate gate surfaced a pre-existing machine-environmental red (no live mcp.json),
recorded in the KNOWN-RED.local overlay. Follow-up: probes 1 and 11 in a fresh session;
use-it-or-lose-it clock to 2026-08-17.

## Continuation Prompt

## Continuation: gh-copilot post-merge probes (1 + 11)

**Parent session:** 2026-07-18-gh-copilot-s7-merge-acceptance.md

### Context
The gh-copilot programme (Copilot CLI delegation: the `/gh-copilot` skill plus its policy wrapper) completed at s7 on 2026-07-18: branch merged to main, pushed, spine `status: complete`. Two shakedown probes were deliberately deferred because they only work in a fresh session where the skill is discoverable from the primary checkout.

### What was done this session
- Clean-revert rehearsal PASS (merge `4134b3e` reverted by `60564a6`, tree byte-identical to main afterwards); recorded in shakedown.md.
- s7 records commit `217178f` landed through a three-lens adversarial merge-gate (MERGE, zero must-fix; five findings applied pre-commit).
- Merged `gh-copilot` to main (`0627086`) and pushed; `git check-ignore gh-copilot.json` passes on main.
- Post-merge estate gate initially FAILED on `wiring/test-mcp-config.sh`; diagnosed pre-existing machine-environmental (no live mcp.json; worktree runs SKIP the check); recorded in `tests/KNOWN-RED.local.md`; re-run PASS (4 expected red, 3 machine-local).
- Acceptance criteria 1 to 8 recorded; use-it-or-lose-it clock started (deadline 2026-08-17); ideas #mocz66 and #qypmxb logged; the s7 SHIPPED writeback landed on the branch (`92183fa`) and was folded to main (`c50547c`), pushed.

### Current state
- `~/.claude` main == origin/main at `c50547c`; spine `docs/programmes/gh-copilot.md` reads `status: complete`, `lived_in: 0/2`.
- `skills/gh-copilot/` live on main; `metadata.last_shakedown` UNSET (waits on probes 1 + 11).
- Branch `gh-copilot` and its worktree (`.claude/worktrees/programme/gh-copilot`) still exist: branch kept by policy, worktree removable at leisure.
- This machine has the enabled `gh-copilot.json` (check-ignored). The Huble Mac keeps no config; its next pull should show `/gh-copilot preflight` refusing `machine_disabled`.

### Where we left off
Programme closed cleanly. The only open work is the deferred fresh-session shakedown pair.

### Next steps
1. Probe 1 (acceptance criterion 1's attended half): confirm the skill is not model-visible, a natural-language "hand this to copilot" does not invoke it, and a typed `/gh-copilot preflight` returns a valid envelope. Oracles in `skills/gh-copilot/references/shakedown.md` probe 1.
2. Probe 11 (scoped allowed-tools pilot, zero credits): per shakedown.md probe 11; record either way; feed the outcome to backlog #wjy2mt.
3. On both PASS: set `metadata.last_shakedown` in `skills/gh-copilot/SKILL.md`, update the shakedown STATUS block, commit.
4. Optional cleanup: `git worktree remove` the programme worktree (needs `--force` for the untracked config symlink); keep the branch.
5. Alternative entry point: `/programme next --offer-shakedown` surfaces gh-copilot as shakedown-owed from live state.

### Key references
- `skills/gh-copilot/references/shakedown.md` (probes 1 and 11; the s7 acceptance record)
- `docs/programmes/gh-copilot.md` (spine, complete)
- `docs/plans-archive/gh-copilot-delegation.md` section 10
- `tests/KNOWN-RED.local.md` (the mcp-config overlay entry; clears with #qypmxb)

### Notes for next session
An organic `/gh-copilot` use (review mode is the proven one) before 2026-08-17 starts filling `lived_in: 0/2`; none by then and /hygiene-sweep surfaces the removal path.
