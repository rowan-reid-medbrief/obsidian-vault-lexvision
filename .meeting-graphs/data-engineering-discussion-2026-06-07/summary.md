---
type: meeting-summary
date: 2026-06-07
title: Data Engineering Discussion
participants: [Rowan Reid, Laura Gongas, Deon Kuhn, Brendan, Mediha, Chantel Pilla, Fatima, Dave]
tags: [cumulus, medbrief, data-engineering, ground-truth, expert-match, nice-api, human-in-the-loop]
---

# Data Engineering Discussion — 2026-06-07

## Key Decisions

1. **Send full expert profile on sync** (ch. 1, confidence 0.95) — When calling the [[Expert Match]] AI ingestion endpoint, send the entire expert profile with all fields rather than only the changed fields. The endpoint determines what is relevant.

2. **Ground truth cases must be deceased patients** (ch. 2, confidence 0.90) — Following [[Brendan]]'s guidance, annotation cases should use deceased patients with simple content and minimal handwritten text, to satisfy privacy requirements.

3. **[[Cumulus]] scope reduced to entity extraction and pseudonymization** (ch. 3, confidence 0.95) — The original proposal exceeded budget. [[Cumulus]] was asked to resubmit with a reduced scope covering data ingestion, entity extraction, and pseudonymization only (the "green box" in their flow diagram).

4. **[[Cumulus]] NICE API key may be shared temporarily with key rotation on exit** (ch. 3, confidence 0.90, tentative) — [[Deon Kuhn]] proposed allowing [[Cumulus]] access during the engagement via Azure Key Vault, then rotating the key once the work is done. [[Laura Gongas]] wants to verify compliance with [[Brendan]] first.

5. **[[Rowan Reid]] to focus on [[Cumulus]] data engineering work** (ch. 5, confidence 0.95) — [[Deon Kuhn]] took back the [[Expert Match]] ingestion endpoint task. The task requires too much prior codebase context for [[Rowan Reid]] to ramp on quickly; coordinating closely with other developers would also pull attention away from the data engineering investigation the team needs most.

6. **Thumbs up/down tickets stay with [[Deon Kuhn]]'s side** (ch. 5, confidence 0.90) — [[Rowan Reid]] may have a data collation role once the pipeline is clearer, but the tickets remain with [[Deon Kuhn]] for now.

7. **Ground truth collection is the top priority; data strategy is longer-term** (ch. 5, confidence 0.90) — [[Laura Gongas]] stated the explicit priority order at close of meeting: ground truth collection first (clinician time is the bottleneck), data architecture review second, data strategy last.

8. **Expert Match endpoint prioritisation against other tasks before assigning** (ch. 1, confidence 0.90) — Superseded by decision 5; resolved in ch. 5 when [[Deon Kuhn]] retook the task.

---

## Action Items

### [[Rowan Reid]]
- ✓ Investigate the Expert Match update queue table and ingestion endpoint integration (ch. 1, superseded — [[Deon Kuhn]] ultimately took this)
- ✓ Join tomorrow's meeting with [[Brendan]] to define entities and cases for ground truth (ch. 2)
- ✓ Review [[Cumulus]] data architecture proposal (Databricks, Azure Data Factory, Data Lake) and assess its suitability (ch. 4, depends on [[Laura Gongas]] forwarding the presentation)
- ✓ Watch the hackathon meeting recording once access is granted (ch. 5, depends on access request email being sent)
- ✓ Take the script for [[Chantel Pilla]] (ch. 5)

### [[Laura Gongas]]
- Send [[Cumulus]] meeting recording access request email (ch. 2)
- Fill in the [[NICE]] API access application form (ch. 3)
- Invite [[Rowan Reid]] to the enterprise skills development platform (ch. 4)
- Forward the [[Cumulus]] architecture presentation to [[Rowan Reid]] once available (ch. 4)

### [[Deon Kuhn]]
- Take on [[Expert Match]] ingestion endpoints (ch. 5)
- Consider asking [[Chantel Pilla]] to bump the thumbs-down ticket priority to high (ch. 5)
- Send instance numbers to [[Brendan]] (ch. 5)
- Investigate anomalous expert profile instances created via direct profile update (overdue from Friday)

### Team (unassigned owner)
- Clarify with [[Cumulus]] their intended depth of [[NICE]] guideline entity extraction (ch. 3)
- Investigate [[NICE]] API compliance requirements in parallel with the application (ch. 3)
- If [[Cumulus]] does not handle [[NICE]] guideline entity extraction, [[Rowan Reid]] to take on that integration (ch. 3, conditional on scope clarification)

---

## Open Questions

1. **What annotation tool should be used for ground truth collection that meets data privacy requirements?** (ch. 2) — Options include existing tools or building in-house. Open.

2. **How does [[Mediha]]'s graph database work fit alongside the [[Cumulus]] proposed pipeline?** (ch. 2) — [[Mediha]] is on leave; the [[Brendan]] meeting tomorrow is expected to help clarify this.

3. **Is it compliant to share the [[NICE]] API key with [[Cumulus]] (non-UK based)?** (ch. 3) — [[Deon Kuhn]] leans yes (with key rotation); [[Laura Gongas]] wants to confirm with [[Brendan]]. [[NICE]] may also charge non-UK users. Open.

4. **Should [[Medbrief]] do [[NICE]] guideline entity extraction before or after the [[Cumulus]] engagement, to reuse their pipeline?** (ch. 3) — Depends on the [[Cumulus]] scope clarification. Open.

5. **Is there any additional [[Cumulus]] material beyond the pre-hackathon documentation?** (ch. 4) — Partially answered: a detailed presentation exists but is not yet accessible while [[Cumulus]] adjusts it.

---

## Key Claims

1. **Expert Match endpoint task requires significant prior knowledge** (confidence 0.90) — [[Deon Kuhn]]'s concern; primary justification for keeping [[Rowan Reid]] off it.

2. **[[Cumulus]]'s approach to pseudonymization is vague; they likely do not yet have a firm plan** (confidence 0.90) — [[Laura Gongas]] and [[Deon Kuhn]]'s shared assessment; reason for insisting on an independent ground truth framework.

3. **Without ground truth, third-party vendors produce proof-of-concept work of unknown quality** (confidence 0.90) — [[Laura Gongas]]'s experience; justification for prioritising ground truth collection above all else.

4. **[[NICE]] guideline data is effectively publicly available online** (confidence 0.90) — [[Deon Kuhn]]'s view; used to support the case for sharing the API key temporarily.

5. **[[Cumulus]] will deliver code transparently; [[Medbrief]] engineers can extend and reuse it** (confidence 0.90) — Motivates the architecture review: the tech choice matters because the team will own and maintain the code.

6. **The team lacks data engineering expertise and cannot critically evaluate [[Cumulus]]'s architecture claims** (confidence 0.95) — [[Laura Gongas]]'s admission; reason for asking [[Rowan Reid]] to conduct the independent assessment.

7. **Entity types in clinical guidelines and clinical case records are expected to be the same** (confidence 0.90) — [[Laura Gongas]]; means the two [[Cumulus]] pipeline tracks are complementary rather than divergent.

8. **Data architecture review is worthwhile regardless of whether [[Cumulus]] is ultimately engaged** (confidence 0.85) — [[Medbrief]] will need to build this stack with or without them.

9. **[[Cumulus]] will reveal more about their technical approach once the engagement formally starts** (confidence 0.85) — [[Deon Kuhn]]; some questions cannot be answered before contract sign-off.

10. **The safest [[Cumulus]] scope is entity extraction only; [[NICE]] guideline processing should be excluded from this engagement** (confidence 0.85) — [[Deon Kuhn]]'s recommendation; [[Cumulus]]'s intentions for the guidelines are unclear.

11. **[[Rowan Reid]] working closely with other developers on Expert Match would create distraction** (confidence 0.88) — Secondary reason [[Deon Kuhn]] retook the endpoint task.

12. **Clinicians cannot annotate ground truth cases during their billable working hours** (confidence 0.85) — [[Laura Gongas]]; annotation must happen after shifts, which constrains the timeline.

13. **Only two cases are needed for the initial ground truth annotation exercise** (confidence 0.85) — [[Laura Gongas]] citing [[Cumulus]]'s statement; the scope is manageable.

14. **[[Rowan Reid]] having time to investigate the data engineering stack is the most important thing the team is currently lacking** (confidence 0.90) — [[Deon Kuhn]].

15. **Third parties often recommend the newest or most expensive Azure services regardless of suitability** (confidence 0.90) — [[Laura Gongas]]'s concern; motivates the independent architecture assessment.

---

## Chapter Summaries

**Chapter 1 — Expert Match Storage Endpoint Integration (0:00–8:00)**
[[Laura Gongas]] opened by requesting that the dev team call the AI ingestion endpoint automatically whenever an expert or case is created, updated, or deleted, removing the need for manual syncing. The team walked through the three-table endpoint structure (expert, case, case-expert), examined the update queue table in production (which exists but is currently empty), and discussed cache invalidation implications. [[Deon Kuhn]] noted the task requires significant prior codebase knowledge and flagged it as a concern before assigning it to [[Rowan Reid]].

**Chapter 2 — Cumulus Scope and Pseudonymization Ground Truth (8:00–17:30)**
[[Laura Gongas]] introduced the [[Cumulus]] partnership, covering entity extraction and pseudonymization as the core scope. The team agreed they need to build their own ground truth dataset via clinician annotation of deceased-patient cases in order to evaluate [[Cumulus]]'s output independently, rather than relying on [[Cumulus]] to self-assess. Discussion covered annotation tooling, the option to pre-populate using AI to reduce clinician burden, and the fact that [[Mediha]]'s graph database work from Sprint 9 is paused while she is on leave.

**Chapter 3 — Cumulus Flow Diagram and NICE API Compliance (17:30–27:00)**
[[Laura Gongas]] shared the kumulus_flow.png diagram showing [[Cumulus]]'s proposed two-track pipeline: [[NICE]] guideline structuring (top) and clinical case entity extraction and pseudonymization (bottom), running in parallel before feeding a reasoning layer. The team debated the [[NICE]] API key sharing problem: [[Laura Gongas]] was uncomfortable sharing it with a non-UK entity; [[Deon Kuhn]] suggested temporary access via Azure Key Vault with key rotation on exit. An alternative emerged: [[Medbrief]] ingests [[NICE]] guidelines itself and hands [[Cumulus]] the resulting JSON, bypassing the key sharing issue entirely.

**Chapter 4 — Data Architecture Review and Rowan's Onboarding (27:00–33:20)**
[[Laura Gongas]] asked [[Rowan Reid]] to review [[Cumulus]]'s proposed data architecture (Databricks, Azure Data Factory, Data Lake) and assess whether it is fit for purpose. The concern is that vendors tend to propose the newest or most expensive services regardless of suitability, and the team lacks the data engineering background to evaluate these claims critically. [[Deon Kuhn]] suggested [[Rowan Reid]] use the enterprise skills development platform as a learning resource. [[Rowan Reid]] acknowledged his limited data engineering tool experience but committed to applying his judgement.

**Chapter 5 — Priorities, Human-in-the-Loop, and Closing Decisions (33:20–37:45)**
The team closed out remaining items. The Sally integration stays with [[Deon Kuhn]]. The human-in-the-loop thumbs up/down feature for [[Ask Alex]] (kicking off in June) is on [[Dave]]'s ticket; [[Rowan Reid]] may assist with data collation later. [[Deon Kuhn]] retook the [[Expert Match]] storage endpoint task, determining the ramp-up cost would be too high for [[Rowan Reid]] right now. Final priority order: ground truth collection first (clinician calendar time is the binding constraint), then data architecture review, then the wider data strategy.

---

## Participants

| Person | Role | Speaking turns |
|--------|------|----------------|
| [[Laura Gongas]] | AI team lead | 330 |
| [[Deon Kuhn]] | Lead developer | 212 |
| [[Rowan Reid]] | AI/data engineer, new to team | 165 |
| [[Brendan]] | Clinical team contact; holds patent document | 0 (referenced) |
| [[Mediha]] | Graph database / knowledge graph work; on leave | 0 (referenced) |
| [[Chantel Pilla]] | Expert profile completeness checks | 0 (referenced) |
| [[Fatima]] | MLOps/infrastructure focus | 0 (referenced) |
| [[Dave]] | Holds thumbs-down feature tickets | 0 (referenced) |
