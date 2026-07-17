---
tags: [gh-copilot, programme, copilot-cli, delegation, wrapper, red-first, teardown, security]
repos:
  - ~/.claude @ e121ba3 (main); branch gh-copilot @ e6f5d6d
  - ObsidianVault (session log + memory mirror)
model_check: not-needed
---

# gh-copilot delegation build (programme M1 + most of M2)

Continued the gh-copilot delegation handoff on the Lexvision laptop and turned the hardened plan into a tracked programme spine, then shipped M1 and most of M2. M1: the 0b raw trial against the real Copilot CLI (1.0.71) cleared all 10 unverified pins and the demand gate was answered yes. M2: the `disable-model-invocation` spec carve-out (s2), then the red-first suite, `mock-copilot`, and the policy+dispatcher wrapper to green for preflight/consult/review (s3, 49 tests). An advisor review caught a real credit-burn teardown hole in the wrapper (a detached paid child orphaned on timeout/cancel), fixed in the same spec with process-group reaping and signal handlers.

## What shipped
- **Programme promote**: spine at `~/.claude/docs/programmes/gh-copilot.md` (7 specs, M1-M3, branch-mode on `gh-copilot`), validated; discovery-pointer memories under the demo1 and estate slugs.
- **s1** raw trial: pins recorded into plan section 11; org_confirmed 2026-07-17; profile correction (drop `--silent`); demand gate = yes.
- **s2** `disable-model-invocation` carve-out in SKILLS-SPEC + `run-skills-ref` (commit c348d25).
- **s3** wrapper core: `gh_copilot_profiles.py` (pure policy), `gh_copilot_delegate.py` (dispatcher, single `Popen` spawn site, group-kill teardown, signal handlers), `mock-copilot`, and a 49-test red-first suite (commits bfa78d1, e6f5d6d). `--excluded-tools github` and the deny-first defaults witnessed against the real CLI.

## Where we left off
M2 spec **s4** (worktree/implement module) is next: `needs_subplan`, security-critical, and it carries two carry-forwards from the advisor review, both recorded in plan section 11: release the implement lock in `finally` and `killpg` on lock teardown; and at s6 add the real-CLI witness (dispatch a real consult, `kill -TERM` the wrapper mid-run, confirm no surviving `copilot` and no continued billing). Resume with `/programme next` in a fresh window; it will emit the s4 launch prompt from live state. Branch `gh-copilot` is machine-local (unpushed); it merges to main at s7 after the live shakedown.

## Decisions (Rowan)
- Promote to a programme spine rather than run from handoff prompts; branch-mode build (primary checkout stays on main).
- v1 builds all three modes; whole build attended on the Lexvision laptop; merge gated on the live shakedown.
- Demand gate answered yes.
- The teardown reflected learning is applied in code and recorded in plan section 11; not logged as a separate backlog idea (Rowan's call).

## Note
Continued a handoff whose parent session log lives on the Huble Mac's vault (`.session-logs/lexvision/2026-07-17-gh-copilot-delegation-plan.md`), so `parent:` is omitted here (cross-machine; not resolvable on this vault).
