---
type: handoff
date: 2026-06-09
project: lexvision-poc
domain: medbrief
tags: [kumulus, logicalis, medbrief, lexvision-poc, patent, dossier, meeting-graph]
repos:
  - lexvision-poc
  - ~/.claude
  - ObsidianVault
---

# 2026-06-09 — Kumulus dossier filed into lexvision-poc

Filed all Kumulus/Logicalis source material into the lexvision-poc project (April ideation deck, case-studies PDF, both meeting recordings and transcripts; recordings, transcripts and the deck gitignored, the public case-studies PDF tracked) and authored a six-part Kumulus dossier under `docs/kumulus/` (overview, company profile, proposal architecture, 28 May and 1 June meeting notes, and a patent-substantiation map). Added ADR-007 (Proposed) plus a medical-legal vertical track in `poc-scope.md`, Kumulus engagement and infrastructure terms in the glossary, and corrected the vendor name (Kumulus, not the ASR "Cumulus"), the meeting dates, and the inverted Expert Match codebase fact. Logged the /meeting-graph question-premise-as-fact bug to the central backlog. The continuation prompt below carries the Kumulus engagement work.

## Continuation Prompt

## Continuation: Kumulus engagement work (LexVision POC)

**Parent session:** 2026-06-09-kumulus-dossier-lexvision-poc.md

### Context
LexVision POC (patent US 2024/0185039 A1). Medbrief (a LexVision subsidiary) has Microsoft-incentivised funding and engaged Kumulus (Logicalis's Brazil-based Data and AI arm) to build all or part of a pipeline comparing clinical cases against NICE guidelines, a concrete instance of the patent. The Kumulus material is now fully filed into the project; this picks up at the engagement decisions.

### What was done last session
- Filed all Kumulus source material under `source_material/kumulus/` (deck, case-studies PDF, 2 recordings, 2 transcripts; recordings/transcripts/deck gitignored, public PDF tracked).
- Authored `docs/kumulus/` 00-05 (overview, company profile, proposal architecture, 28 May note, 1 June retro, patent-substantiation map).
- Added ADR-007 (Proposed) and a medical-legal vertical track in `poc-scope.md`; added Kumulus glossary terms; fixed pre-existing em dashes; logged the /meeting-graph question-premise bug centrally.

### Current state
- Committed: lexvision-poc `2038660`; ~/.claude `43c567d`; vault `d8d32ba` (pushed). Branch `main`.
- ADR-007 is Proposed, not ratified. Awaiting Kumulus's revised zero-cost proposal (comparison layer removed).

### Where we left off
Dossier complete and committed. Engagement decisions are open, documented in `docs/kumulus/05-patent-substantiation-map.md` under "Open questions for the engagement".

### Next steps
1. Build split: which pipeline components Kumulus builds vs Medbrief owns (Expert Match shares the Medbrief codebase, so ingestion may be Medbrief-owned).
2. Three stack divergences, decide adopt/diverge/compare for each, recording any divergence as a new ADR: graph store (ADR-002 Neo4j vs Cosmos Gremlin), pseudonymisation (ADR-005 Presidio vs Azure AI Foundry NLP), NLP backend (ADR-006 provider-agnostic/local vs cloud Foundry).
3. Agree acceptance benchmarks per ADR-004 (OCR fidelity, entity and identity resolution accuracy, pseudonymisation recall, comparison groundedness).
4. Ratify or revise ADR-007.
5. Review Kumulus's revised zero-cost proposal when it arrives.

### Key references
- `docs/kumulus/` (esp. `05-patent-substantiation-map.md`, `02-proposal-architecture.md`)
- `docs/decisions.md` (ADR-002/004/005/006/007); `docs/poc-scope.md` (medical-legal track)
- Graphs: `~/meeting-graph-output/{kumulus-medbrief,data-engineering-discussion}-2026-06-07/`
- Parked: /meeting-graph question-premise bug (in `~/.claude/docs/IDEAS.md`)
- People: Brendan Hughes (CEO/inventor), Deon Kuhn (CTO Medbrief), Laura Gongas (AI lead); Kumulus: Joao Marcura (pre-sales)

### Notes for next session
No learnings were queued this session.
