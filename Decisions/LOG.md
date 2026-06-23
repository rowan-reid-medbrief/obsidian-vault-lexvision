---
title: Decision Log
type: index
created: "2026-06-23"
modified: "2026-06-23"
tags: [decisions, index]
---

# Decision Log

The master log of strategic decisions across the vault's domains. Each row is one
decision; rich rationale lives in a linked full note at `Decisions/{date}-{slug}.md`.
Tactical and tooling micro-choices do not belong here.

| Date | Decision | Domain | Status | References | Note |
|---|---|---|---|---|---|
| 2026-06-19 | Scope the MRI-133 relocation POC to page-less documents, build it standalone in Python outside the monolith, prove forward redaction-survival (not today's re-export orphaning), and adopt a stamp-first identity model with content-matching as the fallback | medbrief | active | [[2026-06-19-mri133-scope-and-stamp-first]], [[Annotations]] | Two-arm POC (stamped + content); open fork for Deon: stamp at extraction vs sort-prep (rec: extraction) |
