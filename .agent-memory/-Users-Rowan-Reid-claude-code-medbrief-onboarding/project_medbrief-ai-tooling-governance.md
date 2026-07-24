---
name: medbrief-ai-tooling-governance
description: "MedBrief's AI Tools Policy + live GitHub Copilot vs Claude Enterprise board decision: what's approved and what data is cleared for which tool"
metadata:
  node_type: memory
  type: project
  originSessionId: b59a8cbe-ae88-4779-bf13-359e6fb426bd
  modified: 2026-07-24T14:00:12.137Z
---

MedBrief has a real, actively-revised Acceptable Use of AI Tools Policy (governance
portal, v1.6 as of 22/04/2026) plus a live June 2026 Board decision paper on which AI
tool to use. Full detail with citations: `notes/16-governance-policies.md` (index),
`notes/17-ai-on-customer-data-synthesis.md` (the policy synthesis), and
`notes/18-confluence-ai-data-guidance.md` (Confluence research: the Board paper, ISF
minutes, 2024 tool research).

Core facts:
- Customer data is classified "Restricted" and cannot go into any AI tool (Copilot
  included) without case-by-case authorisation and risk assessment. Health/patient
  data is stricter still: prohibited without a written Compliance exemption. Tool
  approval (which platform) and data approval (what may go into it) are separate
  gates; only the first has confirmed evidence of being cleared.
- GitHub Copilot is the company-standard AI dev platform (Board paper, June 2026);
  Claude Enterprise + Claude Code CLI is a governed, pilot-phase exception for
  specialist work only (senior/lead engineers, architecture review, migration,
  refactoring, tech debt). Explicitly NOT approved: Claude Pro/Max, personal
  Claude/OpenAI/Gemini accounts, unmanaged Claude Code CLI, Claude Cowork.
- Model/tool standardisation for dev AI use was still under active ISF evaluation as
  of 8 June 2026 (not settled).
- Key human contacts for governance/compliance questions: Adam Stead (CEO, Data
  Protection Officer), Chris Fuller (IT, Compliance and Business Success), Zac Dreyer
  (Senior Software Developer and SecOps, drives AI/dev-tooling evaluation).

**Why:** Rowan asked directly whether GitHub Copilot is approved and what customer
data may go into it; the governance portal alone didn't have a live, tool-specific
answer, so Confluence research filled the gap.

**How to apply:** start from `notes/16-18` for any future MedBrief AI-tooling or
data-classification question in this project rather than re-extracting; the
governance portal and this Confluence research are both already mined.
