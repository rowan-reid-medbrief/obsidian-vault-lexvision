---
name: mri133-content-arm-primary-goal
description: "Making the content-only arm as strong as possible is a PRIMARY project goal (Rowan, 2026-07-03); prefer RESOLVING hard cardinality cases in the content arm over safe-queueing and leaning on the stamped-id arm."
metadata: 
  node_type: memory
  type: project
  originSessionId: 1f4a79f3-1020-4ce7-ab15-94bbb922a4f5
---

Rowan (2026-07-03): "One of my primary goals in this project is to make the Content arm only as strong as possible." Said when choosing to RESOLVE the bench-115132 split-vs-twin silent error inside the content arm (approach A) rather than safe-queue it and rely on the stamped-id arm (approach B), even though the stamped-id arm already resolves that twin safely.

**Why:** the durable-id (stamped `Page.id`) arm is the primary architecture, but it only works where a durable id exists. The content-only arm is the fallback for legacy / un-stamped / id-stripped pages, and its ceiling determines coverage on real bundles that lack ids. So "the stamp arm already covers it" is NOT an acceptable resolution for a content-arm gap; the content arm has to earn the resolution itself.

**How to apply:** when a hard cardinality case (split / clone / removed) is resolvable by the stamped-id arm but silent or queued in the content arm, do NOT treat "the stamp arm covers it" as done. Push the content arm to resolve it, accepting a measured precision cost guarded by the bake-off silent-error metric, and fall back to safe-queue only when page-local evidence genuinely cannot separate the cases (e.g. gp's pure-white blank child). Weight content-arm strength above minimal-risk safe-queueing in design trade-offs. Related: [[mri133-cardinality-channels]], [[mri133-content-arm-scoped-to-originals]].
