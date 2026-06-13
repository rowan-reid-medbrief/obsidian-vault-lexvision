---
type: meeting-timeline
date: 2026-05-28
title: "Kumulus & Medbrief — Vendor Proposal"
---

# Timeline — Kumulus & Medbrief Vendor Proposal

| Time | Event | Speaker | Type |
|------|-------|---------|------|
| 0:05 | Meeting opened; João introduced as presenter | Laura Gongas | — |
| 0:59 | Recap of proposal scope: NICE ingestion, anonymisation, tokenisation, comparison | João Marçura | Claim |
| 3:49 | Scope defined: one domain, 1-2 cases, entity extraction, anonymisation, initial comparison | João Marçura | Decision (0002) |
| 5:02 | System will not provide clinical or legal conclusions — only alignment/deviation | João Marçura | Claim (gf0003) |
| 5:57 | Q: Will PoV cover multiple NICE guidelines per case? | Laura Gongas | Question (0001) |
| 6:30 | Every medical-legal case contains handwritten notes in some form | Steve Ashford | Claim (0003) |
| 7:10 | Cases typically reference 1–3 NICE guidelines; rarely more | Steve Ashford | Claim (0004) |
| 8:20 | Medbrief's existing Document Intelligence OCR can be reused — no re-OCR needed | João Marçura | Decision (0001) |
| 9:05 | Q: What exactly is deterministic pseudonymisation? | Laura Gongas | Question (0002) |
| 10:30 | Medbrief holds compliance certifications required to obtain NICE API key | João Marçura | Claim (0002) |
| 11:00 | Medbrief responsible for obtaining NICE API key | João / Laura | Decision (0003) |
| 13:40 | NICE API stores historical guideline versions queryable by year and ID | João Marçura | Claim (0001) |
| 14:10 | NICE previously directed users to National Archive — questioned current state | Steve Ashford | Claim (0005) [CONTRADICTS claim:0001] |
| 15:08 | NICE API integration in scope: Medbrief leads, Kumulus supports technically | João Marçura | Decision (0003) |
| 16:00 | Cases must be compared against the guideline version current at time of procedure | João Marçura | Claim (0007) |
| 17:30 | PoV NICE API integration enables future full-catalog ingestion without new work | João Marçura | Claim (gf0008) |
| 19:01 | Entity dimension schema: patient, doctor, hospital, case, document (five types) | João Marçura | Topic (gf0005) |
| 20:00 | Entity classification schema must be agreed with Medbrief data science team before coding | Brendan Hughes | Decision (0006) |
| 21:30 | Sending PII to LLMs is too risky even within Azure AI Foundry | João Marçura | Claim (0008) |
| 25:00 | Entity dimensions must be scoped per-case to prevent cross-case identity confusion | João Marçura | Claim (0011) |
| 28:00 | Brendan: personal identifiers (NHS number, address) distinct from entity attributes (blood pressure) for PII scoping | Brendan Hughes | Claim |
| 32:59 | Databricks chosen over Microsoft Fabric for parallel unstructured data processing | João Marçura | Decision (0005) |
| 33:10 | Databricks with Spark is best-in-class for this parallel processing workload | João Marçura | Claim (0009) |
| 33:30 | Fabric acceptable only if a one-hour batch wait is tolerable | João Marçura | Claim (gf0011) |
| 33:45 | Model fine-tuning out of scope; pre-trained Azure AI Foundry models used as-is | João Marçura | Claim (gf0004) |
| 34:00 | Azure AI Foundry chosen for entity extraction — no bespoke NER framework | João Marçura | Decision (0007) |
| 34:50 | Medbrief already has clinician-reviewed ground truth for sample cases | Laura Gongas | Claim (0010) |
| 36:00 | Manual review replaced with quantitative evaluation in success criteria | Laura Gongas | Decision (0008) |
| 38:30 | Q: How will pseudonymisation be evaluated for OCR-missed handwritten content? | Momoko Iwagami | Question (0008) |
| 41:36 | System outputs alignment/deviation with page-level evidence pack and traceability | João Marçura | Claim (gf0003) |
| 42:00 | Data pipeline to be built for scale beyond the 2-case PoV | João Marçura | Decision (0011) |
| 44:51 | Engagement timeline: 10 delivery weeks + 2 testing = ~12 weeks total | João Marçura | Claim (0012) |
| 45:30 | Microsoft 12-week funding deadline: PoV must be delivered within 12 weeks of start | João Marçura | Claim (0013) |
| 47:00 | Medbrief can take full Milestone 1 ownership without committing to Phase 2 | João Marçura | Decision (0009) |
| 51:08 | Azure cost capped at ~$700/month including 30% buffer; Databricks is dominant cost | João Marçura | Claim (0014) |
| 52:30 | Anonymisation compliance certification out of scope for PoV | João Marçura | Claim (gf0007) |
| 54:00 | MLOps engineer to review and approve Azure infrastructure choices | Laura Gongas | Decision (0010) / Action (0008) |
| 57:02 | Full engagement cost: ~£35,000 before Microsoft incentives | João Marçura | Claim (0015) |
| 57:30 | Microsoft incentives (Data POV + AI POV) reduce cost by ~£22,000 | João Marçura | Claim (0016) |
| 58:00 | Net cost to Medbrief: ~£13,000 after both Microsoft funding streams | João Marçura | Claim (0017) |
| 58:30 | Brendan: Medbrief had expected full Microsoft sponsorship | Brendan Hughes | Question (0010) |
| 59:00 | Scope revision agreed: comparison layer removed, Medbrief team resources it | João / Laura | Decision (0012) |
| 60:00 | João to deliver revised zero-cost proposal within 5 business days | João Marçura | Action (0009) |
| 61:56 | Meeting closed | — | — |
