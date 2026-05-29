---
name: feedback-commenting-style-expert-sheet
description: "This project requires heavy commenting in scripts — narrate the research journey, attribute reference scripts, explain decisions about utils"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: fb2380d4-84e8-4a15-8928-cf88d544cd81
---

For the expert-sheet-data-processing project, scripts must be heavily commented. This is an explicit override of the default no-comment rule.

**Why:** The scripts are meant to be readable by a reviewer who wants to understand the journey taken to arrive at each decision. Comments should narrate: what research led to this approach, which reference scripts were drawn from (and where), why a particular utility from Laura's common_utils library was or wasn't used, and what DB exploration or other investigation underpinned a design choice.

**How to apply:**
- Add a file-level header comment summarising the context and research basis for the script
- At each significant code section, explain WHY it works the way it does — not just what it does
- When lifting a pattern from a reference script (`gemini_file.py`, `production_main.py`, etc.), note it explicitly: "Pattern lifted from reference_scripts/gemini_file.py — see [context]"
- When using a common_utils function, note why that function was chosen; when NOT using one, note why it was deemed unsuitable
- When a DB query or signal was chosen based on schema exploration, note the exploration that led to it (e.g., "userinternal table found during schema exploration — 4 regex patterns for @medbrief.* domains")

Also applies to: adaptability notes — flag where constants, category strings, or thresholds should be revisited after re-watching the recording or consulting Chantel/Laura.
