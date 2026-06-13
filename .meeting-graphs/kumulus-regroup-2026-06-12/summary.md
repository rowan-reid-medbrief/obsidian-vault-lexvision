---
title: "Kumulus Regroup (meeting graph)"
type: note
created: "2026-06-12"
tags: [meeting-graph]
---

# Kumulus Regroup

## TL;DR
Rowan walked Deon and Laura through his Kumulus research document, which breaks the proposed clinical-data pipeline into discrete modules (M1 to M7) with clear inputs, outputs, metrics and benchmarks per module, and ties each module back to Brendan's patent. The work was prompted by Laura's ask to assess whether the vendor is recommending tooling to earn commission or because it is a genuine fit (the vendor had given three presentations by this point: the first on Amazon, the revised proposal on the 28th, and a subsequent PDF that reversed direction). The team agreed Kumulus should take modules two to seven (not OCR), that the reply to Vanessa needs to be more explicit (MedBrief will supply the entities to extract and classify), and to start the proof of concept narrow on case 39945 plus one similar antibiotic-discharge case before branching out. Laura takes the email and entity-extraction track; Brendan still has to verify the case and the NICE application form; Deon pulled Rowan onto an independent research task on two existing tickets.

## Decisions
- Use a two-layer raw/curated approach for the POC rather than the full bronze/silver/gold medallion, but add an intermediate layer so entity extraction and pseudonymisation can be evaluated (tentative); decided by [[Rowan Reid]], on Laura's prompt.
- Reuse Azure Document Intelligence for OCR, the same as Kumulus proposed for M1 (made); decided by [[Rowan Reid]]. MedBrief has already moved from Tesseract to it.
- Treat the entity model as aspirational and broad, then narrow it using the sample-case chronologies and the previously-defined pseudonymisation entities (tentative); decided by [[Rowan Reid]] and [[Laura Gongas]].
- Databricks over Microsoft Fabric for the data platform (made); decided by [[Rowan Reid]]. Databricks is more composable and gives finer control over data staging.
- Neo4j as the team's graph database preference (made); decided by [[Rowan Reid]].
- Treat CQRS as optional for the proof of value, worth it only if it is cheap to set up (tentative); decided by [[Rowan Reid]].
- Use Presidio for the first-pass pseudonymisation, with Label Studio for clinician annotation feeding back into a Presidio reconfiguration (tentative); decided by [[Rowan Reid]].
- Kumulus to build modules two to seven, not module one, since they do not do OCR (agreed); decided by [[Deon Kuhn]] and [[Laura Gongas]].
- Be more explicit in the email reply to Vanessa, since she is not technical (agreed); decided by [[Laura Gongas]].
- MedBrief will supply the entities to extract and classify; Kumulus does the entity extraction (agreed); decided by [[Laura Gongas]].
- Include the evaluation metrics in the email reply to Kumulus (agreed); decided by [[Laura Gongas]].
- Select case 39945 (Brendan's case) plus a similar antibiotic-discharge case for the POC (decided); decided by [[Laura Gongas]].
- Start narrow in one domain for the complex-pipeline POC, then scale (decided); decided by [[Laura Gongas]] and [[Deon Kuhn]].
- Branch out to other case types after the proof of value (decided); decided by [[Deon Kuhn]].
- Deon takes Rowan for the ticket research task rather than the data-strategy item (decided); decided by [[Deon Kuhn]].

## Action items
- Review the per-module evaluation metrics and the entities (pseudonymisation entities and case chronologies), then draft the email to Kumulus and have Rowan check it before it goes; owner: [[Laura Gongas]]. (This was voiced several times across the meeting: review the metrics, find the previously-defined pseudonymisation documentation, send the email, and start the entity extraction.)
- Add a point in the email clarifying the NLP semantic processing (M2) versus entity identification distinction; owner: [[Laura Gongas]].
- Check the selected case and the NICE application form; owner: [[Brendan Hughes]].
- Resend Rowan the ticket; owner: [[Deon Kuhn]].
- Take five minutes with Deon offline (Deon to call); owner: [[Laura Gongas]].

### Your follow-ups
- Do independent exploratory research on the two existing tickets (granular storing of records, and date filtering): assess the system as it currently is and what each ticket is asking, without Deon's input, and come back with ideas to compare against his own assessment. Depends on Deon resending the ticket.

## Open questions
- Should Kumulus build the hard custom modules (for example graph construction), or should MedBrief? (asked by [[Rowan Reid]]) Partly resolved: Kumulus takes modules two to seven, but whether MedBrief keeps the graph-construction work it has already started is left open.
- Will Presidio also work for entity extraction, so entities that will not be pseudonymised (for example medications) can still be tagged and the extraction module evaluated? (asked by [[Laura Gongas]]) Answered by Rowan: likely yes via spaCy inside Presidio, though he had not gone deep enough to be sure.
- What is meant by NLP semantic processing in module two? (asked by [[Laura Gongas]]) Answered by Rowan: M2 identifies named things, M3 classifies them; Laura noted she would normally fold semantics into identification, and will add a clarifying line to the email.
- Do rights and obligations come from the case or from the NICE guidelines? (asked by [[Laura Gongas]]) Resolved: they come mainly from the NICE guidelines (M4); Rowan conceded the point.
- Should we perfect the system for one case type, or branch out early to avoid overfitting? (asked by [[Deon Kuhn]]) Answered by Laura: start narrow on similar cases for a complex-pipeline POC, then scale; branch out after the proof of value.
- What is Rowan working on next? (asked by [[Deon Kuhn]]) Resolved: Deon's ticket research task.

## Risks
- Data-protection constraints apply to the NLP models used; some open-source models can be self-hosted, which is worthwhile for small NLP models (raised by [[Laura Gongas]]).
- Overfitting was discussed as a risk of perfecting the system on a single case type. The team's mitigation is to start narrow then branch out after the proof of value.
- A Claude-generated note (which Rowan flagged he had not yet read closely) warns that running the pseudonymisation process does not necessarily save time if it is not done properly (raised by [[Rowan Reid]]). Worth reading before committing the approach.

## To resolve
- **Module placement of the NICE guidelines.** Rowan placed the NICE guidelines input in M7 ("the NICE one is down somewhere, they're an M7"), while rights and obligations were earlier discussed as coming from NICE in M4. This is an in-meeting inconsistency to pin down before the module map is sent to Kumulus.

## Side notes
- **How Laura found the comparison case:** she searched the MedBrief patient database for deceased patients with anything involving allergies, contraindications or prescriptions, found several, and picked the antibiotic-discharge case as the closest match to case 39945.
- **Work reallocation off Rowan:** Deon took the expert-match-integration storage endpoints back from Rowan and handed them to the developer who wrote about 80% of the original code; Deon also took the cell integration. This clears Rowan's plate for the ticket-research task.
- **The ticket task is a deliberate comparison exercise:** Deon wants Rowan's assessment formed independently, without his input, so he can compare it against his own two assessments.

## Artifacts referenced
- Rowan Kumulus Research document (document) — the primary artefact Rowan presented.
- Primers and further learning document (document).
- Lucidchart diagram, "Kumulus Visualisation", Rowan's annotations (tool).
- Brendan's patent application (document).
- Module breakdown M1 to M7 with build tiers (commodity versus must-prove/custom).
- Medallion architecture, bronze/silver/gold (system); CQRS (system).
- OCR and platform: Azure Document Intelligence, Tesseract (prior), Databricks, Microsoft Fabric, Azure Data Factory, Azure Blob storage monitor, Azure AI Foundry, Neo4j.
- Pseudonymisation and NLP tooling: Presidio, spaCy, GLiNER, AllenNLP, Label Studio.
- Clinical coding standards: ICD-10, SNOMED CT, dm+d, OPCS-4.
- NICE guidelines, NICE pipeline, NICE application form, recommendation engine.
- Cases: case 39945 (Brendan's case: two medications should have been co-prescribed, one was omitted, the patient died) and a similar antibiotic-discharge case (patient discharged without antibiotics, leading to death).
- Tickets and other: granular-storing-of-records ticket, date-filtering ticket, company data strategy (broader future item), the Kumulus 28th revised-proposal recording, Kumulus's latest email (Vanessa's bullet-point reply), Claude (used for the entity-model and tools research).
- MedBrief systems and data: the patient/case database (queryable by allergies, contraindications, prescriptions, deceased status), the expert-match-integration storage endpoints, cell integration.

## People
- [[Rowan Reid]]: presenter; part-time CTO at Huble, working for LexVision and MedBrief. Most of the talking time and the highest graph centrality.
- [[Laura Gongas]]: AI team lead, MedBrief. Owns the email and entity-extraction track.
- [[Deon Kuhn]]: CTO, MedBrief. Directing work allocation and the client relationship.
- [[Brendan Hughes]]: CEO, LexVision; patent inventor. Needs to verify the case and the NICE application form.
- [[Vanessa]]: Kumulus contact (non-technical) handling the email exchange.
- [[Chantel]]: MedBrief colleague who ran a product walkthrough with Rowan.
- [[Momo]]: Deon's colleague (mentioned re Microsoft Fabric).

## Graph views
![[graph.mermaid.md]]
