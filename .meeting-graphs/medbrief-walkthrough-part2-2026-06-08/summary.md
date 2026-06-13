---
title: "MedBrief Walkthrough Part 2 (meeting graph)"
type: note
created: "2026-06-12"
tags: [meeting-graph, medbrief, onboarding]
source_recording: "MedBrief Walkthrough Part 2-20260608"
presenter: Chantel van Wyk
duration: "1h 51m"
---

# MedBrief Walkthrough Part 2

## TL;DR
A full feature-by-feature demo of the MedBrief platform, presented by [[Chantel van Wyk]] to [[Rowan Reid]] as developer onboarding. It walks the whole case lifecycle: records management and the permission model, the Apryse document viewer with CER bookmark and heading extraction, the MedBrief Insights AI panel (Ask Alex), CER indexing, key events and chronologies, Early Case Assessment, the radiology viewer, MedBrief Match expert matching, letters of approach and instruction, the expert experience, disclosures, and the admin and billing sections. Much of the AI surface (Insights, the CER index, the chronology wizard, key events) is in development rather than live, and several decisions on the roadmap, scope, and pricing are still open.

## How MedBrief fits together (orientation)
MedBrief processes medical records for medico-legal cases. The spine of the product is:

1. **Records** come in (often as a CER, a computerised electronic record from systems like Epic), get sorted into a folder structure, and are shown through the Apryse viewer.
2. **AI features** sit on top of the sorted records: MedBrief Insights / Ask Alex to interrogate them, the CER index to extract headings and dates, key events and chronologies to build a timeline.
3. **Expert workflow**: MedBrief Match finds a suitable expert, a letter of approach is sent, the expert responds inside the platform, and a letter of instruction follows.
4. **Admin and billing**: disclosures share records between parties, DocSorter configures sorting, and invoicing runs through Xero.

## Decisions
Stated by [[Chantel van Wyk]] unless noted.

**Made**
- The CER index pivoted away from trying to identify clinical sections, towards extracting bookmarks (with a visual language model extracting headings as the fallback). Reason: clinical-section identification is too hard because content varies and a single page can hold several sections.
- The CER index launches on Epic only, with other CER types attempted later. Reason: Epic covers roughly 70% of computerised electronic records.
- MedBrief Insights / Ask Alex will not go to production until the AI team has confirmed the model's accuracy is good enough. Reason: an inaccurate assistant is harmful in a medico-legal context.
- Key events as an AI-generated output is out of the MVP. The chronology wizard is built first; key events come later. Reason: key events is hard to do accurately without a chronology.
- The letter of approach PDF is not emailed as an attachment. It is encrypted and only reachable once the expert logs in, which is what enables the response workflow.
- Instructed status is inferred from the moment an expert is invited to a matter, since an expert is only ever invited after being instructed.
- Agency notifications were removed: MedBrief no longer notifies expert agencies when a linked expert is instructed or invited, having concluded the notification served no necessary purpose.

**Tentative**
- MedBrief Insights will pick up a subtle version of the MedBrief Match purple palette (mainly the button and logo) to tie the AI features together visually.
- MedBrief Match will show the total number of similar cases an expert has worked on across the platform, but restrict the detailed case view for privacy.
- Experts will be required to accept MedBrief terms and conditions whatever their response (accept, decline, or request information).

**Deferred / open**
- 'Private Folders' (the records root folder) will be renamed, possibly to 'Workspace', as part of a parked improvements project.
- Users' folders within Case Documentation will be grouped by type (internal, client, expert) instead of listed alphabetically.
- The MedBrief Match service markup is not finalised: the options on the table are 8.5% or 14.5% of the expert's total fee.

## Action items
Most of these are MedBrief-team roadmap items Chantel described rather than tasks assigned in the meeting.

- Build the chronology wizard so clinicians can generate hyperlinked digital chronologies in MedBrief. This is a prerequisite for the AI key-events work.
- Develop a generalised date-extraction model (AI team) rather than per-section rules for each CER type.
- Extend the records-page date-range filter so it applies to individual documents within files, not just whole files. Owner: [[Dion]].
- Save annotation and redaction coordinates at a granular level so they survive record updates that shift page numbers or positions. Owner: [[Dion]].
- Build in-platform generation of the letter of instruction, mirroring the letter-of-approach workflow (clients currently create it outside MedBrief).
- Automatically route expert email replies (sent to the office address rather than through the platform) to the correct matter.
- Add an AI step to replace the claimant or patient name with initials in the letter of approach, replacing the current manual process.
- Automate creation of a billing service request when a letter of approach is sent, and track what follows.
- Let clients request customisations to the letter-of-approach template, with MedBrief maintaining client-specific variants.
- Add an 'Invite this expert' button on the MedBrief Match expert page so a solicitor can invite directly from Match.
- Change the Match similar-case display to show the total count across all matters, not just the current client's.
- Prompt experts to classify a file they upload (invoice, report, or other), which drives downstream handling.
- Show a Match marker next to any expert on the users page who was contacted via MedBrief Match.
- Fix the MedBrief Insights feedback-mechanism font (too small).
- Finalise the MedBrief Match markup percentage (8.5% or 14.5%).
- Improve the client-upload flow so records route to the correct destination without the ops team moving them by hand.
- [[Chantel van Wyk]] to follow up on the suppressed-invitation notification issue she spotted during the demo.

### Relevant to you
None of these were first-person commitments you made in the call, but these are the items that point at you directly:

- **A possible project handover:** one of [[Dion]]'s two current projects, possibly the intra-file document date filter, may be handed to you. Chantel flagged this as contingent and not yet confirmed.
- **An expected follow-up from Dion:** Chantel expects [[Dion]] to follow up with you on the granular annotation and redaction coordinate-storage problem, to get your input on a solution.
- **Handover materials:** [[Chantel van Wyk]] committed to sending you links to the internal lookup tables and the MSR product-notes pages she uses for product reference.

## Open questions
All the questions in the demo were asked by [[Rowan Reid]] and answered by [[Chantel van Wyk]] in the moment, so none are left open. They are still a useful index of the things worth understanding. A sample:

- Was the MedBrief Insights chat interface built in-house or on a third-party library?
- The CER index extracts headings, not bookmarks? (clarifying the pivot)
- Why did MedBrief migrate the radiology viewer from Orthanc to Medream?
- Are there CER section types beyond the patient section and the repeatable event section?
- How do MedBrief clients currently find medical experts without using MedBrief Match?
- Is the letter of instruction created inside MedBrief like the letter of approach?

## Risks
- Requiring experts to agree to terms and conditions even when they decline is acknowledged as a risk that could cause expert drop-off. (raised by [[Chantel van Wyk]])

## Artifacts and systems referenced
**MedBrief features:** Records page, Unsorted Records folder, Private Folders, MedBrief Insights panel, Ask Alex, CER index, key events, chronology wizard, Early Case Assessment wizard, MedBrief Match, letter of approach, letter of instruction, user simulation, disclosures, communications tab, reports section, DocSorter, system messages, expert profiles.

**Third-party tools and systems:** Apryse (the document viewer, formerly PDFTron), Epic (CER source system), a visual language model for heading extraction, Orthanc (the former radiology viewer), Medream (the new radiology viewer), Figma (design mockups), Xero (invoicing).

**Reference material to chase:** the internal lookup tables, the MSR product notes, the MedBrief Index to Medical Records, the expert master list.

## People
- [[Chantel van Wyk]]: presenter, MedBrief team. Ran the walkthrough.
- [[Rowan Reid]]: newly-joined developer (you).
- [[Dion]]: developer at MedBrief. Owns the annotation/redaction coordinate work and the intra-file date filter, one of which may come to you.
- [[Anna]]: freelance designer at MedBrief. Responsible for the Figma mockups shown.

## Graph views
![[graph.mermaid.md]]
