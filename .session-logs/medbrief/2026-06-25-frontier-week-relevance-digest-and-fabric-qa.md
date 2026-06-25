---
tags: [frontier-week, data-strategy, work-digest, fabric, kumulus, pseudonymisation, audio-digest]
repos: [data_strategy, ObsidianVault, ~/.claude]
parent: 2026-06-23-frontier-week-graphs-and-routing.md
model_check: not-needed
---

# Frontier Week project-relevance digest + Fabric / pseudonymisation Q&A

Produced the Frontier Week project-relevance digest, the action queued from the prior session: a ~47-minute spoken audio digest (macOS Daniel en-GB voice) of the three Microsoft Cloud & AI Frontier Week talks (22 June), theme-woven across all three and led by the MedBrief data strategy, rendered via `/work-digest`'s render stage with the gather/lint pipeline bypassed (it digests talk content, not session logs). The 8,072-word narration script renders at 46.6 min; a first 4,965-word cut came in at 29 min (the Daniel voice runs ~173 wpm, not the template's ~150), so it was expanded to hit the ~45-min walk target. Transcript saved to `data_strategy/notes/frontier-week-digest-2026-06-22.md`; audio copied to iCloud Drive (`Frontier-Week-Digest/`, ~118 MB).

Then an advisory Q&A across three questions:

- **Are Microsoft proposing Fabric as the solution?** Yes, that is the pitch (OneLake as the foundation, Foundry for agents), but even Microsoft frame it as "unify onto OneLake, keep your existing stores connected" (two-way Databricks/Snowflake sharing). For us it is a leading-but-not-chosen candidate, with a natural edge because the estate is already Azure, to be tested against Dot Collective and Kumulus, not adopted by default.
- **Should we pseudonymise MedBrief data before OneLake?** Brendan's "pseudonymise before pushing upstream" pattern is right for the egress / third-party flow (e.g. to Kumulus and shared training sets), but wrong as a blanket ingest rule: pseudonymised data is still personal data under UK GDPR (does not remove the obligation), stripping identifiers on ingest breaks the workloads that need them, and a re-identification map just relocates the risk. The model proposed: land real data in a locked-down zone, expose a masked/pseudonymised view to broad workloads via OneLake's apply-security-once, and pseudonymise physically only at egress. This is a Deon + DPO call, driven by the data classification, and it sharpens the vendor evaluation and the data-retention item.
- **Do the talks re-open Fabric for the Kumulus PoC?** Yes, but per-module and for the longer-term architecture, not the current narrow PoV. The Kumulus build is already Azure end to end (Databricks modelling, Azure AI Foundry NLP/pseudonymisation, Cosmos DB Gremlin, Microsoft-incentive funded), so Fabric was never really off the table. The current revised PoV is deliberately tabular/non-graph with no benchmarks (ADR-008), so its headline features (ontologies, graph DB, both public preview) would be scope creep. Where it genuinely re-opens: ADR-002's graph store (now wholly MedBrief-side) gains Fabric's native graph DB as a third Azure-native candidate alongside Neo4j and Cosmos Gremlin, and MedBrief's newly-owned prep-zone / de-identification work is where OneLake security and the apply-once masking apply. Evaluate per-module under ADR-008's modular-architecture framing and ADR-004's benchmark bar; it does not change the live 10-June negotiation.

Logged one `/work-digest` improvement idea (central backlog): its word-count-to-duration model undershoots at the default voice rate.

## Next
- Raise the standard agent-to-data interface (MCP) against the MSR MCP server epic (MSR-5832) as a buy-vs-build question (strongest follow-up).
- Carry Fabric (apply-security-once, AI-on-PDF, works-with-Databricks) into the Dot Collective (26 June, Jack Ford) and Kumulus evaluation as a baseline to test against.
- Fold the ontology cross-check (do our condition types carry actions and rules?) and Fabric's native graph DB into ADR-002.
- Start data-source discovery across the customer / product / people cycles.
