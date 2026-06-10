---
name: kumulus-engagement
description: "LexVision POC's live Kumulus/Logicalis vendor engagement to build the patent-substantiation pipeline for Medbrief"
metadata: 
  node_type: memory
  type: project
  originSessionId: 94adaf74-d053-4f72-82fd-eb29ef5c3153
---

Medbrief (a LexVision subsidiary) has Microsoft-incentivised funding and engaged **Kumulus** (the Brazil-based Data and AI arm of **Logicalis**) to build all or part of a pipeline that compares clinical cases against NICE guidelines. That pipeline is a concrete instance of the LexVision patent (US 2024/0185039 A1), so the build is the POC's real-data substantiation of the patent claims.

Four touchpoints: ~22 Apr 2026 ideation deck (London hackathon, Fabric/CQRS); 28 May 2026 vendor proposal (Databricks, ~£35k gross to ~£13k net; João offered to cut the comparison layer for a zero-cost revision); 1 June 2026 internal data-engineering retro; 10 June 2026 the revised proposal arrived with the OPPOSITE cut: Kumulus keeps the comparison layer (NICE, Databricks, data contract validation, explainable outputs) and drops the entire upstream (OCR, entity extraction, pseudonymisation, Cosmos DB, GraphQL, app), which becomes MedBrief's prepared-data obligation. £22,085.10 services exactly offset by two Microsoft incentives, £0 conditional on incentive approval. Full dossier in `docs/kumulus/` (assessment of record: `10-revised-proposal-2026-06-10.md`; audit: `audit-2026-06-10.md`). The vendor name is **Kumulus**, not the ASR "Cumulus".

Position (ADR-008, Proposed): accept in principle and negotiate eight gating conditions (IP/takeover-ability, incentive conditionality in writing, NICE 2020 sourcing via the National Archive, co-authored data contract, ADR-004-grade acceptance criteria, engine transparency, Azure cap, MedBrief tenancy). Product-layer ownership of the comparison module stays with MedBrief/Mediha. Divergence states after the revision: ADR-002 (graph store) moot for the PoV; ADR-005 (Presidio) is now MedBrief's own prep-zone obligation; ADR-006 exposure reduced. See [[kumulus-architecture-first-framing]] for Rowan's framing (modular architecture is the primary artefact; module ownership is fluid).
