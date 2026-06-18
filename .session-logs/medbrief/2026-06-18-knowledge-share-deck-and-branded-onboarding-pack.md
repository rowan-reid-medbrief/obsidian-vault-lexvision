---
tags: [medbrief, onboarding, medbrief-brand, harden-plan, presentation, docx, pptx]
repos:
  - medbrief-onboarding
model_check: not-needed
---

# Knowledge-share deck and branded onboarding pack

Built a 14-slide MedBrief-branded knowledge-share deck on how Rowan onboarded himself at MedBrief with Claude Code (the sources, the CLAUDE.md instructions, the MCP fetch, the spec->branded-output pipeline), hardened from a ~23-slide draft via a four-critic /harden-plan fan-out: cut to fit a 30-minute slot, added two verbatim "show don't tell" slides (a real CLAUDE.md snippet and a real prompt+response), plus a confidentiality scrub and a per-slide overflow budget. Then rendered the existing onboarding-pack-v1.md synthesis into a 46-page branded Word doc (Contents page, per-section page breaks, navigation bookmarks), post-processing the generated spec to bold inline-code identifiers and drop literal `---` thematic breaks. Both deliverables built via the medbrief-brand skill, scrubbed of secrets, and committed under output/.
