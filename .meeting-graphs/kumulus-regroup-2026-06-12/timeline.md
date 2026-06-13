---
title: "Kumulus Regroup (timeline)"
type: note
created: "2026-06-12"
tags: [meeting-graph, timeline]
---

# Kumulus Regroup — timeline

Total length about 44.7 minutes. Speaking split (diarisation): Rowan about 22.5 min, Laura about 11.6 min, Deon about 5 min.

## 1. Opening and screen-share setup
**00:00 to 01:16**

Deon confirms the latest Kumulus email has been forwarded to Rowan. Rowan offers to run through his research document and starts sharing his screen.

![](screenshots/frame-00005.png)
*Rowan shares the "Rowan Kumulus Research" document in Word for the web, scrolled to the module catalogue.*

- Rowan: "let me just quickly run through my document to, I guess, just surface the high level thoughts and thinking."

## 2. Module breakdown approach and medallion architecture
**01:16 to 07:04**

Rowan explains why he decomposed the proposed system into modules with clear inputs, outputs, measurable metrics and benchmarks, and aligned them back to Brendan's patent so the build also substantiates the patent application. He covers the Databricks bronze/silver/gold medallion pattern and argues a two-layer raw/curated approach is enough for the POC. Laura asks for an intermediate layer so entity extraction and pseudonymisation can be evaluated.

![](screenshots/frame-00006.png)
*The "Rowan Kumulus Research" document on the module catalogue page, navigation pane expanded.*

- Rowan: "a module being something that takes particular clear inputs and outputs that we can kind of be opinionated on how it perhaps should be working internally, what metrics we can measure ... and then actually define sort of appropriate benchmarks for those things."
- Rowan: "I kind of tried to marry the modules back to the patent application as well, just so that it kind of can more clearly substantiate or support that application."
- Laura: "we normally have the raw, the intermediate steps, and then the actual output ... maybe just having the output won't give us like enough information to be able to evaluate all of them."

## 3. Per-module metrics and benchmarks
**07:04 to 09:15**

Rowan critiques Kumulus's vague success criteria (for example "one to two surgery cases processed") and proposes discrete metrics per module: parsing accuracy, fidelity, completeness, hallucination for ingestion. He names ScoreBench (a tool you can run) and ExtractBench (a methodology with self-prepared ground truth), and flags that rule structuring is novel with no established benchmark.

![](screenshots/chapframe-03.png)
*The M1 Document ingestion and OCR module detail, with an inputs/outputs/metric/benchmark comparison table.*

- Rowan: "They said success criteria for ingestion was one to two surgery cases processed. Like that's not, there's no metrics there to say, well, was it ingested well?"
- Rowan: "that score bench is an actual tool that we could run, and extract bench is just a methodology. So we prepare our own graph, ground truth data and then measure it."

## 4. Entity model and clinical coding standards
**09:15 to 14:11**

Rowan presents an entity model researched with Claude, grounded in ICD-10 (diagnoses), SNOMED CT, dm+d (UK medicines) and OPCS-4 (procedures), with a people/organisations/clinical hierarchy. Laura notes Brendan will want it generalisable to natural and legal entities per the patent. The team agrees the entity set serves two purposes (pseudonymisation and graph representation) and Laura will check the previously-defined pseudonymisation entities and the sample-case chronologies.

![](screenshots/chapframe-04.png)
*A "what Kumulus proposed against what we propose" comparison of the entity/ontology model.*

- Laura: "remember in the patent it says like, if it's like a natural and legal entity ... perhaps it makes sense to make it generalizable enough for non-clinical cases potentially."
- Rowan: "if we were to ask Cumulus to extract all of this, that could be the entire budget ... maybe we just needed them to prove the foundation and the structure and it works and then we could evolve it over time."
- Laura: "the entities that we have to extract has to be for two things. One is pseudonymization ... and then the other purpose is graph representation."

## 5. Platform infrastructure tooling
**14:11 to 16:35**

Rowan reviews the proposed Azure stack: the shift from Microsoft Fabric to Databricks (Databricks more composable, finer control over staging; Fabric a newer all-in-one abstraction), Azure Data Factory connectors, Blob storage monitoring, AI Foundry for models, and Neo4j as the graph database preference.

![](screenshots/chapframe-05.png)
*The document's "3. Tools (open-source and vendor)" section, a narrative list of named tools.*

- Rowan: "Databricks, which is more you pick and like more composable ... Microsoft fabric is more of like an abstraction layer, which doesn't actually give us the nitty gritty control."
- Deon: "I remember Momo and I saw it at an event and it was literally, the purpose was to consolidate all their disparate tools ... a catch all for anything data related."

## 6. Architecture and cross-cutting: CQRS
**16:35 to 18:25**

Rowan explains Kumulus's proposed CQRS (command query responsibility segregation) pattern, which separates the ingestion/processing layer from the queryable layer used by MedBrief. He judges it sensible for production scaling but not essential for a proof of value unless it is cheap to set up.

![](screenshots/chapframe-06.png)
*Lucidchart canvas "Kumulus Visualisation Draft #2" in edit mode, with a Risks and Mitigation Strategy header.*

- Rowan: "it's kind of like have your operational data store and all your processing in one place, then have your data ready for exposure for use in MedBrief separately ... it's not an absolute necessary, I say for a proof of value potentially."

## 7. Pseudonymisation ground truth and NLP tooling
**18:25 to 25:12**

Rowan researches building the pseudonymisation ground truth. Presidio (Microsoft) is the leading first-pass tool combining regex and LLMs. Discussion of spaCy (traditional NER, good for an initial run), GLiNER for relationships/classification, AllenNLP as an older option, data-protection constraints on open-source models, and self-hosting small NLP models. Label Studio proposed for clinician annotation feeding back into Presidio reconfiguration. Laura confirms this matches what she had in mind.

![](screenshots/chapframe-07.png)
*The document's entity extraction and classification section, with a two-column implementation comparison.*

- Rowan: "the tool for doing the first run seems to be overwhelmingly a tool called Presidio ... it allows you to combine regex plus LLMs ... you can use it as a human in front, looking at your data."
- Laura: "spaCy is a very traditional approach for natural language tasks ... normally good for an initial run, or for quite simple cases."
- Laura: "we also have to be careful with the models that we use to make sure that they meet with protection of the data."

## 8. Reflecting on Kumulus's latest email
**25:12 to 27:24**

Rowan notes Kumulus took a step back in their recent email, stripping out the detailed architecture and committing to build the NICE pipeline plus the recommendation engine without evolved tooling detail. Deon reads it as them trying to get the high-level direction right first (Vanessa replied with bullet points). Laura agrees the module-structured document is useful and takes a homework action.

![](screenshots/frame-00009.png)
*Rowan's document showing a prose section followed by indented pseudocode.*

- Deon: "I think they're trying to get the high level thing right now, because they keep getting it wrong with us ... that's why their latest email, it was just Vanessa replying with bullet points."
- Laura: "I like the way that you structured and divided by modules ... perhaps I can just take it as homework and come back to you."

## 9. Build tiers and division of labour
**27:24 to 31:01**

Rowan introduces "build tiers" describing how novel or challenging each module is: commodity (off-the-shelf, configure only) versus must-prove/custom. The open question is whether Kumulus should build the hard custom modules (for example graph construction) or MedBrief should, given MedBrief has already started the graph work. The team aligns that Kumulus would do modules two to seven (not one, as they do not do OCR).

![](screenshots/frame-00012.png)
*The document's summary table listing modules with a status/owner column.*

- Rowan: "do we want to spend money on them just to configure a whole bunch of commodity things ... or do we want them to do genuinely hard things?"
- Deon: "Not one, Laura, because they don't do OCR." / Rowan: "Two to seven."

## 10. Refining the email response to Kumulus
**31:01 to 34:47**

The team decides to be more explicit in the reply since Vanessa is not technical: state clearly that Kumulus should do entity extraction and MedBrief will supply the entities to extract and classify. Rowan clarifies module two (NLP semantic processing, identifying named things) versus module three (entity extraction, classifying them). Laura notes rights and obligations come mainly from the NICE guidelines (M4), not the case. Agreement to include evaluation metrics in the email.

![](screenshots/chapframe-10.png)
*Participant video gallery: Rowan Reid, Laura Gongas, Deon Kuhn.*

- Laura: "I feel that Vanessa is not technical ... we can be more explicit. We want you to do entity extraction and we will provide you with the entities that we want to be extracted and classified."
- Laura: "from the case, how would you get the rights and obligations from the case? Wouldn't it be defined in the NICE guidelines?" / Rowan: "Yes. I suppose you're right."

## 11. Case selection for the proof of concept
**34:47 to 40:41**

Laura presents case 39945 (Brendan's case: two medications should have been co-prescribed, one was omitted, the patient died) and a similar candidate case (patient discharged without antibiotics, leading to death). Discussion of whether two similar cases risk overfitting. Laura argues starting narrow in one domain (for example gynaecology and obstetrics) is the right way to begin a complex-pipeline POC, then scale; Kumulus also asked for similar cases and wanted to limit the NICE guidelines ingested. Deon agrees to branch out after the proof of value. Brendan still needs to check the case and the NICE application form.

![](screenshots/chapframe-11.png)
*Participant video gallery.*

- Laura: "two medications had to be prescribed together. And then only one of them was prescribed ... which caused the patient to be deceased."
- Deon: "would we first try perfecting the system for this type of case ... or does that cause a risk of the system being, you would use a term like overfitting?"
- Laura: "it is a risk of overfitting, but when it's such a complex pipeline and you're doing a proof of concept, normally you start in a domain ... and then scale."

## 12. Rowan's next work and action assignments
**40:41 to 44:23**

Discussion of what Rowan works on next. Laura needs him to go deeper on Kumulus later but it is on her side for now. Deon assigns Rowan an independent exploratory research task on two existing tickets (granular storing of records, and date filtering), wanting Rowan's independent assessment to compare with his own. Laura mentions defining the company data strategy as a broader future item. Reference to Chantel's product walkthrough where Rowan asked strong questions.

![](screenshots/chapframe-12.png)
*Participant video gallery: Laura Gongas and Rowan Reid.*

- Deon: "I sent you two tickets a while back when you just started ... the granular storing of records. I want you to independently do research on the system as it currently is ... and just come up with ideas."
- Deon: "putting you in the deep end blindly with this ticket is actually a good exercise for you to apply that knowledge of your current understanding of the system."

## 13. Wrap-up
**44:23 to 44:39**

Laura asks for five minutes with Deon offline; Deon agrees to call her. He will resend Rowan the ticket. Closing goodbyes.

![](screenshots/frame-00014.png)
*Two-up participant gallery, end of call.*

- Laura: "I actually need five minutes from you, Dionne, but we can take it offline." / Deon: "I'll give you a call."
