---
name: reference_meeting_graph_outputs
description: Locations and stats for meeting-graph runs (7 total under ~/meeting-graph-output/). Details the two Phase-B runs (DE Discussion + Kumulus); DE re-built 2026-06-12.
metadata: 
  node_type: memory
  type: reference
  originSessionId: 95fbdc5d-e42a-43bb-9c2b-56f4db01df7a
---

Both DE + Kumulus used Phase B recall recovery (gapfill, grounded_admit, chunk_budget, anchors, validate_repair, gleaning_passes=2).

**Full inventory (7 runs on this machine):** DE + Kumulus (Phase B on, detailed below); mb-product-walkthrough-2026-06-03 + medbrief-walkthrough-part2-2026-06-08 (presenter-dominated solo demos, Phase B off by design, already rebuilt 2026-06-12 with current code); beyond-vibe-coding-2026-06-05 + vibe-coding-vs-sdd-2026-06-05 (pre-Phase-B, reference content, not re-run); kumulus-regroup-2026-06-12 (FULLY BUILT: 170 nodes, 287KB graphml; the earlier "UNFINISHED" note was wrong). As of 2026-06-13 all 5 of {kumulus-medbrief, data-engineering-discussion, kumulus-regroup, mb-product-walkthrough, medbrief-walkthrough-part2} are promoted into the vault `.meeting-graphs/` store (the R6/H+GATE-2 calibration). Vault NOTES from that run were reverted at Rowan's request. See [[reference_r6h_gate2_calibration]]. One manual lift: Kumulus summary.md referenced by hand in `lexvision-poc/docs/kumulus/research/c1-kumulus-spec.md`.

**FILING STATUS (2026-06-18).** The premise "nothing filed" was only half-true. The 28 May (kumulus-medbrief) and 1 June (data-engineering) Kumulus meetings were ALREADY hand-curated, in higher quality than the pipeline, in `lexvision-poc/docs/kumulus/03-meeting-2026-05-28-vendor-proposal.md` and `04-meeting-2026-06-01-data-engineering-retro.md` (part of a rich hand-built Kumulus dossier: notes 00-10 + audit + research/). Delta-checked both graphs against those notes on 2026-06-18: ZERO genuine gaps (the 2 apparent gaps for DE were already elsewhere in the dossier). Do NOT re-file those two. The other three were genuinely unfiled and ARE now filed (each carries a frontmatter `graph_ref` pointer): kumulus-regroup -> `lexvision-poc/docs/kumulus/11-meeting-2026-06-12-regroup.md` (curated dossier note); the two MedBrief demos -> `medbrief-onboarding/notes/meetings/{slug}.md`. Routing was project-only (no strategic-vault writes). lexvision-poc was vault-coupled in the same session (hub down-link in `Projects/lexvision/LexVision POC.md`, new `docs/SOURCES.md`, CLAUDE.md coupling section).

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

**DONE (2026-06-18):** Filing complete (see FILING STATUS above). The 3 unfiled meetings were placed into their projects from the vault `.meeting-graphs/` store; the 2 already-hand-filed Kumulus meetings were delta-checked and left as-is. `calibration-misplaced-cleanup.md` is now historical (those mis-placed bullets were superseded by the hand-curated dossier, not re-placed).
