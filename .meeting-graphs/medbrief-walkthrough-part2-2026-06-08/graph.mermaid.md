# Graph views (Mermaid)

These render inline in Obsidian. For the full interactive graph open `graph.html`.

## Decisions

```mermaid
flowchart LR
  decision_0001["Private Folders root folder to be renamed (to 'W"]
  decision_0002["Folders in Case Documentation to be grouped by u"]
  decision_0003["MedBrief Insights panel will not go live until t"]
  decision_0004["Use bookmarks (or VLM heading fallback) instead "]
  decision_0005["Launch CER index on Epic only first, extend to o"]
  decision_0006["Key events not included in MVP; chronology wizar"]
  decision_0007["MedBrief Match markup fee not yet finalised; con"]
  decision_0008["Apply MedBrief Match purple colour palette to Me"]
  decision_0009["Display total similar-case count across all Matc"]
  decision_0010["Letter of Approach PDF delivered encrypted via p"]
  decision_0011["T&Cs required from expert for any response (acce"]
  decision_0012["Expert 'instructed' status inferred from invitat"]
  decision_0013["Expert agency notification discontinued — MedBri"]
  claim_0020 -->|SUPPORTS| decision_0004
  claim_0026 -->|SUPPORTS| decision_0005
  claim_0030 -->|SUPPORTS| decision_0006
  claim_0034 -->|SUPPORTS| decision_0006
  claim_0059 -->|SUPPORTS| decision_0007
  claim_0060 -->|SUPPORTS| decision_0007
  claim_0065 -->|SUPPORTS| decision_0011
  claim_0009 -->|SUPPORTS| decision_0004
  action_0009 -->|DEPENDS_ON| decision_0006
  action_0016 -->|DEPENDS_ON| decision_0012
  decision_0005 -->|BUILDS_ON| decision_0004
```

## Action items (dependency DAG)

```mermaid
flowchart TD
  action_0001["Implement single-upload flow so client r<br/>"]
  action_0002["Follow up on suppressed-invitation notif<br/>Chantel van Wyk"]
  action_0003["Dion to speak to Rowan about the granula<br/>"]
  action_0004["Implement granular annotation/redaction <br/>"]
  action_0005["Fix MedBrief Insights font size (noted a<br/>"]
  action_0006["AI team to pursue a generalised date-ext<br/>"]
  action_0007["Dion to extend date filter to apply with<br/>Dion"]
  action_0008["Dion (or possibly Rowan) to implement in<br/>Dion"]
  action_0009["Build chronology wizard as prerequisite <br/>"]
  action_0010["Finalise MedBrief Match markup fee (8.5%<br/>"]
  action_0011["Apply MedBrief Match purple colour palet<br/>"]
  action_0012["Update MedBrief Match to display total s<br/>"]
  action_0013["Add client-specific letter of approach t<br/>"]
  action_0014["Implement AI component to auto-replace c<br/>"]
  action_0015["Implement automatic email-reply ingestio<br/>"]
  action_0016["Build in-platform letter of instruction <br/>"]
  action_0017["Add 'Invite this expert' button directly<br/>"]
  action_0018["Implement expert upload document-type pr<br/>"]
  action_0019["Build automated billing service request <br/>"]
  action_0020["Add MedBrief Match logo marker to contac<br/>"]
  action_0021["Chantel to send Rowan the useful lookup <br/>Chantel van Wyk"]
  action_0009 -->|DEPENDS_ON| decision_0006
  action_0007 -->|DEPENDS_ON| action_0006
  action_0019 -->|DEPENDS_ON| action_0016
  action_0016 -->|DEPENDS_ON| decision_0012
  action_0004 -->|BLOCKS| decision_0003
  action_0008 -->|BLOCKS| action_0007
```

## Questions and answers

```mermaid
flowchart LR
  question_0001["Do the folders Rowan sees as MedBrief ad<br/>(answered)"]
  question_0002["Was the chat interface built from a libr<br/>(answered)"]
  question_0003["Is the whole MedBrief Insights panel not<br/>(answered)"]
  question_0004["Does the CER index extract headings or b<br/>(answered)"]
  question_0005["Does the keyword search look through the<br/>(answered)"]
  question_0006["Does the patient section header carry a <br/>(answered)"]
  question_0007["What sections appear in a CER beyond the<br/>(answered)"]
  question_0008["For sections with dates embedded in cont<br/>(answered)"]
  question_0009["Does the CER structure (heading format) <br/>(answered)"]
  question_0010["What is the purpose of key events and wh<br/>(answered)"]
  question_0011["Who creates the Figma designs for MedBri<br/>(answered)"]
  question_0012["Does the ECA progress indicator track wh<br/>(answered)"]
  question_0013["Why did MedBrief move from Orthanc to Me<br/>(answered)"]
  question_0014["How do clients find experts without MedB<br/>(answered)"]
  question_0015["Does MedBrief Match show similar-case re<br/>(answered)"]
  question_0016["Could matters without sufficient info st<br/>(answered)"]
  question_0017["Is the entire search-to-response process<br/>(answered)"]
  question_0018["Is the letter of instruction also create<br/>(answered)"]
  question_0019["How does a disclosure get to the recipie<br/>(answered)"]
  claim_0015 -->|RESOLVES| question_0002
  claim_0016 -->|RESOLVES| question_0003
  claim_0019 -->|RESOLVES| question_0004
  claim_0022 -->|RESOLVES| question_0005
  claim_0023 -->|RESOLVES| question_0006
  claim_0024 -->|RESOLVES| question_0007
  claim_0025 -->|RESOLVES| question_0008
  claim_0026 -->|RESOLVES| question_0009
  claim_0033 -->|RESOLVES| question_0010
  claim_0041 -->|RESOLVES| question_0013
  claim_0048 -->|RESOLVES| question_0014
  claim_0051 -->|RESOLVES| question_0015
  claim_0057 -->|RESOLVES| question_0016
  claim_0062 -->|RESOLVES| question_0017
  claim_0068 -->|RESOLVES| question_0018
  claim_0067 -->|RESOLVES| question_0019
  person_rowan-reid -->|ASKED| question_0002
  person_rowan-reid -->|ASKED| question_0003
  person_chantel-van-wyk -->|ANSWERED| question_0002
  person_chantel-van-wyk -->|ANSWERED| question_0003
  person_rowan-reid -->|ASKED| question_0004
  person_rowan-reid -->|ASKED| question_0005
  person_rowan-reid -->|ASKED| question_0006
  person_rowan-reid -->|ASKED| question_0007
  person_rowan-reid -->|ASKED| question_0008
  person_rowan-reid -->|ASKED| question_0009
  person_rowan-reid -->|ASKED| question_0010
  person_rowan-reid -->|ASKED| question_0011
  person_chantel-van-wyk -->|ANSWERED| question_0004
  person_chantel-van-wyk -->|ANSWERED| question_0005
  person_chantel-van-wyk -->|ANSWERED| question_0006
  person_chantel-van-wyk -->|ANSWERED| question_0007
  person_chantel-van-wyk -->|ANSWERED| question_0008
  person_chantel-van-wyk -->|ANSWERED| question_0009
  person_chantel-van-wyk -->|ANSWERED| question_0010
  person_chantel-van-wyk -->|ANSWERED| question_0011
  person_rowan-reid -->|ASKED| question_0012
  person_rowan-reid -->|ASKED| question_0013
  person_rowan-reid -->|ASKED| question_0014
  person_chantel-van-wyk -->|ANSWERED| question_0012
  person_chantel-van-wyk -->|ANSWERED| question_0013
  person_chantel-van-wyk -->|ANSWERED| question_0014
  person_rowan-reid -->|ASKED| question_0016
  person_rowan-reid -->|ASKED| question_0017
  person_rowan-reid -->|ASKED| question_0018
  person_chantel-van-wyk -->|ANSWERED| question_0016
  person_chantel-van-wyk -->|ANSWERED| question_0017
  person_chantel-van-wyk -->|ANSWERED| question_0018
  person_rowan-reid -->|ASKED| question_0019
  person_chantel-van-wyk -->|ANSWERED| question_0019
```

