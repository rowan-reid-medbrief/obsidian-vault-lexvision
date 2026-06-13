---
title: "MB Product Walk-through (meeting graph)"
type: note
created: "2026-06-12"
tags: [meeting-graph, medbrief, onboarding]
source_recording: "MB product walk-through-20260603"
presenter: Chantel van Wyk
duration: "57m"
session: "first of two"
---

# MB Product Walk-through (session 1)

## TL;DR
The first of two onboarding walkthroughs, presented by [[Chantel van Wyk]] to [[Rowan Reid]]. It focuses on the front of the MedBrief workflow: creating a matter through the matter-creation wizard, configuring services (records request, chronology, sort and paginate), the matter dashboard, and then the document-sorting pipeline (DocSorter and the Sally AI pre-processing system) that turns raw uploads into a sorted, indexed record set. It ran over time, so a follow-up session was agreed (that became the Part 2 walkthrough). Several concrete follow-ups for Rowan came out of it.

## How the front of MedBrief works (orientation)
1. A **matter** (a case) is created through the **matter-creation wizard**, which has replaced the older classic modal. The wizard collects the client, patient details, case type, and the **services** required.
2. **Services** are things like records request, chronology, and sort-and-paginate. Each has its own configuration page in the wizard.
3. Once records are uploaded, a **sorting session** runs them through **DocSorter** and the **Sally** AI pre-processing system, which unitises and classifies the documents into a sorted index (by trust, admission, record type).
4. The **matter dashboard** is the shared workspace where admins track progress, see service widgets, and manage the case.

## Decisions
Stated by [[Chantel van Wyk]] unless noted.

- The matter-creation wizard is the current standard for creating matters. The classic modal is effectively deprecated, though a small number of users still use it.
- A follow-up walkthrough session was agreed (likely two hours, or two one-hour slots) to cover the remaining topics, because this session ran over and Rowan had another meeting with Steve. This became the Part 2 walkthrough.
- Chantel will give Rowan access to the MedBrief production UI after the session, since Rowan currently has only database read access.

## Action items

**MedBrief / product:**
- Resolve the inconsistency where the same concept (a client) is labelled 'area' or 'storage area' in some parts of the UI. (raised when Rowan spotted it)
- The wizard services page is hard to use (questions are not easy to match to their service); Chantel has flagged it as needing improvement.

**Chantel to do:**
- Share the matter-creation wizard flow and summary document with Rowan.
- Share the MSR Products Confluence space link with Rowan as onboarding reference material.
- Walk Rowan through the disclosure workflow (which uses additional requests) later in the session.
- Add Rowan as a user on the MedBrief production environment and send the invitation.

### Your follow-ups
These are the items you took on or were directed to in this session:

- **Email Chantel tomorrow morning** with the status of the processing script and the sheet.
- **Book the follow-up session:** check calendars and book a follow-up with Chantel (likely two hours, or two one-hour slots) to continue the walkthrough. (This became the Part 2 session on 8 June.)
- **Explore the Grace Clayton matter** on the dev environment: it has a full sorted document set, including radiology, and is a good worked example to study.

## Open questions
All questions were asked by [[Rowan Reid]] and answered by [[Chantel van Wyk]] in the session, so none are left open. A useful index of what was worth clarifying:

- Is the autocomplete dropdown a list of clients, and why does it say 'area' instead of 'client'?
- Does MedBrief perform early case assessments within the platform itself?
- Would someone creating a new matter always know whether liability is admitted at that point? (Rowan noted there is no "I don't know yet" option.)
- Is the Form of Authority the form submitted to the trust to obtain medical records?
- Is the matter dashboard where an administrator tracks case progress and uploads documents?

## Artifacts and systems referenced
**MedBrief features:** matter-creation wizard, classic matter modal, matter dashboard, records-request service page, chronology service page, sort-and-paginate page, sorting session, records page, the wizard flow and summary documents.

**AI / sorting systems (relevant to the AI team):** DocSorter (the sorting tool) and Sally (the AI pre-processing system that unitises and classifies documents). Worth understanding how these two relate.

**Platform and reference:** MedBrief Secure Review platform (MSR), the MSR Products Confluence space, the matter flow diagram and the Frequently Used Terms glossary (both in Confluence), the predefined trust / medical-institution list, the Grace Clayton dev test matter.

## People
- [[Chantel van Wyk]]: MedBrief team member, presenter. Ran the walkthrough.
- [[Rowan Reid]]: newly-joined developer (you). Currently has database read access; production UI access to follow.

## Cross-reference
This is session 1. The [[MedBrief Walkthrough Part 2 (meeting graph)|Part 2 walkthrough]] (8 June) continues from here and covers records, the AI panel, MedBrief Match, the expert workflow, disclosures, and admin.

## Graph views
![[graph.mermaid.md]]
