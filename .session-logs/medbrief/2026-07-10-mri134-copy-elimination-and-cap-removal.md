---
date: 2026-07-10
project: /Users/Rowan.Reid/claude_code/medbrief-work
domain: medbrief
session: Disproved the "19x MedBrief runtime overhead", eliminated the whole-file copy behind the page-subset endpoint, and replaced the invented 500-page cap with the document's own length
type: wrap-up
tags: [mri-134, medbrief, apryse, pdfnet, performance, benchmarking, php, symfony, page-subset, nginx, php-fpm]
repos:
  - path: /Users/Rowan.Reid/claude_code/medbrief-work/repo
    commit: 27547ede35e26bb7dfc23b626d81db04ae1747bd
parent: 2026-07-10-mri134-scale-benchmark-and-php-vs-python.md
model_check: not-needed
---

## Session Summary

Profiling the page-subset extraction path overturned the premise it was meant to confirm: the "~19x MedBrief runtime overhead" does not exist, and measured warm and back-to-back the booted Symfony kernel runs the identical PDFNet operation at standalone-PHP speed. The real cost was `copyToLocal` copying the whole multi-GB source before extracting a handful of pages, doubling the working set past RAM so the extract read cold; opening a local source in place cut a 10,000-page subset from 89s to 46s and a 500-page one from 26s to 1.8s (`3a0b5d109`). A second commit (`27547ede3`) dissolved the 500-page cap, which was ours rather than inherited and whose stated rationale was already covered by the document-bounds check: ranges are now measured arithmetically and expanded only after the document bounds them, so a legitimate 9,000-page date range works while `1-999999999` is refused in 0.058ms with no allocation.

For Deon: PHP-Apryse-11.4 and Python-Apryse-12.0 tie at every size (same C++ core), so Python is not faster than PHP, and PyMuPDF is disqualified (133s at 10k pages, 2.9GB RSS, cannot linearise). Three pre-existing constraints surfaced and were logged as ideas: the PHP request wall is nginx's 60s fastcgi default (not the 600s I first claimed), php-fpm runs only 5 workers with no terminate timeout, and the subset cache has no eviction. Two honesty corrections belong on the record: an earlier "functional test passed" claim was an artefact of reading `tail`'s exit code through a pipe (the functional test cannot run at all here, a pre-existing `MatchLoA` test-container failure proven by reproducing it at `f0314aea1`), and the 600s timeout claim was wrong. Verification that did hold: 23 unit tests, PHPStan, Psalm, and direct runtime probes.
