---
type: meeting-summary
date: 2026-05-28
title: "Kumulus & Medbrief — Vendor Proposal"
participants:
  - João (John) Marçura (Kumulus — presenter)
  - Vanessa Patrocinio (Kumulus — sales)
  - Steve Ashford (Kumulus)
  - Momoko Iwagami (Kumulus)
  - Laura Gongas (Medbrief)
  - Brendan Hughes (Medbrief)
  - Deon Kuhn (Medbrief)
  - Mediha Zukic (Medbrief)
  - Namrata Tanwani (Medbrief)
tags: [kumulus, medbrief, data-pipeline, vendor-proposal, entity-extraction, pseudonymisation, nice-api, azure]
---

# Kumulus & Medbrief — Vendor Proposal (2026-05-28)

62-minute meeting. [[Kumulus]] presented a fixed-fee data pipeline proposal to [[Medbrief]] covering entity extraction, pseudonymisation, and case-vs-guideline comparison using NICE guidelines. Closed with a scope revision: comparison layer removed, revised zero-cost proposal to follow within 5 business days (~£13k net after Microsoft incentives).

---

## Key Decisions

| # | Decision | Confidence |
|---|----------|------------|
| decision:0001 | Use [[Medbrief]]'s existing Document Intelligence OCR output as PoV input — no re-OCR of handwritten notes | 0.90 |
| decision:0002 | Limit PoV to one medical domain to keep scope bounded | 0.90 |
| decision:0003 | [[Medbrief]] is responsible for obtaining the NICE API key | 0.90 |
| decision:0004 | Select the simplest case with the fewest NICE guideline references for the PoV | 0.90 |
| decision:0005 | Databricks chosen over Microsoft Fabric for parallel processing of unstructured medical data | 0.90 |
| decision:0006 | Entity classification schema must be agreed with [[Medbrief]] data science team before any coding begins | 0.90 |
| decision:0007 | Azure AI Foundry models used for entity extraction — no bespoke NER framework | 0.75 |
| decision:0008 | Replace manual review with quantitative evaluation metrics in success criteria | 0.90 |
| decision:0009 | [[Medbrief]] can take full ownership at end of Milestone 1 without committing to Phase 2 | 0.90 |
| decision:0010 | [[Medbrief]] MLOps engineer to review and potentially modify Azure infrastructure choices | 0.90 |
| decision:0011 | Data pipeline to be built for scale beyond the 2-case PoV from the outset | 0.90 |
| decision:0012 | [[Kumulus]] to produce a revised zero-cost-to-client proposal removing the comparison layer | 0.90 |

---

## Action Items

### João Marçura ([[Kumulus]])
- action:0002 — Verify NICE API historical guideline coverage and earliest queryable year
- action:0004 — Agree entity classification schema with [[Medbrief]] data science team at project kickoff
- action:0005 — Define with [[Medbrief]] which entity types require pseudonymisation before coding begins
- action:0007 — Update success criteria to use quantitative evaluation metrics instead of manual review
- action:0009 — **Deliver revised zero-cost proposal within 5 business days** (comparison layer removed)

### [[Medbrief]] (owner: org:medbrief)
- action:0001 — Obtain NICE API key (Medbrief already holds required compliance certifications)
- action:0003 — Identify sample cases with the fewest NICE guideline references for the PoV
- action:0006 — Create ground truth labels for pseudonymisation and comparison evaluation on sample cases

### Laura Gongas ([[Medbrief]])
- action:0008 — MLOps engineer to review and approve proposed Azure infrastructure choices

---

## Open Questions

| # | Question | Status |
|---|----------|--------|
| question:0001 | Will the PoV cover multiple NICE guidelines referenced by a single case? | Partially resolved: yes, but scope limited to simplest case |
| question:0002 | What exactly is meant by deterministic pseudonymisation? | Addressed in chapter 6 |
| question:0003 | Has NICE confirmed the API provides access to historical guideline versions? | Contested (claim:0001 vs claim:0005) — action:0002 |
| question:0004 | Will handwritten notes OCR'd by Medbrief's existing pipeline be usable as PoV input? | Resolved: yes (decision:0001) |
| question:0005 | Is the NICE API connection in scope? | Resolved: Medbrief owns access (decision:0003) |
| question:0006 | Is existing OCR on handwriting reusable for this project? | Resolved: yes (decision:0001) |
| question:0007 | Which service or model performs entity extraction? | Resolved: Azure AI Foundry (decision:0007) |
| question:0008 | How will pseudonymisation be evaluated, especially for OCR-missed handwritten content? | Open — linked to action:0006 |
| question:0009 | What are the entity type and subtype classifications used before pseudonymisation? | Open — linked to action:0004 |
| question:0010 | Did [[Medbrief]] expect full Microsoft sponsorship with zero cost to them? | Resolved: no — hence decision:0012 |

---

## Key Claims

| Claim | Speaker | Confidence |
|-------|---------|------------|
| NICE API stores all historical guideline versions, queryable by year and ID | [[Kumulus]] (João) | 0.75 |
| NICE previously directed users to National Archive for old guideline versions — contested | Steve Ashford | 0.90 |
| Every medical-legal case will contain handwritten notes in some form | Steve Ashford | 0.95 |
| A typical case references one but sometimes two or three NICE guidelines | Steve Ashford | 0.90 |
| Cases must be compared against the NICE guideline version current at the time of the procedure | João | 0.90 |
| Sending PII to LLMs is too risky even within Azure AI Foundry | João | 0.90 |
| Databricks with Spark is best-in-class for parallel processing of unstructured medical data | João | 0.90 |
| Fabric is an acceptable choice only if a one-hour batch wait is tolerable; otherwise Databricks | João | 0.85 |
| [[Medbrief]] already has clinician-reviewed ground truth for the sample cases | Laura Gongas | 0.90 |
| Engagement estimated at 10–12 weeks (10 delivery + 2 testing) | João | 0.90 |
| Microsoft funding deadline is 12 weeks from project start | João | 0.90 |
| Azure cost capped at ~$700/month including 30% buffer | João | 0.90 |
| Full service cost is approximately £35,000 before Microsoft incentives | João | 0.90 |
| Microsoft funding reduces cost by approximately £22,000 (Data POV + AI POV) | João | 0.90 |
| Net cost to [[Medbrief]] after Microsoft incentives is £13,000 | João | 0.90 |
| System will not provide clinical or legal conclusions — only guideline alignment or deviation | João | 0.95 |
| Model fine-tuning is explicitly out of scope; pre-trained Foundry/Azure OpenAI models used as-is | João | 0.90 |
| Anonymisation compliance certification is out of scope for the PoV | João | 0.90 |
| PoV NICE API integration enables future full-catalog ingestion with no new integration work | João | 0.85 |

---

## Commercial Summary

| Item | Value |
|------|-------|
| Full engagement cost | ~£35,000 |
| Microsoft Data POV incentive | ~£11,000 |
| Microsoft AI POV incentive | ~£11,000 |
| Total Microsoft discount | ~£22,000 |
| **Net cost to Medbrief** | **~£13,000** |
| Azure running cost (PoV) | ~$700/month (capped, 30% buffer) |
| Timeline | 10–12 weeks |
| Microsoft deadline | 12 weeks from start |
| Scope revision | Comparison layer removed; revised proposal in 5 business days |

---

## Chapter Summaries

**Chapter 1 — Introductions (0:05):** Laura (Medbrief) opens the meeting, introduces João from [[Kumulus]], and invites him to present. João shares his screen after a brief technical fumble.

**Chapter 2 — Proposal Overview (0:59):** João recaps the proposal: gathering NICE guideline data, comparing it with medical-legal case documents, data anonymisation, and tokenisation. He outlines what the presentation will cover.

**Chapter 3 — Scope Definition (3:49):** João walks through the fixed-fee scope: one medical domain, one or two real cases, entity extraction, anonymisation, and initial case-vs-guideline comparison. Out of scope: handwritten note OCR from scratch, full historical NICE processing, production application development.

**Chapter 4 — Q&A: Guidelines and NICE API (5:57):** Laura asks about multiple NICE guideline references per case. Steve Ashford (Kumulus) clarifies cases typically reference one to three guidelines. The group confirms [[Medbrief]]'s existing OCR can be reused. Laura asks about deterministic pseudonymisation and NICE API key access.

**Chapter 5 — NICE API Historical Guidelines and Data Ingestion (15:08):** João explains the NICE API stores historical versions queryable by year and ID. Steve flags a past concern about archive availability. João describes Steps 1 and 2: NICE API ingestion and case PDF ingestion including chunking and metadata strategy.

**Chapter 6 — Entity Extraction and Pseudonymisation (19:01):** João covers Steps 3 and 4: entity detection and classification (patient, doctor, hospital) and PII replacement with deterministic tokens before LLM calls. Brendan Hughes raises the need to agree a classification schema with [[Medbrief]]'s data science team before coding begins.

**Chapter 7 — Full Architecture Walkthrough (32:59):** End-to-end Azure architecture presented: Blob Storage, Data Factory for orchestration, Databricks for raw/silver/gold layer processing, Azure AI Foundry for LLM inference, Azure Monitor for observability. Databricks preferred over Microsoft Fabric for this unstructured, parallel-processing workload.

**Chapter 8 — Case-vs-Guideline Comparison and Evaluation (34:50):** João walks through the deviation-check logic and evidence pack with page-level traceability. Laura notes [[Medbrief]] already has clinician-reviewed ground truth. Momoko raises the challenge of evaluating pseudonymisation on handwritten content that OCR may have missed.

**Chapter 9 — Activities, Success Criteria, and Delivery (41:36):** Six delivery steps outlined (scope alignment through handover). Laura requests quantitative evaluation metrics rather than manual review.

**Chapter 10 — Microsoft Funding and Timeline (44:51):** 10–12 week timeline presented with 12-week Microsoft deadline. [[Medbrief]] confirmed able to take full ownership at Milestone 1 without committing to Phase 2.

**Chapter 11 — Azure Costs and Assumptions (51:08):** Azure cost calculator walkthrough (~$700/month cap, Databricks dominant cost). Fixed-fee limits stated: one domain, two cases, no fine-tuning, no compliance certification, no production integration. Laura confirms MLOps engineer will review infrastructure.

**Chapter 12 — Pricing and Close (57:02):** ~£35k full cost revealed, reducing to ~£13k net after Microsoft incentives. Brendan indicates [[Medbrief]] had expected full sponsorship; João offers a revised zero-cost proposal removing the comparison layer, delivered within 5 business days.

---

## Participants

| Name | Organisation | Role |
|------|-------------|------|
| [[João Marçura]] | [[Kumulus]] | Presenter / Pre-Sales |
| Vanessa Patrocinio | [[Kumulus]] | Sales Manager |
| Steve Ashford | [[Kumulus]] | Technical (challenged NICE historical claim) |
| Momoko Iwagami | [[Kumulus]] | Attendee |
| [[Laura Gongas]] | [[Medbrief]] | Host / Product Lead |
| [[Brendan Hughes]] | [[Medbrief]] | Technical / Data Science |
| Deon Kuhn | [[Medbrief]] | Engineering |
| Mediha Zukic | [[Medbrief]] | Attendee |
| Namrata Tanwani | [[Medbrief]] | Attendee |
