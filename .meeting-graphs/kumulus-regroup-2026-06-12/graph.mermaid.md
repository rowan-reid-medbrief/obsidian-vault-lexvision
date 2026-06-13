# Graph views (Mermaid)

These render inline in Obsidian. For the full interactive graph open `graph.html`.

## Decisions

```mermaid
flowchart LR
  decision_0001["Use a two-layer raw/curated approach for the POC"]
  decision_0002["Reuse Azure Document Intelligence for OCR (alrea"]
  decision_0003["Treat Rowan's entity model as aspirational/broad"]
  decision_0004["Databricks over Microsoft Fabric for the data pl"]
  decision_0005["Neo4j as the team's graph database preference"]
  decision_0006["CQRS treated as optional for the proof of value "]
  decision_0007["Use Presidio for the first-pass pseudonymisation"]
  decision_0008["Cumulus to build modules two to seven (not modul"]
  decision_0009["Be more explicit in the email reply to Vanessa s"]
  decision_0010["MedBrief will supply the entities to extract and"]
  decision_0011["Include the evaluation metrics in the email repl"]
  decision_0012["Select case 39945 (Brendan's case) plus a simila"]
  decision_0013["Start narrow in one domain for the complex-pipel"]
  decision_0014["Branch out to other case types after the proof o"]
  decision_0015["Deon takes Rowan for the ticket research task (o"]
  claim_0002 -->|SUPPORTS| decision_0001
  claim_0011 -->|SUPPORTS| decision_0004
  claim_0012 -->|SUPPORTS| decision_0004
  claim_0015 -->|SUPPORTS| decision_0007
  claim_0021 -->|SUPPORTS| decision_0007
  claim_0014 -->|SUPPORTS| decision_0006
  claim_0007 -->|SUPPORTS| decision_0003
  claim_0026 -->|SUPPORTS| decision_0008
  claim_0029 -->|SUPPORTS| decision_0013
  claim_0028 -->|SUPPORTS| decision_0014
  claim_0030 -->|SUPPORTS| decision_0012
  claim_0031 -->|SUPPORTS| decision_0012
  claim_0003 -->|SUPPORTS| decision_0011
  decision_0008 -->|RESOLVES| question_0003
  decision_0013 -->|RESOLVES| question_0006
  decision_0014 -->|RESOLVES| question_0006
  decision_0015 -->|RESOLVES| question_0007
  decision_0007 -->|RESOLVES| question_0002
  action_0007 -->|DEPENDS_ON| decision_0012
  decision_0014 -->|BUILDS_ON| decision_0013
  decision_0010 -->|BUILDS_ON| decision_0009
```

## Action items (dependency DAG)

```mermaid
flowchart TD
  action_0001["Laura to review the per-module evaluatio<br/>"]
  action_0002["Laura to find the prior pseudonymisation<br/>"]
  action_0003["Laura to find the previously-defined pse<br/>"]
  action_0004["Laura to review the evaluation metrics a<br/>"]
  action_0005["Laura to review Rowan's document, draft <br/>"]
  action_0006["Laura to add a point in the email clarif<br/>"]
  action_0007["Laura to review Rowan's document, send t<br/>"]
  action_0008["Brendan to check the case and the NICE a<br/>"]
  action_0009["Rowan to do independent exploratory rese *<br/>"]
  action_0010["Deon to resend Rowan the ticket<br/>"]
  action_0011["Laura to take five minutes with Deon off<br/>"]
  action_0007 -->|DEPENDS_ON| action_0008
  action_0007 -->|DEPENDS_ON| decision_0012
  action_0009 -->|DEPENDS_ON| action_0010
```

## Questions and answers

```mermaid
flowchart LR
  question_0001["Should Laura review the evaluation metri<br/>(answered)"]
  question_0002["Laura: will Presidio also work for entit<br/>(answered)"]
  question_0003["Should Cumulus build the hard custom mod<br/>(OPEN)"]
  question_0004["Laura asks what is meant by NLP semantic<br/>(OPEN)"]
  question_0005["Do rights and obligations come from the <br/>(OPEN)"]
  question_0006["Should we perfect the system for one cas<br/>(OPEN)"]
  question_0007["What is Rowan working on next?<br/>(OPEN)"]
  person_laura-gongas -->|ASKED| question_0001
  person_rowan-reid -->|ANSWERED| question_0001
  person_laura-gongas -->|ASKED| question_0002
  person_rowan-reid -->|ANSWERED| question_0002
  person_rowan-reid -->|ASKED| question_0003
  person_laura-gongas -->|ASKED| question_0004
  person_rowan-reid -->|ANSWERED| question_0004
  person_laura-gongas -->|ASKED| question_0005
  person_rowan-reid -->|ANSWERED| question_0005
  person_deon-kuhn -->|ASKED| question_0006
  person_laura-gongas -->|ANSWERED| question_0006
  person_deon-kuhn -->|ASKED| question_0007
  person_rowan-reid -->|ANSWERED| question_0007
  decision_0008 -->|RESOLVES| question_0003
  decision_0013 -->|RESOLVES| question_0006
  decision_0014 -->|RESOLVES| question_0006
  decision_0015 -->|RESOLVES| question_0007
  action_0006 -->|RESOLVES| question_0004
  decision_0007 -->|RESOLVES| question_0002
  action_0001 -->|RESOLVES| question_0001
```

