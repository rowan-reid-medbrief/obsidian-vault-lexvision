---
name: reference_meeting_graph_outputs
description: Locations and stats for meeting-graph runs (7 total under ~/meeting-graph-output/). Details the two Phase-B runs (DE Discussion + Kumulus); DE re-built 2026-06-12.
metadata: 
  node_type: memory
  type: reference
  originSessionId: 95fbdc5d-e42a-43bb-9c2b-56f4db01df7a
---

Both DE + Kumulus used Phase B recall recovery (gapfill, grounded_admit, chunk_budget, anchors, validate_repair, gleaning_passes=2).

**Full inventory (7 runs on this machine):** DE + Kumulus (Phase B on, detailed below); mb-product-walkthrough-2026-06-03 + medbrief-walkthrough-part2-2026-06-08 (presenter-dominated solo demos, Phase B off by design, already rebuilt 2026-06-12 with current code); beyond-vibe-coding-2026-06-05 + vibe-coding-vs-sdd-2026-06-05 (pre-Phase-B, reference content, not re-run); kumulus-regroup-2026-06-12 (FULLY BUILT: 170 nodes, 287KB graphml; the earlier "UNFINISHED" note was wrong). As of 2026-06-13 all 5 of {kumulus-medbrief, data-engineering-discussion, kumulus-regroup, mb-product-walkthrough, medbrief-walkthrough-part2} are promoted into the vault `.meeting-graphs/` store (the R6/H+GATE-2 calibration). Vault NOTES from that run were reverted at Rowan's request; no `graph_ref` pointers in visible notes. See [[reference_r6h_gate2_calibration]]. One manual lift: Kumulus summary.md referenced by hand in `lexvision-poc/docs/kumulus/research/c1-kumulus-spec.md`.

**Data Engineering Discussion (2026-06-01, ~37 min)**
- Output: `~/meeting-graph-output/data-engineering-discussion-2026-06-07/`
- 115 nodes, 51 substantive, 205 edges
- 15 gap-fill nodes across 2 gleaning passes (containment only, NLI not triggered)
- Participants (3 only): Rowan Reid, Deon Kuhn, Laura Gongas. The other named Person nodes (Brendan, Mediha, Vanessa, Chantel Pilla, John (Cumulus), Fatima, Dave) are people MENTIONED in discussion, not attendees. `is_participant` is unset on all nodes; the transcript labels only the 3. (Earlier note listing 7 participants was wrong.)
- Topics: Expert Match storage endpoint, Cumulus ground truth, NICE API, data architecture proposal, priority order
- Re-run 2026-06-12 with current code (f9403c4 build fix, same Phase B flags) confirmed the graph is byte-equivalent to the original: 115 nodes / 205 edges / 51 substantive, identical edge set, `stale_lone_speaker=False`. The build fix had no net effect on this meeting (the 5 extra edges it surfaced at build were stripped by the shared repair stage). The duplicate 06-12 output dir was removed as confirmed-equivalent; the 06-07 dir is the canonical graph.

**Kumulus & Medbrief Vendor Proposal (2026-05-28, ~62 min)**
- Output: `~/meeting-graph-output/kumulus-medbrief-2026-06-07/`
- 152 nodes, 53 substantive, 334 edges
- 7 gap-fill nodes (4 rejected by NLI gate)
- Speaker mapping: SPEAKER_03=Joao Margura (Kumulus), SPEAKER_06=Laura Gongas, SPEAKER_00=Brendan Hughes, SPEAKER_01=Steve Ashford, SPEAKER_02=Vanessa Patrocinio
- Key commercial: £35k full cost, £22k Microsoft discount, £13k net; scope revised (comparison layer removed); revised proposal in 5 business days

**Next step:** Place the seeded meetings' real content into their projects (Kumulus/DE -> lexvision-poc, walkthroughs -> medbrief-onboarding); the vault `.meeting-graphs/` store and `~/meeting-graph-output/` are the sources, and `calibration-misplaced-cleanup.md` lists the mis-placed bullets worth re-placing.
