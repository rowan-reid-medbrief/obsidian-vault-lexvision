---
tags: [medbrief, mri-133, data-architecture, divergent-ideation, plan-mode]
repos: [medbrief-onboarding, ~/.claude, ObsidianVault]
model_check: fired-upgrade (effort)
---

# MRI-133 divergent architecture ideation

Divergent, premise-dissolving ideation on MRI-133, following the notes/14 research that went to Dion. Ran three independent design explorations from borrowed paradigms (event-sourced / Git-for-matters, property-graph, and stand-off / transclusion), which all converged on the same kernel: a reference names stable content, position lives in a separate placement table, and a re-sort writes only placements and never touches anchors (the current retrofit done right). Rowan caught a flawed reframe of mine, where I read "every annotated document is page-less" as "never sorted"; a code trace against the MSR source overturned it, since page-less is the universal by-design state of every reviewable Document (Page attaches to BatchDocument only), so it is not evidence of sorting. Wrote notes/15 (the three architectures, the convergent kernel, wilder provocations, and the product fork on where annotation should live), added a correction addendum to notes/14 §11, and updated docs/SOURCES.md; effort was raised to max for the ideation. Open and DB-checkable: the re-export lifecycle, and whether sorted output is annotated in the intended workflow; the divergent options plus the product fork still go to Dion.
