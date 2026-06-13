---
type: meeting-timeline
date: 2026-06-07
title: Data Engineering Discussion
---

# Timeline — Data Engineering Discussion

| Time | Event | Speaker | Type |
|------|-------|---------|------|
| 0:00 | Expert Match storage endpoint integration raised: dev team not yet calling the AI ingestion endpoint; manual sync still in place | Laura Gongas | Decision (context) |
| 0:10 | Expert Match storage endpoint integration priority to be ranked against other Rowan tasks before assigning to him | Deon Kuhn | Decision |
| 1:35 | Expert Match AI ingestion endpoint covers three tables: expert, case, case-expert | Laura Gongas | Claim |
| 2:35 | Update queue table exists in production but is currently empty; not yet logging update events | Deon Kuhn | Claim |
| 3:55 | Expert cache is described as "over-caching"; needs invalidation when ingestion endpoint is called | Laura Gongas | Claim |
| 3:55 | Expert Match endpoint task requires significant prior knowledge; unsuitable for Rowan at this stage | Deon Kuhn | Claim |
| 4:20 | Expert update queue table worth investigating as mechanism for triggering AI sync | Deon Kuhn | ActionItem |
| 5:15 | Send full expert profile (all fields) to AI ingestion endpoint on sync, not individual changed fields | Deon Kuhn / Laura Gongas | Decision |
| 7:20 | Ingestion endpoint documentation shared in chat | Laura Gongas | Claim (context) |
| 8:00 | Cumulus partnership introduced: entity extraction and pseudonymization as core scope | Laura Gongas | Decision (context) |
| 8:12 | Cumulus meeting recording access request email to be sent by Laura | Laura Gongas | ActionItem |
| 9:20 | Cumulus's approach to pseudonymization is vague; they likely do not yet have a firm plan | Laura Gongas | Claim |
| 9:40 | Without ground truth, third-party vendors produce proof-of-concept work of unknown quality | Laura Gongas | Claim |
| 10:20 | Ground truth annotation cases should be deceased patients with simple content and minimal handwritten text | Laura Gongas / Brendan (referenced) | Decision |
| 10:40 | Only two cases are needed for the initial ground truth annotation exercise | Laura Gongas | Claim |
| 11:00 | Annotation tool for ground truth must meet data privacy requirements; tool not yet selected | Laura Gongas | Claim |
| 13:00 | Rowan to join tomorrow's meeting with Brendan to define entities and cases for ground truth | Laura Gongas / Rowan Reid | ActionItem |
| 13:10 | Mediha's graph database and Cypher query work (Sprint 9) is paused while she is on leave | Laura Gongas | Claim |
| 15:50 | Cumulus proposed using an Azure Foundry model for pseudonymization; vague — no firm decision evident | Laura Gongas | Claim |
| 17:30 | Cumulus two-track pipeline architecture shown: NICE guideline structuring (top) and clinical case entity extraction and pseudonymization (bottom) running independently before a reasoning layer | Laura Gongas | Claim |
| 17:40 | Cumulus scope reduced to green box: data ingestion, entity extraction, and pseudonymization only | Laura Gongas | Decision |
| 18:10 | Awaiting Cumulus revised proposal; expected this week | Laura Gongas | ActionItem |
| 20:00 | NICE API access requires ISO compliance and UK-based registration | Laura Gongas | Claim |
| 20:30 | NICE may charge non-UK users for API access | Laura Gongas | Claim |
| 21:20 | NICE guideline data is effectively publicly available on the NICE website, reducing compliance concern | Deon Kuhn | Claim |
| 21:30 | NICE API key may be shared with Cumulus temporarily, stored in Azure Key Vault, with key rotation after engagement ends | Deon Kuhn | Decision |
| 22:20 | Laura to fill in NICE API access application form | Laura Gongas | ActionItem |
| 22:25 | Investigate NICE API compliance requirements in parallel with the application | Team | ActionItem |
| 23:00 | Alternative approach proposed: Medbrief ingests NICE guidelines itself and supplies JSON output to Cumulus, avoiding key sharing | Laura Gongas | Claim |
| 24:00 | Entity types in clinical guidelines and clinical case records are expected to be the same | Laura Gongas | Claim |
| 25:00 | Cumulus will deliver code transparently; Medbrief engineers can extend and reuse it | Laura Gongas | Claim |
| 25:20 | Cumulus planned to focus on a narrow case type (e.g. obstetrics) to limit the NICE guidelines scope | Deon Kuhn | Claim |
| 25:30 | Team to clarify with Cumulus their intended depth of NICE guideline entity extraction | Laura Gongas | ActionItem |
| 25:40 | Should Medbrief do NICE guideline extraction before or after the Cumulus engagement to reuse their pipeline? | Deon Kuhn | ActionItem |
| 26:00 | Cumulus will reveal more about their technical approach once the engagement formally starts | Deon Kuhn | Claim |
| 26:20 | Safest Cumulus scope is entity extraction only; NICE guideline processing should be excluded from this engagement | Deon Kuhn | Claim |
| 27:00 | The team lacks data engineering expertise and cannot critically evaluate Cumulus's architecture claims | Laura Gongas | Claim |
| 27:22 | Laura to invite Rowan to the enterprise skills development platform (data engineering learning section) | Deon Kuhn | ActionItem |
| 27:35 | Third parties often recommend the newest or most expensive Azure services regardless of suitability | Laura Gongas | Claim |
| 27:40 | Rowan to review Cumulus data architecture proposal (Databricks, Azure Data Factory, Data Lake) and assess suitability | Laura Gongas | ActionItem |
| 28:20 | Rowan is not a data engineering expert and has not used these tools himself | Rowan Reid | Claim |
| 31:15 | Laura to forward the Cumulus architecture presentation to Rowan once available | Laura Gongas | ActionItem |
| 31:50 | Data architecture review is worthwhile regardless of whether Cumulus is ultimately engaged | Laura Gongas | Claim |
| 33:20 | Ground truth collection is the single most important priority; data strategy is longer-term | Laura Gongas | Decision |
| 33:55 | Rowan having time to investigate the data engineering stack is the most important thing the team is currently lacking | Deon Kuhn | Claim |
| 34:35 | Human-in-the-loop / thumbs up/down pre-requisites due for Ask Alex in June; tickets with Dave | Deon Kuhn | Claim |
| 35:15 | Thumbs up/down tickets remain with Deon's side; Rowan may have data collation role once clearer | Deon Kuhn | Decision |
| 36:00 | Rowan's focus to be on Cumulus data engineering work, not Expert Match ingestion endpoints | Deon Kuhn / Laura Gongas | Decision |
| 36:40 | Rowan working closely with other developers on Expert Match would create distraction | Deon Kuhn | Claim |
| 36:35 | Deon to take on Expert Match ingestion endpoints | Deon Kuhn | ActionItem |
| 36:40 | Deon to consider asking Chantel Pilla to bump thumbs-down ticket priority to high | Deon Kuhn | ActionItem |
| 37:02 | Rowan to watch hackathon meeting recording once access is granted | Rowan Reid | ActionItem |
| 37:05 | Clinicians cannot annotate ground truth cases during their billable working hours | Laura Gongas | Claim |
| 37:25 | Rowan to take the script for Chantel Pilla | Rowan Reid | ActionItem |
| 37:35 | Deon to send instance numbers to Brendan | Deon Kuhn | ActionItem |
