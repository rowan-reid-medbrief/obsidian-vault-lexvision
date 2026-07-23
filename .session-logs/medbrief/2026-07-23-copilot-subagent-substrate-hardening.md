---
session_id: [6f63d4c7-4e81-4b0a-88f7-1d1e0e1338d1]
title: "Copilot as a sub-agent substrate: plan + 12-agent hardening"
type: handoff
domain: medbrief
created: "2026-07-23"
parent: null
tags: [session-log, medbrief, gh-copilot, harden-plan]
---

# Copilot as a sub-agent substrate: plan + 12-agent hardening

## Session summary

Designed and hardened a plan to route sub-agent work onto the GitHub Copilot CLI whenever Claude would otherwise fan out, with `/harden-plan` as the first caller. A 12-agent Claude fan-out produced ~60 findings, including three that killed parts of the draft: the target MedBrief repo has private keys tracked in git and reachable by Copilot's read tool, `harden-plan` has no `Bash` in `allowed-tools` so it cannot dispatch at all, and a failed Copilot leg was indistinguishable from a leg that found nothing. Rowan then caught four further flaws the fan-out missed, all of them premises seeded into the grounding digest, which is the session's most durable finding (#k3mq7w).

## Continuation Prompt

## Continuation: Copilot as a sub-agent substrate - interrogate the frame

**Parent session:** 2026-07-23-copilot-subagent-substrate-hardening.md

### Context
Rowan asked whether the GitHub Copilot CLI could stand in whenever Claude would otherwise spin off
sub-agents: Claude emits paste-ready prompts, Rowan runs them, Claude waits for the results. The
driver is that this laptop runs a small MedBrief Claude subscription while Copilot draws on pooled
MedBrief AI credits that are not to be rationed. Copilot also exposes frontier models (gpt-5.6-sol,
gpt-5.5, claude-opus-4.8), so this need not be workhorse-only.

### What was done this session
- Drafted the plan, then hardened it with a 12-agent fan-out: ten scrutiny dimensions, a pre-mortem,
  an architectural review, plus the external-source and oracle conditional phases. ~60 findings.
- Three findings killed parts of the draft: the target MedBrief repo has `docker/jwt/private.pem`
  and `docker/keys/xero-dev-privatekey.pem` tracked in git and reachable by Copilot's read tool;
  `harden-plan/SKILL.md:12` has no `Bash` in `allowed-tools` so the skill cannot dispatch at all;
  and a failed Copilot leg was indistinguishable from a leg that ran and found nothing.
- Measured the baseline: 871,887 sub-agent tokens across 11 reporting critics, range 61,114 to
  98,902. Burn scales with grounding surface (how much source a lens opens), not plan length.
- Rowan then found four more flaws the fan-out missed. Plan rewritten to r2.
- Config: split the meter/egress conflation in the offload-policy gate, recorded the no-rationing
  posture, logged learning #k3mq7w.

### Current state
- Plan: `~/.claude/plans/copilot-as-subagent-substrate.md` at r2. NOTE: `plans/` is gitignored
  (`.gitignore:30`), so it is machine-local and untracked.
- Vault: committed and pushed (`683fd045`).
- `~/.claude`: committed locally at `715a3ea` but **NOT pushed**. The eval net gate blocked it on
  three suites red but unlisted, none caused by this session's commit: `test-taxonomy-sync`
  (`delegation-scout` on disk, missing from the taxonomy) and `test-voice-reconcile` (four
  `profile/*.md` orphans: `delegation-vision`, `improvement-front-doors`,
  `interview-to-convergence`, `model-tier-fable-permanent`), plus `test-registry-index`. Drift from
  commits `ceb783f`, `e1cc005`, `10413e1`. Do NOT use `push_gate_bypass`; fix the drift.
- Nothing is time-pressured: the seeded-synthetic-plan test replaced the archaeology that had a
  2026-08-07 transcript-pruning deadline.

### Where we left off
Plan hardened and saved. Nothing implemented. Rowan wants a fresh Fable session at max effort to
interrogate the plan before any build starts.

### Next steps
1. Run `/model fable` and `/effort max`, then the interrogation brief below.
2. Clear the three red suites (a `/hygiene-sweep` job) so `~/.claude` can push.
3. Then, if the frame holds: cooldown config keys; `--add-dir` on the consult profile; deny-paths
   plus preflight secret scan; the seeded-synthetic-plan bake-off.

### Key references
- Plan: `~/.claude/plans/copilot-as-subagent-substrate.md`
- Skill + wrapper: `~/.claude/skills/gh-copilot/` (SKILL.md, references/modes.md,
  references/offload-policy.md, scripts/)
- First caller: `~/.claude/skills/harden-plan/SKILL.md`
- Learning: `~/.claude/learnings/k3mq7w.md`

### The interrogation brief

Read the plan, then `~/.claude/skills/gh-copilot/` (SKILL.md, references/, scripts/) and
`~/.claude/skills/harden-plan/SKILL.md`.

WHY YOU ARE BEING ASKED. After twelve agents reported, Rowan found four more flaws in minutes. Every
one was a premise Claude had seeded into the grounding digest as established fact, which every critic
then inherited:

1. That Copilot cannot read files outside the target repo, so plan text must be inlined, which Claude
   argued inverted the economics. Wrong: `--add-dir` exists and the wrapper's own implement profile
   already uses it. One agent had even found `--add-dir` in the CLI docs. Nobody connected them.
2. That "MedBrief-estate only" was a security boundary, so Claude built repo allow-list enforcement.
   It is a routing rule about which subscription pays.
3. That Copilot credits are scarce and want guarding. They are not to be rationed.
4. That this is a `/harden-plan` feature. It is a general capability.

Blind critics are blind to each other, not to the frame. The plan is now r2, but it is still Claude's
frame.

YOUR JOB. Attack the FRAME, not the contents. Line-by-line checking has been done and is low value.
Specifically:
- What premise is still load-bearing and still unexamined? The plan's "What the fan-out missed"
  section lists four that were caught. Find the fifth.
- Is the binding constraint dissolvable? The plan assumes Claude tokens are scarce and Copilot
  credits are not, that a human pastes each command, and that the unit of work is a per-lens
  critique. Are any of those actually fixed?
- Is there a fundamentally different implementation shape: a different decomposition, trigger point,
  or division of labour between the two systems? Or not this at all?
- Is `/harden-plan` the right first caller, or merely the most seductive because it is the most
  expensive?

SETTLED, DO NOT RE-LITIGATE (Rowan's decisions, made with the trade-offs in view): typed
`/gh-copilot` stays the only dispatch path and propose-and-yes is out of scope; `implement` mode is
out of scope; do not ration credits; Copilot may read `~/.claude` when serving MedBrief work; high
dispatch friction is accepted.

WHAT GOOD OUTPUT LOOKS LIKE. Not a findings list. A short, direct argument: here is the premise still
holding this plan in the wrong shape, here is what it looks like if that premise goes, here is what I
would build instead, here is what would tell us quickly which is right. If the frame holds, say so
plainly and name what you tried to break and could not.

Verify claims against source before asserting them. The previous pass's worst failures were
confident, unchecked assertions about the Copilot CLI's behaviour.
