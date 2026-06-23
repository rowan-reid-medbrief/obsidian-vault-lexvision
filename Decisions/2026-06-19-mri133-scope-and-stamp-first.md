---
title: "Decision: MRI-133 POC scope + stamp-first identity"
type: decision
domain: medbrief
status: active
created: "2026-06-23"
modified: "2026-06-23"
tags: [decision, medbrief, mri-133]
source: manual
references: ["[[Annotations]]"]
supersedes: []
superseded_by: []
---

# Decision: MRI-133 POC scope + stamp-first identity

## Decision

Two linked choices for the MRI-133 annotations/redactions relocation proof of concept:

1. **Scope (from the Fri 19 Jun 2026 meeting with Deon Kuhn and Chantel van Wyk).**
   Target page-less documents (client uploads, unitised and raw extracted records),
   where roughly 100% of live annotations sit. Build a standalone throwaway Python POC
   outside the PHP/MySQL monolith. Prove a forward capability (a redaction surviving a
   re-sort), not today's exact behaviour (annotations currently orphan on re-export
   rather than sliding within a document).

2. **Stamp-first identity (decided during planning, hardened 2026-06-23).** Stamp a
   durable per-page identity at the point MedBrief controls ingestion (a page-dictionary
   key plus a content-hash, with a sidecar manifest and DB lineage; not invisible
   watermarks, which 2024 research shows are not robust enough for redaction-grade
   identity). Re-identification then becomes a deterministic lookup; content-matching is
   the fallback for opaque externally-reordered documents and for split/clone children
   without lineage. Confirmed identity is also what unlocks safe per-document
   auto-redaction. Both arms (stamped + content) are wanted, reported as two tables that
   answer different questions, never row against row.

## Rationale

No product relocates annotations across page changes, and PHI rules force self-hosting,
so build (not buy) is unavoidable. The page-less population is where the annotations
actually live, so that is where the POC must prove reliability. Framing it as a forward
capability keeps the POC honest: it is what redaction launch needs, not a reproduction
of a bug. Stamp-first is the leverage: detecting what moved is hard and lossy, but
stamping a durable id where ingestion is controlled turns most of the problem into a
lookup, and a confirmed identity is the precondition for burning a redaction safely per
document. The a1 stamp-survival spike (2026-06-23) returned GO: a page-dictionary key
survives a save + repaginate under both the pikepdf and pymupdf backends, so the stamped
arm has a save-stable home.

## Open fork (for Deon)

Stamp at extraction versus at sort-prep. Stamping reaches the annotated population (on
page-less raw records that never pass sort-prep) only if done at the earliest controlled
point. Recommendation: stamp at extraction. Until resolved, the content-matching arm
carries the as-is annotated population.

## References

- [[Annotations]]: the MRI-133 hub note (status, strategic framing). Working detail and
  the hardened plan live in the coupled project at `~/claude_code/projects/annotations`
  (programme spine `mri133-annotations-poc`).

## Downstream impact

- Sets the build direction for the `mri133-annotations-poc` programme (Milestones A and B).
- Defers the extraction-vs-sort-prep stamping decision to Deon; it gates how much the
  content-matching arm must carry.
- The standalone-Python-POC choice keeps the monolith untouched in v1; the production
  stack recommendation (likely Node.js + Apryse plus a Python ML service) is a separate,
  later call.
