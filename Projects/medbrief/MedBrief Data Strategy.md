---
title: "MedBrief Data Strategy"
domain: medbrief
created: 2026-06-19
tags: [data-strategy, medbrief]
status: discovery
project_repo: "~/claude_code/data_strategy"
project_key: "data_strategy"
---

# MedBrief Data Strategy

Company-wide initiative to understand, define, and implement a coherent data strategy for MedBrief. Covers the full business across three cycles: customer, product, and people.

## Status

**Discovery.** Kick-off meeting held 19 June 2026 ([[Rowan Reid]], [[Deon Kuhn]], [[Laura Gongas]]). No timeline yet. Third-party partner options being researched; meeting with [[Dot Collective]] on 26 June 2026.

## Why

MedBrief's data is currently siloed across systems, in inconsistent formats, with fragmented workflows. The goal is to move to a defined strategy and implemented architecture that covers the whole business — how data flows through the customer cycle, the product cycle, and the people cycle.

## Scope

- Identify all data sources across MedBrief's systems
- Define current state and target state
- Agree approach: internal, third-party, or a combination
- Implement (likely with a specialist partner)

## Partner candidates

- **Kumulus** — already engaged on the LexVision clinical pipeline; potential to expand scope
- **Microsoft / Azure** — platform already in use; pursue CSA engagement
- **Dot Collective** — data engineering consultancy; exploratory meeting 26 June 2026

## Relationship to clinical pipeline

This is a separate track from the LexVision / Kumulus clinical data pipeline POC. That work (entity extraction, pseudonymisation, Databricks architecture) is a discrete project; this initiative covers the broader business.

## Detailed working project

Working detail for this initiative lives in the Claude Code project at `~/claude_code/data_strategy` (the `project_repo` field above). That project owns the working detail; this note holds the hub layer. Per-topic detail:

- `docs/OVERVIEW.md` — start here: what it is, status, document map.
- `docs/SOURCES.md` — provenance and up-link map back to this note.
- `docs/DESIGN-NOTES.md` — project-tactical design notes (not a vault decision mirror).
- `docs/IDEAS.md` — project backlog.
- **Frontier Week (Microsoft) sessions, 22 June 2026.** Three sessions processed as input to the data strategy and the Microsoft CSA partner evaluation: the data-foundation-first thesis, the Fabric / OneLake / Fabric IQ / Foundry blueprint, and the governance model. Records: `notes/frontier-week-*-meeting.md`; source map: `docs/SOURCES.md`.
