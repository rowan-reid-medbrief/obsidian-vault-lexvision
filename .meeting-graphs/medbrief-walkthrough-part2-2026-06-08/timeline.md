---
title: "MedBrief Walkthrough Part 2 (timeline)"
type: note
created: "2026-06-12"
tags: [meeting-graph, medbrief, onboarding]
---

# MedBrief Walkthrough Part 2 - Timeline

Presenter: [[Chantel van Wyk]]. Audience: [[Rowan Reid]]. Duration: 1h 51m. 20 chapters.

## 1. Records page permission model: super-admin, expert and client folder views

`0:03 - 4:09`

Recap of the records page, how personal folders are created under both case documentation and private folders, and what super-admins, experts and clients each see. Covers the parked project to rename private folders to workspace and group users by internal, client and expert.

![](screenshots/frame-00004.png)
*The MedBrief Matter Dashboard for case 'Orla Grace Clayton', showing patient details, instructions, services, matter background narrative, matter notes, and a right-hand progress panel of work streams. This is the central per-case overview that ties together records, reviews and assessments.*

Key lines:
- **Rowan Reid:** So you said that like the clients get to see that like the appropriate folders they're supposed
- **Chantel van Wyk:** Then the unsorted records, which I said that any records that clients upload, they get uploaded
- **Chantel van Wyk:** And then case documentation, again, the same way that we see all the users, well, as a MedPref

## 2. Unsorted records folder, client uploads and folder actions

`4:09 - 6:51`

The unsorted records folder where client-uploaded records land, the duplication this causes for the ops team, and folder actions such as rename, delete, download and notify. Includes the suppressed-invitation case where notification is replaced by sending the invitation.

![](screenshots/frame-00005.png)
*The Records tab with the left-hand records tree and the Apryse document viewer rendering a MedBrief 'Index to Medical Records' cover page for the case. Shows how the chronological index sits alongside the underlying record files, with a 'MedBrief Insights' launcher bottom-right.*

Key lines:
- **Chantel van Wyk:** It's, I would say it creates a bit of duplication because if it is a matter that requires a sorting
- **Chantel van Wyk:** and then the ops team, they need to go download whatever the clients uploaded from this folder,
- **Chantel van Wyk:** So, okay, it's not working now for some reason, but what they, what the option that will appear

## 3. Records viewer (Apryse), CER bookmarks and the annotation/redaction problem

`6:51 - 15:43`

The Apryse (formerly PDFTron) records viewer: bookmark and heading navigation of long computerised electronic records, why MedBrief does not classify or date CER sections, and the annotations and redaction feature. Explains how updates lose annotations and Dion's granular-storing project to preserve coordinates across page changes.

![](screenshots/frame-00011.png)
*Apryse viewer on a Computerised Electronic Record for Jan Lanham, showing structured clinical notes from a 22/04/2020 Clinic/Practice Visit in the Plastics Dressing Clinic, including a Medication List, progress notes by nursing staff and an attribution key. Shows the granular clinical detail captured per encounter.*

Key lines:
- **Chantel van Wyk:** And then you get Oracle and you get a few others, but the epic ones are usually if they are bookmarked,
- **Chantel van Wyk:** Except for history, like when you get to history, advanced care, then they do go a little bit deeper
- **Chantel van Wyk:** So certain sections like all these, the patient section, they only, they only return the second

## 4. MedBrief Insights AI panel and Ask Alex mode

`15:43 - 19:35`

Introduction to the in-development MedBrief Insights AI panel and its primary Ask Alex mode for interrogating MedBrief-sorted records, with file and folder filters, example questions, references and a feedback mechanism. Notes the chat interface was built in-house and the AI team is still reviewing model accuracy.

![](screenshots/frame-00016.png)
*The Records tab with the document viewer on the Index to Medical Records and the AI 'MedBrief Insights' (Ask Alex) panel open on the right showing a 'How can I help you today?' prompt. Browser-windowed view (multiple tabs visible) demonstrating the AI insights assistant docked alongside the records.*

Key lines:
- **Chantel van Wyk:** Like I said, the user will be able to remove it if they want all the records, whatever query they put in to apply to all the records rather than just whatever they've selected.
- **Chantel van Wyk:** But since I am on this page, so one of the features that we're currently busy with is incorporating AI with MedWeb Insights, which is this button here.
- **Chantel van Wyk:** Now, the questions that you see or queries, the queries that you see in here was actually specific to a matter that you use for a demo for Gatsby Wix.

## 5. CER index mode: heading extraction, date and keyword filtering

`19:35 - 29:30`

The reworked CER index that extracts Epic bookmarks or, failing that, headings via a visual language model, presented as an interactive index with date-range and keyword filtering over heading content. Covers patient versus event sections, date-extraction rules per event type, and the decision to launch on Epic first as it is roughly 70% of CER records.

![](screenshots/frame-00021.png)
*The MedBrief document viewer showing a single page of a computerised electronic record (CER) from Cambridge University Hospitals / Addenbrooke's for patient LANHAM, Jan, with a left-hand bookmark/heading tree extracted from the record. It demonstrates how MedBrief parses CER files into a navigable outline of clinic visits, visit info, clinical notes, flowsheets and documents.*

Key lines:
- **Chantel van Wyk:** But they will also be able to filter the, once it appears, yeah, the content according to the, according to a keyword that's not in the second level, that's not returned as a second level heading.
- **Chantel van Wyk:** And like demographics, patient contacts, problem lists, all of that, it can't really be dated, or like allergies can't really be dated because it's not a datable, you know, item.
- **Chantel van Wyk:** So the patient, the first section, the patient section is a bit hard to date because a lot of the time it's only a summary of stuff that's further down in the document.

## 6. Records date-range filter on files and documents

`29:30 - 32:06`

How the records-page date range works: each document and folder carries a date range from DocSorter, but the filter currently applies at file level rather than to documents within a file. Dion is to extend it to filter documents inside files, and any applied date range auto-carries into Ask Alex.

![](screenshots/chapframe-06.png)
*The MedBrief Records module showing the document viewer for patient Orla Grace Clayton (University Hospitals Birmingham NHS Foundation Trust), displaying a structured 'Bed history' table and 'Clinical notes' from a Nervecentre-sourced record. The left panel is the records folder tree (super-admin view) and the top toolbar holds the Apryse viewer controls; this shows how tabular clinical data is surfaced inside extracted records.*

Key lines:
- **Chantel van Wyk:** So if I still have, so let's say if computerized, no, not a bad example, if antenatal records, or let's click on this one, if administrative documentation had multiple documents in it with different dates, and I click on it, even though the date range is applied, I will still see all the documents that's in it, regardless whether it actually falls within that date falls or not.
- **Chantel van Wyk:** All this means is that the date range of the, it lists the date of the first, the date, the first date of the first document and the date of the last document, the oldest document, the newest document and the oldest document within that file.
- **Chantel van Wyk:** This records the date filters independent of this feature as well, because it is, of course, useful, you know, for just whether we have MedBreat Insights or not.

## 7. Key events mode and the planned chronology wizard

`32:06 - 34:35`

The key events mode that lists a timeline of key events from the records, and why it is hard to do accurately. Covers the plan to build a chronology wizard so clinicians generate chronologies in MedBrief as a hyperlinked digital form rather than in Word, which would later feed key events.

![](screenshots/chapframe-07.png)
*The MedBrief Records viewer showing a generated 'Index to Medical Records' for Orla Grace Clayton (University Hospitals Birmingham NHS Foundation Trust), a hyperlinked index of record entries by date, alongside a right-hand 'Timeline of key events' panel. It illustrates how MedBrief builds a navigable master index/chronology across the disclosed records.*

Key lines:
- **Chantel van Wyk:** And then at some point, once we actually can do key events without the help of chronology, then the AI team will add key events as another mode or future for metric insights.
- **Chantel van Wyk:** So once this is created via the wizard, at least we will be able to present all this information in this panel.
- **Chantel van Wyk:** But the idea here is just to list a timeline of key events from all the information that's in the documents.

## 8. Key events positioning versus paid chronologies, and Figma mockups

`34:35 - 38:48`

Why key events exists as a lighter overview sitting between nothing and a paid chronology, framed against competition from AI legal-document providers and the cost of a full chronology. Reviews Figma designs by freelancer Anna for the key events view and the updated CER index.

![](screenshots/frame-00025.png)
*A CER page in the MedBrief viewer showing an Imaging report ('Orthopaedic pinning lower limb', final result) for patient LANHAM, with structured End Exam Questions and a deep left-hand heading tree grouping Clinical Notes, Imaging, Procedures, Labs, Flowsheets and more. It shows the depth of heading extraction MedBrief performs on hospital records.*

Key lines:
- **Rowan Reid:** So the key events, I guess just to summarize, is AI reading the documents and extracting out and representing the key events for someone just to have a look at.
- **Chantel van Wyk:** So like you see, the other chronology that I showed you is a lot more detailed and it's got verbatim copy and it's got, yeah, a lot more specific references.
- **Rowan Reid:** And what is the, like, what purpose does the key events, like, let's say we could generate key events either with chronologies on a case or no chronologies.

## 9. Early Case Assessment wizard

`38:48 - 42:12`

The ECA wizard that moved early case assessments from Word onto the platform, with structured questions on breach of duty and causation whose answers determine a supportive, not supportive or inconclusive conclusion. Notes that storing ECA data in the database makes it reusable by the AI team, for example for MedBrief Match.

![](screenshots/chapframe-09.png)
*The MedBrief clinical-summary / Early Case Assessment editor for Orla Grace Clayton, showing narrative findings (chemotherapy after surgery with page citations), a 'Point of note' rich-text box, Yes/No safeguarding and disclosure questions, and a 'Recommendations' section, with a 'Jump to section' navigator on the right. It shows the structured assessment output MedBrief produces with cited page references.*

Key lines:
- **Chantel van Wyk:** So depending on what the clinician selects with each question, that at the end will determine whether an early case assessment is supportive, not supportive or inconclusive.
- **Chantel van Wyk:** Or it does indicate that the defendant breached a duty of care or it does not indicate that the defendant breached the duty of care or it's inconclusive.
- **Chantel van Wyk:** So just ask a bunch of questions, like the total number of pages considered, the hospitals or the trusts or the medical institutions that it contains.

## 10. Radiology viewer migration from Orthanc to Medream

`42:12 - 44:35`

The radiology viewer, demonstrated in production, and the move from Orthanc to Medream. The main driver was broader format support, plus the ability to read PDF radiology reports inside the viewer, alongside study loading and measurement features.

![](screenshots/frame-00041.png)
*The MedBrief radiology DICOM viewer showing an axial CT abdomen slice with a vertical strip of series/slice thumbnails down the left, demonstrating scrolling and selecting through a multi-slice imaging study within the radiology viewer.*

Key lines:
- **Chantel van Wyk:** So it pretty much works the same as Orthanc, whether they drag and drop the series into
- **Chantel van Wyk:** And then the one thing it also supports is with different radiology that we do receive,
- **Rowan Reid:** We did create, we did create, we did build in an early version of the radiology viewer

## 11. MedBrief Match: expert-matching concept and enablement

`44:35 - 52:32`

Introduction to MedBrief Match (Medream Merge) for finding experts, currently live for select Lime users only, with enablement conditions such as matter-wizard creation and clinical-negligence cases. Covers AI-generated expert profiles sourced from the internet, the letter-of-approach approach, the cost advantage over expert agencies, and AI-recommended specialities and queries.

![](screenshots/frame-00046.png)
*The Match search form lets the user pick a speciality, accept MedBrief-recommended specialities, set a consultation element, and ask MedBrief Match in natural language or pick a generated suggested search. This shows how Match turns case context into a structured expert query.*

Key lines:
- **Chantel van Wyk:** And we created profiles for those experts, for expert match to use for expert or med brief match,
- **Chantel van Wyk:** Whereas with us, it hasn't been confirmed, well, finalized yet, but we're thinking of only asking
- **Chantel van Wyk:** For one, if it is a matter that was not created by the matter creation wizard, Medreamerge match

## 12. MedBrief Match results, similar-case matching and expert profiles

`52:32 - 58:02`

The expert search results grouped by speciality, including similar-case matching that cross-references the matter against other MedBrief Match matters. Walks through profile cards, hourly rate and turnaround data, filters, and AI-generated recommendation reasons for each expert.

![](screenshots/frame-00047.png)
*Match has returned 141 experts across four specialities, shown as ranked expert cards, with a Filters dialog open over them. The filters (hourly rate, AI hourly rates, number of prior instructions by firm, date of last instruction) show how results can be narrowed when shortlisting experts.*

Key lines:
- **Chantel van Wyk:** Then there is also filters available, although the filters right now isn't very useful, especially
- **Chantel van Wyk:** So if the moment they click that, then we consider it as the profile information that we collected
- **Chantel van Wyk:** seen to an expert, the first time that expert logs in, if they have not confirmed their profile

## 13. Generating and sending the letter of approach

`58:02 - 66:29`

Creating a letter of approach: standard template, the choice to show the claimant's full name or initials, AI-generated background and records of tape, attachments requested by Lime, and the criteria for sufficient matter information. The PDF is encrypted and viewed only after the expert logs in rather than sent as an attachment.

![](screenshots/frame-00055.png)
*The Letter of Approach editor for Dr Alastair Bint, an AI-drafted letter with editable sections (Background, Records obtained, Progress of litigation) and inline placeholder tokens such as [Claimant initials] and [Chapter] page references. An 'Ask Alex' style helper bubble ('How did we do with the case summary?') sits over the letter, showing the AI assists drafting and the user reviews and edits before sending.*

Key lines:
- **Chantel van Wyk:** Because if it does not have sufficient information, we don't, we obviously wouldn't know what the
- **Chantel van Wyk:** And if the user chooses to go ahead with an expert, they will click generate letter of approach.
- **Chantel van Wyk:** Either that, or it needs an early case assessment or a chronology or a clinical summary or act.

## 14. Expert experience: messages page, user simulation and responding to a letter of approach

`66:29 - 74:09`

The new messages navigation item and how a super-admin can simulate an expert user to see what they receive. Walks through the expert responding to a letter of approach with the eight client questions, the accept, decline or request-more-information flow, mandatory terms and conditions, and profile confirmation.

![](screenshots/chapframe-14.png)
*The Messages area lists all matters that have message threads, with a Search & Filter panel (Client, Manager, Order by). A yellow banner shows the user is in an expert simulation, impersonating James Scurr to see the experience from the expert's side, which is how MedBrief lets staff preview what an instructed expert sees.*

Key lines:
- **Chantel van Wyk:** The only difference is, is that the email obviously contains this link, click here to view and respond
- **Chantel van Wyk:** Uh, and then of course, very importantly, except the main brief user expert user terms and conditions.
- **Chantel van Wyk:** So for that reason, we've created a page specifically to list matters where, where experts have been

## 15. Letter of instruction, email-reply gap and billing automation plans

`74:09 - 82:54`

What happens after acceptance: the letter of instruction (created outside the platform for now), the manual handling of experts who reply by email, and the plan to invite the expert directly from the match page so the instructed status is captured. Also covers planned record-upload prompts to track report and invoice submission and automated billing service requests.

![](screenshots/frame-00065.png)
*The full message thread with Prof. Peter Holt inside MedBrief Match, showing back-and-forth emails about accepting a Letter of Instruction and confirming the email address to grant the expert access to medical records and enclosures. This is the two-way expert communication channel that keeps instruction correspondence inside the platform.*

Key lines:
- **Chantel van Wyk:** and they haven't confirmed their profile information yet, they'll get, they'll immediately get directed
- **Chantel van Wyk:** Um, like in this case, and the letter of instruction is also attached to, is also only accessible
- **Chantel van Wyk:** We don't yet have the status after that would be, for example, the report is the expert submitted

## 16. Inviting users and experts, roles and suppressed invitations

`82:54 - 86:24`

Inviting users from the users page, how suggestions only appear for people with prior dealings with the client, and the available roles including expert, view-only expert, scanner and matter project manager. Demonstrates suppressing an invitation to pre-create an expert folder and the planned MedBrief Match marker on contacted experts.

![](screenshots/chapframe-16.png)
*An 'Add Users' modal over a matter ('Mr Darren Joseph -v- United Lincolnshire Hospitals NHS Trust') with a role dropdown open showing Expert, Expert (View Only), Solicitor and Project Manager. Shows how MedBrief invites people to a matter and assigns their permission role.*

Key lines:
- **Chantel van Wyk:** If you've got the email address or the name, um, so is it, what was it, Alistair Bint, Alistair
- **Chantel van Wyk:** So a user only come up if it's found, if that user, or in this case, the expert had previous
- **Chantel van Wyk:** particular scanner does have download enabled, or it's just a matter of project manager that

## 17. Disclosures: inter-party record sharing

`86:24 - 93:40`

Disclosures, where one firm discloses records and radiology to an opposing firm, created through a client-managed wizard with a fee whose liability can fall on either firm. Covers recipient access by email or activation, the 30-day expiry with reactivation, and updating the disclosed record set.

![](screenshots/frame-00072.png)
*Step 2 of the disclosure wizard for 'Orla Grace Clayton', listing radiology studies with date performed, study description, source disc and Disc ID, all ticked via 'Select all radiology'. Shows how imaging studies are selected into a disclosure.*

Key lines:
- **Chantel van Wyk:** Um, and then they need to specify the recipient's location, but this is also dependent on who is
- **Chantel van Wyk:** I'm not going to recreate it, but I don't know why I just came here if I'm not going to recreate
- **Chantel van Wyk:** So all this is, there's just any communication, like emails, that are sent either to the medical

## 18. Communications tab and workflow-driving reports

`93:40 - 97:16`

The admin-only communications tab that links emails to a matter via reference number or records request, and the reports section that drives the ops team's workflow. Saved reports such as records-request daily chases, batches, clinical reports and new matter requests determine and track outstanding work.

![](screenshots/frame-00079.png)
*A dense matter-requests table (greyed behind a modal) with an 'Update Matter Request Status' dialog set to 'Instructed'. Shows the back-office workflow for tracking the status of records/medico-legal requests across a matter.*

Key lines:
- **Chantel van Wyk:** They need to send a follow-up email to find out how you're doing with the records that we requested, blah, blah, blah.
- **Chantel van Wyk:** that can create these safe reports based on various information for them to alter and modify their workflow.
- **Chantel van Wyk:** For clinical reports, if they need to keep track on what's outstanding, what's overdue, that type of thing,

## 19. Manage section: clients, DocSorter config, service options and invoicing

`97:16 - 104:45`

The admin manage section covering clients, firms (API import via Kennedys), matters, users and incomplete matters, plus DocSorter configuration such as clinical sections, sorting instructions and file-note phrases. Also covers expert agencies, records request centres, service options and timelines, billing items including the MedBrief Match markup, and generating invoices that sync to Xero.

![](screenshots/frame-00082.png)
*The full 'Manage Sorting Instructions' page listing per-client sorting instructions with created/updated timestamps, an 'Add Sorting Instruction' button and a client Search & Filter panel. Shows the catalogue of law-firm sorting rules that drive how records are sorted.*

Key lines:
- **Chantel van Wyk:** We used to, we actually used to, so whenever an expert was instructed that was linked to an expert agency, if they were instructed or invited to MedPREF, we'll obviously send the invitation email to the expert.
- **Chantel van Wyk:** And this is also, again, it will display the summary of how many service requests are in pending state, how many service requests are on hold, how many is incomplete, and then how many is complete.
- **Chantel van Wyk:** So, yeah, PC notes for any additional instructions, missing or updating records received or inserted into existing records, any additional updates, we sort of like.

## 20. Admin tools, profile page and product-notes handover

`104:45 - 110:57`

The remaining admin area: system messages, the radiology status panel, restoring deleted documents, blacklist and failed-login management, and help articles with the user-role matrix. Closes with the profile page (email changes, Microsoft single sign-on, MFA, login logs and downloads) and a handover of internal product-notes lookup pages.

![](screenshots/frame-00085.png)
*A matter dashboard for 'Brienne Marston -v- University Hospitals Coventry & Warwickshire NHS Trust' showing matter details, a clinical 'Matter Background' narrative, and collapsible counters for Records requests, Batches (3/3), Clinical reports, Additional requests and Sorting sessions. Shows the central matter hub tying together records workflow and case context.*

Key lines:
- **Chantel van Wyk:** And it's useful pages for, so this particular one is one I use a lot, but it's useful tables for if you need to know the meaning of certain values.
- **Chantel van Wyk:** But it's useful for the clients to keep track of when they do invite someone or give someone access, what that person can do or not.
- **Chantel van Wyk:** For example, signing and security, creating matters, managing matters, records page, radiology, inviting and manage matter users.

