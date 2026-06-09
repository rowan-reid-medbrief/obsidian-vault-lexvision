---
name: kumulus-engagement
description: "LexVision POC's live Kumulus/Logicalis vendor engagement to build the patent-substantiation pipeline for Medbrief"
metadata: 
  node_type: memory
  type: project
  originSessionId: 94adaf74-d053-4f72-82fd-eb29ef5c3153
---

Medbrief (a LexVision subsidiary) has Microsoft-incentivised funding and engaged **Kumulus** (the Brazil-based Data and AI arm of **Logicalis**) to build all or part of a pipeline that compares clinical cases against NICE guidelines. That pipeline is a concrete instance of the LexVision patent (US 2024/0185039 A1), so the build is the POC's real-data substantiation of the patent claims.

Three touchpoints: ~22 Apr 2026 ideation deck (London hackathon), 28 May 2026 vendor proposal (~£35k gross to ~£13k net after Microsoft incentives; comparison layer later cut), 1 June 2026 internal data-engineering retro. Full dossier in `docs/kumulus/` (start with `05-patent-substantiation-map.md`); recorded in ADR-007 (Status: Proposed). The vendor name is **Kumulus**, not the ASR "Cumulus".

Open threads: the build split (Kumulus vs Medbrief; note Expert Match is a separate product but shares the Medbrief codebase), and three stack divergences to reconcile, Kumulus's Azure / Databricks / Cosmos Gremlin / Azure AI Foundry stack versus the POC's Neo4j ([[ADR-002]]), Presidio ([[ADR-005]]), and provider-agnostic/local NLP ([[ADR-006]]).
