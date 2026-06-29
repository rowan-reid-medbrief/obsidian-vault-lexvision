---
tags: [demo-walkthrough, mri133, cli-frame, skill-development, containment, egress-gate, testing, medbrief]
repos:
  - "~/.claude: a3a77cc"
  - "annotations: 6c74d64 (no remote)"
parent: 2026-06-28-demo-walkthrough-cli-frame-c1.md
model_check: "fired-downgrade (model)"
---

# demo-walkthrough cli frame - C2 (live capture) + C3 (wiring)

Built C2 and C3 of the demo-walkthrough skill's `cli` frame, completing it end to end (C1 renderer + C2 capture + C3 wiring); C4 (the typing animation) stays deferred per the Path C decision.

**C2 - live capture.** Extracted `scripts/containment.py` (`snapshot_real_dir`, `real_dir_unchanged`, `git_porcelain`, a factored `terminate_process_group`) from `screenshot_app.py` so both orchestrators share one mutation proof (anti-drift). Built `scripts/capture_cli.py` + `validate_cli_config`: one throwaway sandbox outside the project (work/ + redirected HOME/TMPDIR/XDG_CACHE_HOME), an allowlisted child env (a parent-env secret can no longer reach or leak through a captured command), bounded no-OOM capture, killpg timeouts, strict-UTF-8-decode-then-drop, ANSI-normalise -> egress-scan -> freeze, per-command mutation proofs that abort exit 3 with no transcript, output_dir confinement, a git-SHA stamp, fail-loud partials. Hardened `gather_surfaces._detect_has_cli` to require the config to validate (malformed = counted soft exclusion; a run against it fails closed exit 2) and added a skill-config skip so the demo configs never leak in as surfaces. Fixtures + tests: `testdata/fixture-cli/tool.py` (with a declared write-into-snapshot-dir positive control, since the env allowlist defeats an env-gated one), `test-containment.sh`, and a 45-check `test-capture-cli.sh`. Shipped + validated the worked mri133 config (`poc/.demo-cli.json` - the --out/--json overrides are load-bearing: the defaults write into a snapshot dir) + `poc/.demo-egress.json` (explicit coverage for the PII-shaped project): live capture exits 0, containment holds under an independent re-check, the cli+tree frames render non-blank.

**C3 - wiring + docs + e2e.** A SKILL.md "Live CLI capture" section with the full contract moved to `references/live-cli-capture.md` (kept under the 500-line conformance cap; validates clean), and `test-cli-e2e.sh` driving capture -> render cli+tree -> grounded narration + audio -> a 2-beat MP4 (ffprobe Tier-A) -> an independent containment re-check; green under bash and zsh, plus an opt-in real-mri133 path.

**Commits:** ~/.claude `7196010` (C2) + `a3a77cc` (C3), pushed at wrap-up; annotations `6c74d64` (poc configs, local - no remote). **Follow-ups (noted, not done):** a `references/shakedown.md` with cli probes (the skill carries a last_shakedown date but no checklist), and moving the s4 app-capture detail into `references/` for body-cap headroom.
