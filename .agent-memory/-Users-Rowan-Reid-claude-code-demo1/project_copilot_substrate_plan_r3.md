---
name: copilot-substrate-plan-r3
description: "Copilot-substrate plan r3: sequencing steps 1-4 built and committed, both read-scope probes returned, shakedown 4-10 re-run PASS; one fresh-session stamp check open; plan file is machine-local"
metadata: 
  node_type: memory
  type: project
  originSessionId: 304e94b3-0b05-4dcf-b79e-dc2fbe776bba
  modified: 2026-07-23T17:25:52.815Z
---

The Copilot-as-sub-agent-substrate plan lives at `~/.claude/plans/copilot-as-subagent-substrate.md` (gitignored, machine-local to this laptop), with an **Execution log appended at the foot of that file**: read it before treating any part of the design as pending. r3, 2026-07-23: twice-interrogated (max-effort Fable pass plus a gpt-5.6-sol consult through the gh-copilot wrapper; both converged on the fifth premise: the orchestrator's beliefs entered the pass as context, never as content under test).

Adopted: the frame-audit leg (one out-of-family consult before any fan-out, plan inlined in the task file, zero wrapper changes needed). Unproven until the three-arm seeded bake-off: the eleven-leg lens offload.

Build state after the 2026-07-23 build+execute session (commits `c23d0b2`, `2778c45`, `9e2afb2` in `~/.claude`): **sequencing steps 1-4 are all built and committed.** Step 1 cooldown config keys; step 2 the read-scope controls; step 3 the offload sub-agent clause with the ledger split to `offload-ledger.md`; step 4 the operator procedure and lens task-file template written into the plan file. Steps 5-8 (the seeded three-arm bake-off) are separate sessions by design and untouched. Net gate green; unit suite 132.

Both read-scope probes returned (`copilot-read-scope-probe.md`, dispatched by Rowan): `--add-dir` **does** grant reads under the deny-first consult profile with no `--allow-all-paths`, cwd confinement **holds** (an ungranted sibling was refused), and a scoped `read(<path>)` deny denies the read tool **wholesale** (ignores the path, refuses every read) rather than scoping or silently no-opping. So the `--add-dir` plumbing was built on that evidence and proven end-to-end through the wrapper at shakedown probe 5. The CLI has **no scoped `read(path)` kind** (`copilot help permissions`, 1.0.73); read scope is an allow-list (cwd plus `--add-dir`), and the wrapper refuses to construct a `read(...)` deny. Separate live finding: shell execution is gated by PATH, not by the tool allow-list, so review runs arbitrary shell, but a bare `--deny-tool write` still blocks every write route including shell redirection. See [[medbrief-tracked-secrets-egress]].

Shakedown probes 4-10 re-run PASS for the day's dispatches; `metadata.last_shakedown` stays at 2026-07-18 pending ONE fresh-session check (procedure in `shakedown.md`): that the scoped `allowed-tools` grant still pre-approves a consult now that it may carry `--add-dir`. An organic hardening run using the frame-audit leg is live in the `medbrief-work` session (Mass Matter Import).

Related: [[programme-gh-copilot-pointer]] (the wrapper build this rides on).
