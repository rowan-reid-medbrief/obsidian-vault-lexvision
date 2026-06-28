---
date: 2026-06-28
project: /Users/Rowan.Reid/claude_code/projects/annotations
domain: medbrief
session: Designed, hardened, and shipped C1 of a cli terminal-frame type for the demo-walkthrough skill
type: handoff
tags: [demo-walkthrough, cli-frame, mri133, harden-plan, skill-build, claude-config]
repos:
  - path: /Users/Rowan.Reid/.claude
model_check: not-needed
---

## Session Summary

Designed, hardened (a five-critic /harden-plan pass), and began building a `cli` terminal-frame type for the demo-walkthrough skill so it can demo command-line tools like MRI-133: the commands run, their real output, and the files they create. Shipped C1 - the static cli renderer (`render_frames.py` cmd_cli + a trim-only draw_cli_frame) and the frame type wired across all six lockstep sites including a new render-dispatch reader that closes a "green test, crashing render" seam, with every affected test green under bash and zsh. C2 (the live capture orchestrator) and C3 (runtime wiring + SKILL.md) remain; the hardened plan at ~/.claude/plans/we-recently-implemented-some-temporal-blanket.md is the spine.

## Continuation Prompt

## Continuation: demo-walkthrough cli frame - C2 (live capture) + C3 (wiring)

**Parent session:** 2026-06-28-demo-walkthrough-cli-frame-c1.md

### Context
Adding a `cli` frame type to the demo-walkthrough skill (~/.claude/skills/demo-walkthrough/) so it demos command-line tools the way `app` demos UI tools: commands typed and run, their real output, and the files they create. Motivating tool: the MRI-133 `mri133` CLI at /Users/Rowan.Reid/claude_code/projects/annotations/poc. The hardened plan (the spine) is at ~/.claude/plans/we-recently-implemented-some-temporal-blanket.md.

### What was done last session
- Planned the feature, then ran a five-critic /harden-plan pass. Rowan chose Path C: terminal frame + automated capture now, typing animation deferred; flags explained by narration.
- Shipped C1 (committed to ~/.claude as b4ec819): the static `cli` renderer (`render_frames.py` cmd_cli + trim-only draw_cli_frame), the frame type across all SIX lockstep sites, a new render-dispatch reader in test-frame-type-enum.sh, has_cli detection + eligibility, and tests (testdata/cli-transcript.good.json + 7 render cases + a render_mp4 type-agnostic proof). All affected suites green under bash and zsh.

### Current state
- C1 committed + pushed to ~/.claude (main). Tasks 1-3 of 8 done; #4-8 pending (re-create the TaskCreate list).
- The hardened plan is the authoritative spec for C2/C3/C4.

### Where we left off
C1 complete and tested. Next is C2, the heavy, security-sensitive stage (it executes commands).

### Next steps (priority order)
1. C2 - extract scripts/containment.py (snapshot_real_dir, real_dir_unchanged, git_porcelain, terminate_process_group); make screenshot_app.py import it; keep the s4 tests green.
2. C2 - build scripts/capture_cli.py + validate_cli_config per the plan: one sandbox outside the project, Popen+killpg timeouts, env ALLOWLIST + TMPDIR/HOME into the sandbox, strict-UTF-8-decode-then-drop, ANSI-normalise-before-scan-and-freeze, output-size cap, per-command containment proofs (project root), output_dir confinement, git-SHA stamp, fail-loud partials; harden _detect_has_cli to require validation.
3. C2 - fixtures/tests: testdata/fixture-cli/ (synthetic subcommands + a write-outside-sandbox positive control) + cli-fixture.json + test-capture-cli.sh (failure matrix); reworked mri133 .demo-cli.json (run --matchers all --seed 1234, then report - NOT gen-corpus->run, which is incoherent) + real-tool validation.
4. C3 - files-created tree frame, SKILL.md "live CLI capture" section (honest mutation-proof wording, env allowlist, card --body-file stays the default, no-live-capture fallback), route the demo through demo-walkthrough-eval as the acceptance gate; validate SKILL.md against docs/SKILLS-SPEC.md.
5. C4 (deferred): typing animation - generate_motion.py per-kind dispatch refactor with the render_text-from-transcript egress fix and a byte-identical static fallback.

### Key references
- Plan/spine: ~/.claude/plans/we-recently-implemented-some-temporal-blanket.md
- Skill: ~/.claude/skills/demo-walkthrough/ (screenshot_app.py is the clone source for capture_cli.py + containment.py; egress_gate.py egress_drop is the shared gate)
- Motivating tool: /Users/Rowan.Reid/claude_code/projects/annotations/poc/src/mri133/cli.py (run regenerates its own corpus and can exit 2; report needs a prior run)

### Notes for next session
- ~/.claude may carry UNRELATED uncommitted work (scaffold-project, settings.json) from another context - stage only your files in C2 commits.
- Pre-existing: test-egress-gate fails on a missing Slinky PDF fixture path (machine-specific, unrelated).
- Model/effort: Opus 4.8 was right; keep opus/high for C2 (executes commands).
