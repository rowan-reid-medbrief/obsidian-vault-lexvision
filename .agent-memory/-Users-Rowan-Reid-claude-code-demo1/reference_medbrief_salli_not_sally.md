---
name: ""
metadata: 
  node_type: memory
  originSessionId: 09432ed0-e3e8-4516-b373-bcfe8799047b
---

There is no person named Sally at MedBrief. When "Sally" comes up in a MedBrief meeting transcript (e.g. in the context of the record-sorting algorithm or duplicate detection), it refers to **SALLI**, a MedBrief AI/software system, not a colleague.

**How to apply:** in meeting-graph extraction, transcript cleanup, or any MedBrief context work, treat "Sally"/"Salli" mentions as the SALLI system (an Artifact-type node: `artifact_type: system` or `tool`), never mint a `Person` node for it. If a prior graph already has a `person:sally` node from before this correction was known, it should be re-typed/relabelled to SALLI as an Artifact when reconciling into notes.

Related: [[reference_meeting_graph_outputs]]
