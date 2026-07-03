---
tags: [mri-133, medbrief, annotations, content-arm, split-detection, session-log]
repos:
  - annotations @ feat/coverage-graph-reframe (docs/IDEAS.md committed)
model_check: not-needed
---

# MRI-133: content-arm viability review + cross-section split gap

Advisory session after Wednesday's Deon demo. Reviewed what shipped since the demo (real-corpus testing, zero silent errors, split detection, the stamp-survival finding, the coverage-graph reframe) and assessed whether the content arm WITHOUT stamping is now a credible primary solution. Verdict: yes - zero silent errors on the real corpus, adjacent splits resolve or safely queue, and stamping can't cover the existing back-catalogue anyway (an in-PDF stamp doesn't survive the merge, and stamping only ever helps documents processed after deploy).

Surfaced a genuine open gap: cross-section (non-adjacent) split confident resolution. The adjacency guard (`split_require_adjacent`) only auto-places contiguous split children, so a real "scatter re-sort" that files a split page's halves into different clinical sections is safely QUEUED, not resolved. Both our real split cases (salli 31+32, bench 141+142) were adjacent, so this is untested; the fix direction is the adjacency-free geometric shape-fit channel and/or clinical-section awareness.

Logged 3 ideas to docs/IDEAS.md ([high] cross-section resolution, [high] its test fixture, [med] full-scale validation on the 1,000+ page docs - the 1,344pp trust doc is currently `--cap-pages`-truncated). Updated the cardinality-channels memory so the gap isn't dismissed as "splits are done".
