---
name: reference_meeting_graph_outputs
description: Locations and stats for the two meeting-graph runs completed 2026-06-08 (DE Discussion + Kumulus Vendor Proposal)
metadata: 
  node_type: memory
  type: reference
  originSessionId: 95fbdc5d-e42a-43bb-9c2b-56f4db01df7a
---

Both runs used Phase B recall recovery (gapfill, grounded_admit, chunk_budget, anchors, validate_repair, gleaning_passes=2).

**Data Engineering Discussion (2026-06-01, ~37 min)**
- Output: `~/meeting-graph-output/data-engineering-discussion-2026-06-07/`
- 115 nodes, 51 substantive, 205 edges
- 15 gap-fill nodes across 2 gleaning passes (containment only, NLI not triggered)
- Participants: Rowan Reid, Laura Gongas, Deon Kuhn, Brendan, Mediha, Vanessa, Chantel Pilla (Teams VTT — named speakers)
- Topics: Expert Match storage endpoint, Cumulus ground truth, NICE API, data architecture proposal, priority order

**Kumulus & Medbrief Vendor Proposal (2026-05-28, ~62 min)**
- Output: `~/meeting-graph-output/kumulus-medbrief-2026-06-07/`
- 152 nodes, 53 substantive, 334 edges
- 7 gap-fill nodes (4 rejected by NLI gate)
- Speaker mapping: SPEAKER_03=Joao Margura (Kumulus), SPEAKER_06=Laura Gongas, SPEAKER_00=Brendan Hughes, SPEAKER_01=Steve Ashford, SPEAKER_02=Vanessa Patrocinio
- Key commercial: £35k full cost, £22k Microsoft discount, £13k net; scope revised (comparison layer removed); revised proposal in 5 business days

**Next step:** Run `/promote-graph` or `/meeting-to-vault` to bridge outputs into the Obsidian vault.
