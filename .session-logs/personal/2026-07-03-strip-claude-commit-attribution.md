---
tags: [config, git, commit-attribution, entire, git-filter-repo, history-rewrite]
domain: personal
repos:
  - medbrief-onboarding@fa8cfad
  - ObsidianVault (session log)
model_check: not-needed
date: 2026-07-03
---

# Strip Claude commit attribution across repos

Turned off Claude commit attribution globally (`settings.json`: `includeCoAuthoredBy:false`, `attribution.commit:""`, `attribution.sessionUrl:false`), then purged historical `Co-Authored-By: Claude` and all `entire` trailers from 8 personal/private repos with `git-filter-repo`, verifying every commit tree SHA stayed byte-for-byte identical (only messages changed). Force-pushed the two cleaned remotes (ObsidianVault `main`; annotations all 3 branches, needing `--no-verify` to bypass entire pre-push hook).

**Purged (local-only):** medbrief-onboarding (13), expert-sheet-data-processing (17), data_strategy (5), apprise-viewer-rendering (7), data_pipelines wrapper (29), lexvision-poc (525). **Purged + pushed:** ObsidianVault (57), annotations (196). `.git` backups saved to session scratchpad (ephemeral).

**Deliberately left alone:** the shared team repos (Azure DevOps `data_pipelines` 118, Bitbucket siblings) to avoid disrupting colleagues history; and `~/.claude` - its remote had diverged (6 commits pushed from another machine today), so a force-push would have destroyed unsynced work. `.claude` remains purge-pending; reconcile with a normal `git pull --rebase` first if ever revisited. entire ongoing `Entire-Agent: Claude Code` tag accepted as-is per Rowan.

Captured the reusable entire behaviour in `profile/entire-git-behaviour.md`.