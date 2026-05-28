# ObsidianVault Vault

This is the Obsidian vault for this machine and the single source of truth for its notes. This
`CLAUDE.md` overrides and extends the global `~/.claude/CLAUDE.md` with vault-specific conventions.
See `~/.claude/docs/ARCHITECTURE.md` for how the global, vault, and project layers fit together.

(Starter template written by `install.sh`. Fill in the `{{...}}` placeholders and strip or replace
any section you do not need.)

## Vault Domains

This vault routes work across the following domains. Routing skills (meeting-to-vault,
transcript-to-insight, decision-log) read this list, so keep it accurate and in step with the
`domains` array in `~/.claude/active-vault.json`.

- **medbrief**: medbrief work
- **lexvision**: lexvision work
- **personal**: personal work

Primary domain: medbrief.

## Folder structure (modified PARA)

- `Inbox/`: unsorted capture; triage into the structure below.
- `Projects/`: active, time-bound work. Per-domain subfolders (`Projects/{domain}/`), plus `Projects/Meetings/{domain}/`.
- `Areas/`: ongoing responsibilities with no end date.
- `Resources/`: reference material (`Technical/`, `Frameworks/`, `Transcripts/{domain}/`, `Summaries/{domain}/`, `Reference Indexes/`).
- `Decisions/`: the decision log (`LOG.md` plus per-decision notes), each with a `domain:` frontmatter field.
- `People/`: per-person notes, in per-domain subfolders.
- `Companies/`: per-company notes.
- `Archives/`: completed or dormant work.
- `Templates/`, `Attachments/`: note templates and binary attachments.

Two hidden dot-folders (Obsidian ignores them; the vault git remote backs them up):

- `.session-logs/{domain}/`: agent session logs, with a `domain:` frontmatter field.
- `.agent-memory/{slug}/`: backup copies of per-project agent memory, mirrored by `/wrap-up`.

## Frontmatter conventions

Every note opens with YAML frontmatter. At minimum:

```yaml
---
title: <human title>
domain: <one of the vault domains above>
created: <YYYY-MM-DD>
tags: []
---
```

## Formatting and placement rules

- UK English, no em dashes (inherited from the global `profile/` layer; do not restate the rules, just follow them).
- Place new notes by PARA: active work in `Projects/`, reference in `Resources/`, people in `People/`.
- Before adding a new tracking structure, check whether an existing one already fits.
- {{Add vault-specific conventions here.}}

## Domain-specific sections

{{Add any domain-specific glossaries, workflows, leadership teams, or pipelines here, one section per
domain as needed. Strip this heading if you have none yet.}}
