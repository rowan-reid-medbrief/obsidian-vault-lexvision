# Graph views (Mermaid)

These render inline in Obsidian. For the full interactive graph open `graph.html`.

## Decisions

```mermaid
flowchart LR
  decision_0001["Use Medbrief's existing Document Intelligence OC"]
  decision_0002["Limit PoV to one medical domain to keep scope bo"]
  decision_0003["Medbrief is responsible for obtaining the NICE A"]
  decision_0004["Select the simplest case with the fewest NICE gu"]
  decision_0005["Databricks chosen over Microsoft Fabric for para"]
  decision_0006["Entity classification schema must be agreed with"]
  decision_0007["Azure AI Foundry models used for entity extracti"]
  decision_0008["Replace manual review with quantitative evaluati"]
  decision_0009["Medbrief can take full ownership at end of Miles"]
  decision_0010["Medbrief MLOps engineer to review and potentiall"]
  decision_0011["Data pipeline built for scale beyond 2-case PoV"]
  decision_0012["Kumulus to produce a revised zero-cost-to-client"]
  claim_0015 -->|SUPPORTS| decision_0012
  claim_0016 -->|SUPPORTS| decision_0012
  claim_0017 -->|SUPPORTS| decision_0012
  decision_0005 -->|BUILDS_ON| decision_0002
  claim_0010 -->|SUPPORTS| decision_0008
  claim_0009 -->|SUPPORTS| decision_0010
  claim_0013 -->|SUPPORTS| decision_0004
  decision_0006 -->|DEPENDS_ON| action_0004
  decision_0001 -->|DEPENDS_ON| claim_0006
  decision_0003 -->|DEPENDS_ON| claim_0002
  claim_0006 -->|SUPPORTS| decision_0001
  claim_0002 -->|SUPPORTS| decision_0003
  claim_0004 -->|SUPPORTS| decision_0004
  decision_0001 -->|RESOLVES| question_0004
  decision_0003 -->|RESOLVES| question_0005
  decision_0001 -->|BUILDS_ON| decision_0002
  claim_0008 -->|SUPPORTS| decision_0006
  claim_0009 -->|SUPPORTS| decision_0005
  decision_0008 -->|RESOLVES| question_0008
  action_0008 -->|DEPENDS_ON| decision_0005
  decision_0012 -->|RESOLVES| question_0010
  action_0009 -->|DEPENDS_ON| decision_0012
```

## Action items (dependency DAG)

```mermaid
flowchart TD
  action_0001["Medbrief to obtain NICE API key<br/>Medbrief"]
  action_0002["Verify NICE API historical guideline cov<br/>João (John) Marçura"]
  action_0003["Medbrief to identify sample cases with f<br/>Medbrief"]
  action_0004["Agree entity classification schema with <br/>João (John) Marçura"]
  action_0005["Define with Medbrief data science team w<br/>João (John) Marçura"]
  action_0006["Create ground truth labels for pseudonym<br/>Medbrief"]
  action_0007["Update success criteria to use quantitat<br/>João (John) Marçura"]
  action_0008["Medbrief MLOps engineer to review and ap<br/>Laura Gongas"]
  action_0009["Kumulus to deliver revised zero-cost pro<br/>João (John) Marçura"]
  topic_data-flow-architecture -->|DEPENDS_ON| action_0001
  topic_success-criteria -->|DEPENDS_ON| action_0001
  artifact_engagement-timeline-gantt -->|DEPENDS_ON| action_0001
  topic_guideline-version-selection -->|DEPENDS_ON| claim_0001
  decision_0006 -->|DEPENDS_ON| action_0004
  claim_0013 -->|DEPENDS_ON| claim_0012
  action_0002 -->|DEPENDS_ON| action_0001
  decision_0001 -->|DEPENDS_ON| claim_0006
  decision_0003 -->|DEPENDS_ON| claim_0002
  action_0001 -->|BLOCKS| topic_nice-api-access
  claim_0001 -->|BLOCKS| decision_0004
  action_0004 -->|DEPENDS_ON| action_0003
  topic_microsoft-funding -->|DEPENDS_ON| claim_0012
  action_0008 -->|DEPENDS_ON| decision_0005
  action_0009 -->|DEPENDS_ON| decision_0012
  action_0001 -->|DEPENDS_ON| action_0002
```

## Questions and answers

```mermaid
flowchart LR
  question_0001["Will the PoV cover multiple NICE guideli<br/>(OPEN)"]
  question_0002["What exactly is meant by deterministic p<br/>(OPEN)"]
  question_0003["Has NICE confirmed that the API provides<br/>(OPEN)"]
  question_0004["Will handwritten notes OCR'd by Medbrief<br/>(OPEN)"]
  question_0005["Is the NICE API connection in scope?<br/>(OPEN)"]
  question_0006["Is existing OCR on handwriting reusable <br/>(OPEN)"]
  question_0007["Which service or model performs entity e<br/>(OPEN)"]
  question_0008["How will pseudonymisation be evaluated, <br/>(OPEN)"]
  question_0009["What are the entity type and subtype cla<br/>(OPEN)"]
  question_0010["Did Medbrief expect full Microsoft spons<br/>(OPEN)"]
  action_0007 -->|RESOLVES| question_0008
  action_0009 -->|RESOLVES| question_0010
  person_laura-gongas -->|ASKED| question_0001
  person_laura-gongas -->|ASKED| question_0002
  person_steve-ashford -->|ASKED| question_0003
  person_laura-gongas -->|ASKED| question_0004
  person_laura-gongas -->|ASKED| question_0005
  person_joao-margura -->|ASKED| question_0006
  person_joao-margura -->|ANSWERED| question_0001
  person_joao-margura -->|ANSWERED| question_0005
  person_joao-margura -->|ANSWERED| question_0006
  person_steve-ashford -->|ANSWERED| question_0004
  person_joao-margura -->|ANSWERED| question_0003
  decision_0001 -->|RESOLVES| question_0004
  decision_0003 -->|RESOLVES| question_0005
  action_0001 -->|RESOLVES| question_0005
  action_0002 -->|RESOLVES| question_0003
  person_brendan-hughes -->|ASKED| question_0009
  person_brendan-hughes -->|ASKED| question_0007
  person_joao-margura -->|ANSWERED| question_0009
  person_joao-margura -->|ANSWERED| question_0007
  person_joao-margura -->|ANSWERED| question_0002
  person_laura-gongas -->|ASKED| question_0008
  person_joao-margura -->|ANSWERED| question_0008
  decision_0008 -->|RESOLVES| question_0008
  person_brendan-hughes -->|ASKED| question_0010
  decision_0012 -->|RESOLVES| question_0010
```

