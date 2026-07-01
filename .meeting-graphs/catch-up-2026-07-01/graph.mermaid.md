# Graph views (Mermaid)

These render inline in Obsidian. For the full interactive graph open `graph.html`.

## Decisions

```mermaid
flowchart LR
  decision_0001["decision:0001"]
  decision_0002["decision:0002"]
  decision_0003["Implement redaction inside DocSorter at the sort"]
  decision_0003 -->|RESOLVES| question_0005
  claim_0020 -->|SUPPORTS| decision_0001
  claim_0028 -->|SUPPORTS| decision_0002
  claim_0019 -->|SUPPORTS| decision_0003
```

## Action items (dependency DAG)

```mermaid
flowchart TD
  action_0001["action:0001<br/>Deon Kuhn"]
  action_0002["action:0002<br/>"]
  action_0003["action:0003<br/>Deon Kuhn"]
  action_0004["Research date-range filtered PDF renderi *<br/>Rowan Reid"]
  action_0002 -->|DEPENDS_ON| action_0003
```

## Questions and answers

```mermaid
flowchart LR
  question_0001["Is that when you discovered it?<br/>(answered)"]
  question_0002["question:0002<br/>(answered)"]
  question_0003["question:0003<br/>(answered)"]
  question_0004["question:0004<br/>(answered)"]
  question_0005["Will solicitors still be able to redact <br/>(answered)"]
  question_0006["Can we stop recording?<br/>(OPEN)"]
  person_rowan-reid -->|ASKED| question_0001
  person_deon-kuhn -->|ANSWERED| question_0001
  person_rowan-reid -->|ASKED| question_0002
  person_deon-kuhn -->|ASKED| question_0003
  person_rowan-reid -->|ANSWERED| question_0003
  person_deon-kuhn -->|ASKED| question_0004
  person_rowan-reid -->|ANSWERED| question_0004
  person_rowan-reid -->|ASKED| question_0005
  person_deon-kuhn -->|ANSWERED| question_0005
  person_deon-kuhn -->|ASKED| question_0006
  decision_0003 -->|RESOLVES| question_0005
```

