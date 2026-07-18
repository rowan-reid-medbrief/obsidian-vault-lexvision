---
tags: [gh-copilot, programme, worktree, implement-mode, harden-plan, merge-gate, security, red-first]
repos:
  - ~/.claude @ main (idea log #rf5ar4); branch gh-copilot @ 2433812 (s4 implement mode)
  - ObsidianVault (session log + memory mirror)
model_check: not-needed
---

# gh-copilot s4: implement mode (worktree isolation, lock, confirm gate)

Shipped s4 of the gh-copilot programme (M2): the isolated-worktree implement mode, built red-first (85 tests) then to green through the full conduct relay - `/harden-plan` (a 13-lens opus fan-out, 63 findings adjudicated), an independent red-author then green-builder, and a three-lens adversarial merge-gate that caught two plan-mandated defences missing behind the green suite (a cleanup pointer-tamper diff leak under `--force`, and an empty `effective_allowances` on the dry-run approval surface), both fixed and re-verified (the leak test was proven to bite against the unpinned code). Rowan deferred the `--allow-cmd` shell-allowance subsystem out of v1 (#rf5ar4). Lock lives in the dispatcher; the worktree module is pure git-over-git_scope with no subprocess. Committed on the branch (2433812); estate gate PASS; handing off before s5. All fan-outs ran on the opus fallback because the Fable burst is out of subagent credits on this machine.
