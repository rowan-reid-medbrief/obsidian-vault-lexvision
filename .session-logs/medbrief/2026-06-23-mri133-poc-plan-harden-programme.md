---
date: 2026-06-23
tags: [mri-133, medbrief, poc, annotations, redactions, programme, harden-plan, planning, research]
repos:
  - .claude
  - ObsidianVault
model_check: not-needed
parent: null
---

# MRI-133 annotations/redactions POC: research, plan, harden, promote to programme

Took Deon's MRI-133 PoC brief (keep annotations and redactions correctly placed when page-less PDFs are re-sorted) from a one-line ask to a hardened, tracked programme. Reopened the initial Python+Apryse assumption with three deep-research streams (build-vs-buy, platform/language, SOTA matching), landing on a stamp-first design with a content-matching fallback, a per-document redaction-safety posture (burn only on confirmed identity, else over-mask or abstain), and conformal review-queue sizing; ran a 13-lens /harden-plan pass that re-grounded the redaction "guarantee" and fixed three more must-fixes. Promoted to the `mri133-annotations-poc` /programme spine: 5 build sessions (a1-a3 Milestone A, the no-Apryse matching bake-off; b1-b2 Milestone B, the Apryse application + visual) plus 2 deferred (real-data validation, WebViewer demo). Next: `/programme next` launches a1 (opening with the stamp-survival go/no-go spike); Rowan owes the Apryse trial key, a few de-identified real scan pairs, and the stamp-at-extraction question to Deon.
