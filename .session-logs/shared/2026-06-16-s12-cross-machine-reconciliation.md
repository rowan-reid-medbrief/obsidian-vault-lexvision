---
date: 2026-06-16
project: /Users/Rowan.Reid/claude_code/demo1
domain: personal
session: s12 cross-machine reconciliation (atlassian dual-scope + Lexvision) - central-config-backlog programme now feature-complete (13/13)
type: programme-session
tags: [config, programme, central-config-backlog, mcp, atlassian, git-hooks, cross-machine, hardening, s12]
repos:
  - path: /Users/Rowan.Reid/.claude
    commit: branch programme/central-config-backlog - c232fe5 (build, MAINTENANCE.md) + 02f174f (bookkeeping); pushed to origin/branch, NOT merged to main
parent: 2026-06-16-s13-mcp-parity-hotfix
---

## Session Summary

Ran **s12**, the final spec of the `central-config-backlog` programme, on the Medbrief machine (`mb-cpt-lt-0021` - the machine gate confirmed this is the only machine where s12 can run). The session opened with a routine push/pull of the central `~/.claude` config (main was 81 commits behind; clean fast-forward, the branch fetched), then moved to s12.

s12 had two halves: the atlassian dual-scope MCP removal (`#mwr7bq` cross-machine half) and the owed one-time Lexvision git-state reconciliation. Worked on the integration branch `programme/central-config-backlog` via the persistent worktree `~/.claude-worktrees/programme-s1` (freeze-main; never committed to main).

**Verify-stale-handoff.** Like s13, the live repo undercut the handoff's worst-case framing. Read-only investigation found **3 of the 4 Lexvision preconditions already satisfied**: `rebase.backend` unset (default merge backend, so the union driver fires), the settings.json clean filter already the canonical `-S` del form, jq 1.7.1-apple, and settings.json git-clean. Only the pre-commit hook was genuinely drifted.

**Hardening (`/harden-plan`: 4 merged-lens critics + a pre-mortem).** The pre-mortem made several strong claims that contradicted the investigation, so each was verified against source. Two were its own errors (it asserted the branch equals main, and that the hook canonical `9f58d47` was "fictional"; in fact the branch is 25 ahead / 38 behind main, components.sh differs, and `9f58d47` is a hook-body sha256, not a git object, so `git cat-file` on it is meaningless). But its core concern was real and got verified, not assumed: the live hook was **gitleaks-only (10 lines)**, and refreshing to the main canonical `5cb6c645` (49 lines) ADDS a skills-ref check-all gate (scanning main's tree by absolute path) plus a settings volatile-key guard. That refresh is safe only because main `run-skills-ref check-all` returns rc 0 (all 39 clean) and s12's commits stage no settings.json. Folded a must-fix (Commit-1 explicit-path add + one-file assertion) and pre-flight gates (pwd==demo1 abort for the cwd-coupled mcp remove; check-all rc 0 before the refresh; sha-match-or-STOP). Rowan chose the direct hook write over `install.sh`, and gave the GO.

**Executed (all reversible; all pre-flight gates green):**
- **A.** `claude mcp remove atlassian -s local` removed the stale project-local `/v1/mcp/authv2` (needs-auth). atlassian now resolves to the single working user-scope `/v1/mcp` (Connected, the same endpoint the claude.ai Atlassian Rovo built-in uses); the "Conflicting scopes" warning is gone. Mutates `~/.claude.json` (machine-local, not the repo).
- **B.** Pre-commit hook refreshed via the direct `precommit_hook_body >` write from the stale gitleaks-only `949ec2ae` to canonical `5cb6c645`, sha-verified. The refreshed hook then live-gated both commits (gitleaks clean + skills 39/39) - a real smoke test of the refresh.
- **C.** `settings.json add --renormalize` was a no-op (porcelain empty), confirming the clean filter.
- **D.** MAINTENANCE.md gained a "Resolving conflicting scopes" subsection plus a per-machine reconciliation-status note (the only repo artifact of the first half).

Two-commit shape on the branch: `c232fe5` (build, MAINTENANCE.md) + `02f174f` (bookkeeping: the spine `**s12 SHIPPED` ledger entry + `#mwr7bq` flipped to `[done c232fe5]`, both halves now closed). Branch pushed to origin so the work reaches the final-merge machine. No claim marker.

**Outcome.** The programme is **feature-complete**: the spine validates OK 13, and `next` returns null with all 13 specs (s1-s13) shipped.

**Corrected, carried (not s12 scope):** `#wkc500` (wrap-up SKILL.md "over the 500-line body cap") - the branch file now validates OK (rc 0) under main's skills-ref despite 517 raw lines and the `[high]` tag, so the raw-line "merge-blocker" framing looks stale; flagged for a scoped check before the programme-end merge, not resolved here.

## Next

The programme-END land is **Rowan-gated and IRREVERSIBLE**, NOT done here:
- merge `programme/central-config-backlog` -> main (ONCE)
- the first live config.push `#isyfts`
- close `#uq6rix`
- the `#wkc500` pre-merge check (confirm it really is conformant before relying on it)

## Notes

- **Vault placement.** This machine's vault has no `.session-logs/shared/` (config logs here have historically gone to `personal/`); I created `shared/` to follow the programme convention and the s-series `parent:` chain. The `parent: 2026-06-16-s13-mcp-parity-hotfix` log lives on the other machine's vault (hd-m-reidr), so the parent reference is cross-machine and reads as dangling on this machine until the two vaults are considered together. This is the first programme log written on this machine's vault.
- **Sub-plan:** `~/.claude-worktrees/programme-s1/plans/s12-cross-machine-reconciliation.md` (gitignored/local).
