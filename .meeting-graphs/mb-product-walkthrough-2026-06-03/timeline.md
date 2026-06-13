---
title: "MB Product Walk-through (timeline)"
type: note
created: "2026-06-12"
tags: [meeting-graph, medbrief, onboarding]
---

# MB Product Walk-through - Timeline

Presenter: [[Chantel van Wyk]]. Audience: [[Rowan Reid]]. Duration: 57m. First session. 16 chapters.

## 1. Matter dashboard, the four views and the renewal cycle

`0:01 - 2:11`

Chantel opens MedBrief logged in as a super-admin and walks the matter dashboard's four views (last viewed, added as fee earner, accepted invitations, renewals). She explains the two-year licence then annual renewal cycle and the 30/7/1-day reminder emails.

![](screenshots/frame-00004.png)
*The MedBrief home dashboard for user Chantel van Wyk (Main SA). Lists most recently viewed matters with toggles, Messages buttons and tabs (Viewed, Favourites, Invitations, Renewals), plus a right-hand 'Search all matters' panel filtered by Client, Manager and Type. This is the landing point from which matters are opened or created.*

Key lines:
- **Chantel van Wyk:** there's a two-year period where they pay a a license fee for two years and then after those two years it
- **Chantel van Wyk:** renews for one year so most some of them have have like a one-year period before it renews some of them
- **Chantel van Wyk:** like like like find that like a contractual renewal yes so so for most clients when they open a matter

## 2. Creating a matter: client option and wizard versus classic modal

`2:11 - 3:09`

She covers the three matter-creation entry points a super-admin sees (add client, classic, new wizard) and what clients see instead. The classic modal-and-flyout is contrasted with the newer matter-creation wizard, which is now the standard route.

![](screenshots/frame-00006.png)
*The classic 'New matter' modal dialog overlaying the dashboard, showing the single-form approach to matter creation. Grouped sections for Client details, MedBrief licence, Patient details and Matter details with fields such as Client, Team, Default matter user role, Licence level, Patient/client name, Patient date of birth, Manager, Client matter number/reference, Billing code, Matter type (Clinical negligence) and Estimated client value. Contrasts with the later step-by-step creation wizard.*

Key lines:
- **Chantel van Wyk:** familiar with i don't know if this is still from your days where it's it's a modal and then you pull out
- **Chantel van Wyk:** latest new matter creation which we refer to as the matter creation wizard the classic one you might be
- **Rowan Reid:** the gotcha yeah that's look that it looks similar okay so it's just a version two of just making it a

## 3. Wizard overview document: default, service-dependent and summary pages

`3:09 - 5:03`

Chantel shares a summary document that maps the wizard flow: the default pages everyone sees, the service-specific pages that appear based on first-page selections (chronology, records request), supporting documents for consent forms and death certificates, and the final summary page.

![](screenshots/frame-00011.png)
*The dashboard back on the 'Renewals' tab, listing matters due for renewal within the next 30 days, each row showing a reference, client, updated date and a 'Renewal due' indicator (Tomorrow / This week). Same Search-all-matters filter panel on the right. Shows how matters are tracked for renewal.*

Key lines:
- **Chantel van Wyk:** that that everyone will see when they create a matter these pages here in the middle this is dependent
- **Chantel van Wyk:** once they pass the service pages then they're back to the default pages that everybody else sees which
- **Chantel van Wyk:** their medical records to be requested from whichever medical institution that's usually if the records

## 4. Live wizard services page and selecting clinical negligence services

`5:03 - 12:25`

Working live in the Bulldog/Ditcher dev client, she explains client-level service defaults and the services page she dislikes. She picks clinical negligence over personal injury and steps through the service questions: records request, review before sorting, early case assessment, sorted records, chronology and schedule of radiology.

![](screenshots/chapframe-04.png)
*The new step-by-step 'Create a Matter' wizard (URL /matter-request) on the services step. A confirmation banner reads the matter will be hosted on the MedBrief Secure Review platform, then asks which area the matter is for (dropdown showing Building Solicitors & Consulting / Personal Injury), followed by an Additional Services questionnaire of yes/no options. This is the wizard alternative to the classic modal.*

Key lines:
- **Chantel van Wyk:** clients so i'm just going to select bulldog we are we we are on dev so i don't have to worry about emails
- **Chantel van Wyk:** case assessment is exactly what it is it's performed on records that are not sorted so the clinicians go
- **Chantel van Wyk:** that's the difference so if they select no they'll just be charged hosting if they select yes then they

## 5. Matter detail page: manager, billing codes, contacts and case data

`12:25 - 16:36`

She completes the matter detail pages: reference number, matter manager drawn from client admin users, optional billing code (compulsory and predefined for defendant firms like Hampsons), team and additional contacts who receive digest and automated emails. Then case type, allegations, claim value, dates of negligence and knowledge, and the limitation date.

![](screenshots/chapframe-05.png)
*The Create a Matter wizard on step 1 of 7 (Matter Details) with the seven-step progress tracker visible: Matter Details, Records Requesting, Sort and Paginate, Chronology, Records Collection, Supporting Documents, Summary. Fields for Matter Reference Number (cvw-20260603-rowan), Matter Manager (Chantel / bulldogPM), Billing Code, Team, and an open Additional Contact(s) dropdown listing client admin/PM accounts.*

Key lines:
- **Chantel van Wyk:** contacts so that's all that is because sometimes the matter manager is not the only person well it might not
- **Chantel van Wyk:** optional field but i'm just going to select a date and the limitation that you know what the limitation date
- **Chantel van Wyk:** period is to to complain or to to put a claim in logic claim yeah exactly so that's what the limitation date

## 6. Patient details and the mother-and-child obstetrics case

`16:36 - 18:55`

Chantel fills in patient details (name, date of birth, deceased status) and shows how an obstetrics case type pre-populates two patients, mother and child. She covers adding additional patients and children, selecting the claimant, and naming defendants.

![](screenshots/chapframe-06.png)
*The Matter Details step with the Case Type dropdown open, listing clinical specialties (Epidemiology, Obstetrics, Neurology, Obstetrics - midwife / breech damage, Obstetrics - brain injury (HIE), Obstetrics - GP/Anaesthetist, etc.). Below are allegation entry fields ('Briefly, but as precisely as possible, complete the following') with an Add Allegation control, plus Estimated Client Value, Date of Alleged Negligence and Date of Knowledge fields. Shows how clinical-negligence case classification and allegations are captured.*

Key lines:
- **Chantel van Wyk:** is uh okay and then we get to the patient details so patient details right i'm sorry but i'm going to
- **Chantel van Wyk:** uh i'm sure they change you changed it recent well not recently last year from whatever it used to be
- **Chantel van Wyk:** actually i have seen your name um i don't know what your birthday is but let's say it's not the 26th

## 7. Records request service page and trust selection

`18:55 - 20:43`

Because records request was selected, the wizard shows the records request page. She selects the trust or medical institution from a predefined list (with pre-populated fields), marks it as new records for both patients, and explains the against-trust checkbox and how the matter name is generated from claimant and defendant.

![](screenshots/chapframe-07.png)
*MedBrief matter-creation wizard on the Records Requesting step, with an expanded request card for Midlands Medical Partnership (High Street Surgery) showing the trust/centre address fields and a New Records vs Updated Records toggle. This is where the legal team specifies each healthcare provider records will be requested from.*

Key lines:
- **Chantel van Wyk:** great um and this is then just need to select obviously if this is not complete they need to complete it
- **Chantel van Wyk:** but this is a request for new records or updated records and for the sake of this demo it's new records
- **Chantel van Wyk:** where the record should be collected from um and then once i've done also this is a predefined list so

## 8. Sort and paginate settings and the chronology service page

`20:43 - 23:24`

She walks the sort-and-paginate page (per-centre versus continuous pagination, prefixes, padding, page-number position and background) with its live preview. Then the chronology service page: chronology for which patient, key date range, and whether liability is admitted, prompting a discussion of the missing don't-know option.

![](screenshots/chapframe-08.png)
*The Chronology Options step of the Create a Matter wizard, with the progress stepper (Matter Details, Records Requesting, Sort and Paginate, Chronology, Records Collection, Supporting Documents, Summary) visible across the top. Lets the user configure how MedBrief builds the case chronology after sorting completes.*

Key lines:
- **Chantel van Wyk:** if yes it's selected no uh do you have any documents you would like to aid blah blah blah no so then this
- **Chantel van Wyk:** then where the page should appear the side size of the page number and would you like a white background
- **Chantel van Wyk:** chronology it's asking me for chronology for who for the mother and for the mother the child or both the

## 9. Records destruction, supporting documents and creating the matter

`23:24 - 25:26`

Chantel sets what happens to records once done (destroy-all by default), uploads the form-of-authority consent forms required per patient for a records request, notes the death certificate requirement for deceased patients, reviews the summary page and creates the matter.

![](screenshots/frame-00013.png)
*The Supporting Documents step showing a Form of Authority document uploaded for rowan reid plus an Additional Documents (Optional) section. A notice warns not to upload medical records or radiology here (those go to the Unsorted Records folder once the matter is opened), clarifying the boundary between supporting paperwork and clinical records.*

Key lines:
- **Chantel van Wyk:** and confirm and then we've got one for each patient obviously the mother and the child need to have their own
- **Chantel van Wyk:** because most of the records we not we get nowadays are all digital um and not hard copies so the default
- **Chantel van Wyk:** is to destroy all but if it wasn't so for instance the the user can choose to to to um save or not save

## 10. Matter dashboard after creation: notes and records request widgets

`25:26 - 27:45`

Landing on the new matter's dashboard, she shows the displayed patient details, the MedBrief-admin-only notes section with important-flag highlighting and sorting, and the two records request service widgets created for the two patients.

![](screenshots/frame-00016.png)
*The opened matter dashboard for patient rowan reid, with tabs (Matter dashboard, Records, Radiology, MedBrief Match, Users, Disclosures, Communications, Download) and panels for Patient details, Instructions, and Matter background, alongside collapsible service-group widgets (Records requests, Batches, Clinical reports, Additional requests, Sorting sessions). This is the central working view of a live case.*

Key lines:
- **Chantel van Wyk:** obviously also displays on the matter dashboard now because i'm logged in again as a med brief administrator
- **Chantel van Wyk:** saw or what you worked on previously i think it's pretty much the same it is a little a bit different but
- **Chantel van Wyk:** created so and the reason why you see two is because there's two patients so it's one for the for the mom

## 11. Confluence detour: matter flow diagram and the glossary

`27:45 - 30:06`

She opens the MSR Products Confluence space, pointing to the matter flow diagram and the frequently-used-terms glossary. She defines the hierarchy of service group, service request and service option, and explains terms like fee earner.

![](screenshots/frame-00019.png)
*The MSR Product Confluence space homepage and left-hand page tree, listing the documentation structure: Useful Information, External Pages, Home Dashboard, and a Matter Creation Wizard (MCW) section enumerating each wizard step. This is the internal knowledge base mirroring the product's matter-creation flow.*

Key lines:
- **Chantel van Wyk:** um like fee earner for example and when i started there was a lot of reference made to fee earner and i kept
- **Chantel van Wyk:** actually does need a bit of updating but it's just to to explain to whoever how this works what the flow
- **Chantel van Wyk:** look for different terms um you can find it on this page and so that relates to the matter dashboard and

## 12. Batches, clinical reports and additional requests on the dashboard

`30:06 - 34:28`

Back on the dashboard she explains batches: linking or creating a batch request, that batches are only created when sorting or radiology is involved, and the hosting-only fallback. She covers the clinical reports group (early case assessment, chronology and schedule of radiology combined) and additional requests used for ad-hoc work and disclosures.

![](screenshots/frame-00032.png)
*Same matter dashboard with the Records requests collapsed to two request rows and the Clinical reports (0/2) accordion expanded, showing two report line items (Early case assessment; Chronology & SOR), each Pending awaiting review. Shows how reports/services are tracked as discrete items against the matter.*

Key lines:
- **Chantel van Wyk:** batch with the same details with the same with the same um medical institution uh let me actually create
- **Chantel van Wyk:** combined because i selected both services but if the if the clients had selected only chronology then it
- **Chantel van Wyk:** that they want us to do which is for this so additional requests we also use additional requests for the

## 13. Creating a sorting session and AI pre-processing via DocSorter

`34:28 - 41:11`

Chantel creates a sorting session, choosing between a client or MedBrief sort, selecting clinicians for each DocSorter stage (sorting, dating, admissions, file note and QA), and uploading a completed batch. She explains the requires-pre-processing flag that triggers AI unitisation and classification (the Sally system) before sending to the sorter.

![](screenshots/frame-00045.png)
*Matter dashboard Sorting sessions (0/1) accordion expanded on Session ID 454 (MedBrief Session), showing the session header (Batches Not Set, Provenance Batches NIA HPO Form Uploaded No, Sorter Chantel van Wyk (MAIN SA)) and a Sorting Session Details panel with active sorter and pagination configuration. Key view of how a DocSorter sorting session is configured per matter.*

Key lines:
- **Chantel van Wyk:** sorting session the first stage by default is also always classify um file net status i'm going to leave blank
- **Chantel van Wyk:** sort and paginate session but that is not automatically created that still needs to be created by the user
- **Chantel van Wyk:** the dating and then it's admissions and then there's the file note or the memo whenever they refer to memo

## 14. Records page folder structure and the sorted-records flow

`41:11 - 45:46`

She opens the records page with its folder tree and viewer, describing the four parent folders (records, case documentation, private folders, unsorted records), how private and case-documentation folders are auto-created per viewer or invited expert, and how sorted records are pushed from DocSorter into a ZZZ sorting-session folder for cleanup.

![](screenshots/frame-00048.png)
*The Records tab for matter 'Orla Grace Clayton', with a folder tree on the left and a MedBrief-generated 'Index to Medical Records' document open in the viewer (proposed matter between claimant Orla Grace Clayton and defendant University Hospitals Birmingham NHS Foundation Trust). Shows the paginated records index MedBrief produces.*

Key lines:
- **Chantel van Wyk:** it automatically gets added to the case documentation the case let me just backtrack a little bit so on the
- **Chantel van Wyk:** that i showed you earlier and that's that's where it will stay well the unsorted records also stay here so
- **Chantel van Wyk:** looks like um the index if you ever do need a matter i mean i think you do have access to production don't

## 15. Grace Clayton example matter and the sorted index structure

`45:46 - 49:55`

Using the Grace Clayton dev matter as a reference, Chantel shows the sorted index hierarchy: trust or institution, then admissions or events, then the records, repeated per patient so duplicates appear. She covers date ranges, page numbers and the bookmarks that mark updates added after a sorting session.

![](screenshots/frame-00050.png)
*Records tab for Orla Grace Clayton with the left-hand records folder tree fully expanded (numbered category PDFs under a hospital/date-range parent) while the document viewer pane is blank/loading. Shows the sorted records folder structure that mirrors the index.*

Key lines:
- **Chantel van Wyk:** all of grace clayton and then you've got the same trust for different patient which is the child elia elijah clayton
- **Chantel van Wyk:** admission uh again trust same thing admission ame attendance is outpatients etc etc and then so it's per per
- **Chantel van Wyk:** it's a trust per um per patient by the way that's why you see two so you've got gp records same trust for

## 16. Expert folders, suppressed invitations and session wrap-up

`49:55 - 57:24`

She explains case-documentation expert folders: the bell icon for disabled users whose folders are kept, and the suppressed-invitation workflow where a fee earner prepares an expert's folder before sending the invitation email from the users tab. The session closes with agreement to schedule a longer follow-up.

![](screenshots/frame-00053.png)
*The Users (invitations) management screen for the Orla Grace Clayton matter, listing invited participants and their roles (matter Expert, ProjectManager, plain Expert) with status toggles and states such as Pending and Suspended. Shows how experts and other roles are granted scoped access to a matter.*

Key lines:
- **Chantel van Wyk:** very much and then i'll speak to you maybe tomorrow yes lovely thank you so much chantelle it's a pleasure okay bye
- **Chantel van Wyk:** that that user is no longer available or they they've been but they they've been disabled yeah exactly and
- **Rowan Reid:** you let me know i'll have a look at our our schedules um and then yeah probably not today because i've got

