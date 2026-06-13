# Graph views (Mermaid)

These render inline in Obsidian. For the full interactive graph open `graph.html`.

## Decisions

```mermaid
flowchart LR
  decision_0001["Expert Match storage endpoint integration to be "]
  decision_0002["Send full expert profile (all fields) to AI inge"]
  decision_0003["Ground truth annotation cases should be deceased"]
  decision_0004["Cumulus scope reduced to green box: data ingesti"]
  decision_0005["NICE API key may be shared with Cumulus temporar"]
  decision_0006["Rowan's focus to be on Cumulus data engineering "]
  decision_0007["Thumbs up/down tickets remain with Deon's side; "]
  decision_gf0015["Explicit priority order: ground truth collection"]
  decision_0006 -->|RESOLVES| question_0001
  claim_0001 -->|SUPPORTS| decision_0006
  claim_0003 -->|SUPPORTS| decision_0005
  claim_0002 -->|SUPPORTS| decision_0005
  decision_0005 -->|RESOLVES| question_0004
  claim_0004 -->|SUPPORTS| decision_0005
  decision_0007 -->|RESOLVES| question_0007
  claim_0004 -->|SUPPORTS| decision_0003
  decision_0002 -->|RESOLVES| question_0005
  claim_0003 -->|SUPPORTS| decision_0006
  decision_0005 -->|BUILDS_ON| decision_0006
  claim_0009 -->|SUPPORTS| decision_0005
```

## Action items (dependency DAG)

```mermaid
flowchart TD
  action_0001["Rowan to investigate Expert Match update *<br/>"]
  action_0002["Laura to send Cumulus meeting recording <br/>"]
  action_0003["Rowan to join tomorrow's meeting with Br *<br/>"]
  action_0004["Laura to fill in NICE API access applica<br/>"]
  action_0005["Team to clarify with Cumulus their inten<br/>"]
  action_0006["Investigate NICE API compliance requirem<br/>"]
  action_0007["If Cumulus does not handle NICE guidelin<br/>"]
  action_0008["Rowan to review Cumulus data architectur *<br/>"]
  action_0009["Laura to invite Rowan to the enterprise <br/>"]
  action_0010["Laura to forward the Cumulus architectur<br/>"]
  action_0011["Deon to take on Expert Match ingestion e<br/>"]
  action_0012["Rowan to watch the hackathon meeting rec *<br/>"]
  action_0013["Rowan to take script for Chantel Pilla *<br/>"]
  action_0014["Deon to send instance numbers to Brendan<br/>"]
  action_0015["Deon to consider asking Chantel to bump <br/>"]
  action_gf0008["Deon to investigate anomalous expert pro<br/>"]
  action_0012 -->|DEPENDS_ON| action_0002
  action_0008 -->|DEPENDS_ON| action_0010
  topic_rules-representation -->|DEPENDS_ON| topic_entity-extraction
  action_0002 -->|DEPENDS_ON| action_0003
  action_0010 -->|DEPENDS_ON| action_0011
```

## Questions and answers

```mermaid
flowchart LR
  question_0001["Should Expert Match endpoint integration<br/>(OPEN)"]
  question_0002["What annotation tool should be used for <br/>(OPEN)"]
  question_0003["How does Mediha's graph database work fi<br/>(OPEN)"]
  question_0004["Is it compliant to share the NICE API ke<br/>(OPEN)"]
  question_0005["Should Medbrief do NICE guideline extrac<br/>(OPEN)"]
  question_0006["Is there any additional Cumulus material<br/>(OPEN)"]
  question_0007["Should the human-in-the-loop / thumbs up<br/>(OPEN)"]
  decision_0006 -->|RESOLVES| question_0001
  action_0003 -->|RESOLVES| question_0003
  decision_0005 -->|RESOLVES| question_0004
  action_0005 -->|RESOLVES| question_0005
  action_0010 -->|RESOLVES| question_0006
  decision_0007 -->|RESOLVES| question_0007
  person_laura-gongas -->|ASKED| question_0001
  person_laura-gongas -->|ASKED| question_0002
  person_laura-gongas -->|ASKED| question_0003
  person_laura-gongas -->|ASKED| question_0004
  action_0002 -->|RESOLVES| question_0002
  decision_0002 -->|RESOLVES| question_0005
  person_laura-gongas -->|ASKED| question_0005
  person_deon-kuhn -->|ANSWERED| question_0005
```

