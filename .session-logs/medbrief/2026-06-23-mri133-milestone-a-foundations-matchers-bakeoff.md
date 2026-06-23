---
date: 2026-06-23
project: annotations
domain: medbrief
tags: [mri-133, medbrief, programme, poc, python, harden-plan, decision-log]
repos:
  - annotations: f90cba3
  - config: docs/programmes/mri133-annotations-poc.md (ledger writeback a1/a2/a3)
  - vault: Decisions/2026-06-19-mri133-scope-and-stamp-first.md
model_check: fired-upgrade (model, dropped into the a1 gate at opus/high; a2 specced sonnet, stayed opus by choice mid-session)
parent: null
programme: mri133-annotations-poc (a1, a2, a3 shipped)
---

# MRI-133 POC: Milestone A built end to end (a1, a2, a3)

Shipped all three Milestone A programme sessions in one sitting: a1 (the ground-truth
harness, opened by a GO stamp-survival spike and anchored by a keystone oracle-faithfulness
test that re-derives the mapping from the mutated PDF bytes), a2 (the four cheap matchers
behind a shared interface, where only the identity signal licenses a confident clone call),
and a3 (scoring with honest separated metrics, conformal queue-sizing on a document-disjoint
fold, the pre-registered DoD bar, and the one-command two-table bake-off). 91 tests green.
The headline on synthetic data is content-arm POOR (ensemble precision 71%/44%) reading
"stamp-at-extraction is the only safe path", with the stamped arm at 97-100% recall as the
if-stamped projection: the stamp-first thesis, in numbers. a1's draft was hardened with an
8-agent /harden-plan fan-out before building; the 19-Jun scoping + stamp-first reframe was
decision-logged to the vault. Milestone B (b1/b2) is blocked on the Apryse trial key.
