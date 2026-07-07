---
type: wrap-up
tags: [mri-133, annotations, content-arm, matcher, split, harden-plan, whats-next, medbrief]
repos:
  - annotations: 8d824ba
parent: 2026-07-05-mri133-median-rescue-hybrid-shipped.md
model_check: switched sonnet -> opus/xhigh for the plan + harden work
---

# MRI-133: cross-section split plan drafted and hardened

Groomed the annotations backlog (/whats-next), then drafted and hardened (/harden-plan, 8 critics + pre-mortem) the plan for the paired `[high]` cross-section (scatter) split-resolution items. The hardening refuted the draft's core premise (page-local geometry is not "strictly stronger" than mutated-index adjacency on assembled/boilerplate pages), and Rowan chose to build it properly: an upgrade-only rescue plus a per-band decisiveness gate that replaces the global consistency adjacency was cheaply providing. Plan committed (`8d824ba`); no code built yet (Phase 1 is fixtures-first).
