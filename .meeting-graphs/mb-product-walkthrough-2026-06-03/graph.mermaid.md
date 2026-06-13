# Graph views (Mermaid)

These render inline in Obsidian. For the full interactive graph open `graph.html`.

## Decisions

```mermaid
flowchart LR
  decision_0001["Matter creation wizard is now the standard route"]
  decision_0002["Schedule a follow-up session (likely two hours) "]
  decision_0003["Chantel to grant Rowan production UI access"]
  decision_0003 -->|RESOLVES| question_0012
  claim_0006 -->|SUPPORTS| decision_0001
  action_0008 -->|DEPENDS_ON| decision_0002
```

## Action items (dependency DAG)

```mermaid
flowchart TD
  action_0001["Chantel to send Rowan the wizard flow/su<br/>Chantel van Wyk"]
  action_0002["Improve the services page UX in the matt<br/>Chantel van Wyk"]
  action_0003["Fix 'area' vs 'client' label inconsisten<br/>"]
  action_0004["Chantel to share the MSR Products Conflu<br/>Chantel van Wyk"]
  action_0005["Chantel to walk Rowan through disclosure<br/>Chantel van Wyk"]
  action_0006["Chantel to grant Rowan production UI acc<br/>Chantel van Wyk"]
  action_0007["Rowan to explore the Grace Clayton dev m<br/>Rowan Reid"]
  action_0008["Rowan to find and block time for the fol *<br/>Rowan Reid"]
  action_0009["Rowan to send Chantel status of the proc *<br/>Rowan Reid"]
  action_0008 -->|DEPENDS_ON| decision_0002
  action_0007 -->|DEPENDS_ON| action_0006
```

## Questions and answers

```mermaid
flowchart LR
  question_0001["Is the wizard flow document mapping out <br/>(answered)"]
  question_0002["Is the 'area' autocomplete dropdown a li<br/>(answered)"]
  question_0003["Does MedBrief perform early case assessm<br/>(answered)"]
  question_0004["Does the last wizard question (schedule <br/>(answered)"]
  question_0005["Are chronology and schedule of radiology<br/>(answered)"]
  question_0006["Would someone always know whether liabil<br/>(answered)"]
  question_0007["Is the Form of Authority the form submit<br/>(answered)"]
  question_0008["Is the matter dashboard where the admini<br/>(answered)"]
  question_0009["Do administrators use SAFE reports to de<br/>(answered)"]
  question_0010["Is the Sally system what gets invoked fo<br/>(answered)"]
  question_0011["Has Rowan seen the records page previous<br/>(answered)"]
  question_0012["Does Rowan have a production user accoun<br/>(answered)"]
  question_0013["Users tab flow: can the administrator ad<br/>(answered)"]
  action_0001 -->|RESOLVES| question_0001
  action_0003 -->|RESOLVES| question_0002
  claim_0018 -->|RESOLVES| question_0003
  claim_0019 -->|RESOLVES| question_0004
  claim_0049 -->|RESOLVES| question_0005
  claim_0034 -->|RESOLVES| question_0006
  claim_0036 -->|RESOLVES| question_0007
  claim_0056 -->|RESOLVES| question_0008
  claim_0063 -->|RESOLVES| question_0010
  decision_0003 -->|RESOLVES| question_0012
  claim_0074 -->|RESOLVES| question_0013
  person_rowan-reid -->|ASKED| question_0001
  person_rowan-reid -->|ASKED| question_0002
  person_rowan-reid -->|ASKED| question_0003
  person_rowan-reid -->|ASKED| question_0004
  person_rowan-reid -->|ASKED| question_0005
  person_chantel-van-wyk -->|ANSWERED| question_0001
  person_chantel-van-wyk -->|ANSWERED| question_0002
  person_chantel-van-wyk -->|ANSWERED| question_0003
  person_chantel-van-wyk -->|ANSWERED| question_0004
  person_chantel-van-wyk -->|ANSWERED| question_0005
  person_rowan-reid -->|ASKED| question_0006
  person_chantel-van-wyk -->|ANSWERED| question_0006
  person_rowan-reid -->|ASKED| question_0007
  person_chantel-van-wyk -->|ANSWERED| question_0007
  person_rowan-reid -->|ASKED| question_0008
  person_chantel-van-wyk -->|ASKED| question_0009
  person_rowan-reid -->|ASKED| question_0010
  person_chantel-van-wyk -->|ASKED| question_0011
  person_chantel-van-wyk -->|ASKED| question_0012
  person_rowan-reid -->|ASKED| question_0013
  person_chantel-van-wyk -->|ANSWERED| question_0008
  person_chantel-van-wyk -->|ANSWERED| question_0009
  person_chantel-van-wyk -->|ANSWERED| question_0010
  person_rowan-reid -->|ANSWERED| question_0011
  person_rowan-reid -->|ANSWERED| question_0012
  person_chantel-van-wyk -->|ANSWERED| question_0013
```

