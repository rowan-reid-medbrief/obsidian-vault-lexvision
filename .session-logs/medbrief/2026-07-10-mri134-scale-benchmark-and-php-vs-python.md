---
type: handoff
date: 2026-07-10
domain: medbrief
project: medbrief-work
ticket: MRI-134
parent: 2026-07-10-medbrief-work-docs-reorg-and-vault-alignment.md
tags: [medbrief, mri-134, benchmark, pdfnet, performance]
---

# MRI-134 scale benchmark, check-order fix, and PHP-vs-Python

Benchmarked the page-subset pipeline for Deon (where does the limit lie, is it pages or file size), fixed a check-order bug, then answered Deon's Python follow-up. The standalone-PHP control (Rowan's idea) overturned the conclusion: the real cost is a ~19x overhead inside the MedBrief runtime, not the language or engine. Next: profile that path to find the culprit.
