---
tags: [medbrief, mri-134, git-migration, github, bitbucket, pdf-split, testing, demo, apryse]
repos:
  - medbrief:f0314aea1
model_check: not-needed
---

# MRI-134 PDF-split: Deon demo, Bitbucket->GitHub migration, demo-hack cleanup, VM tests

Demoed the parked `feature/MRI-134-pdf-split-approach` branch to Deon (positive; he wants to trial it on the zone-2 production-linked VM). Removed Rowan's personal `docs/IDEAS.md` from the MedBrief repo (content preserved in project memory), committed then reverted the two temporary dev-VM demo hacks (PageSpecParser cap 500->1000, PathResolverStrategy native-PDF routing), and migrated the repo Bitbucket->GitHub per the migration guide (repointed origin to `github.com:medbrief/msr-medbrief`, fetched --prune --tags, fast-forwarded develop 11 commits, pushed the branch clean at `f0314aea1`). Confirmed the `streamPageSubsetAction` copy-to-local is production-correct (a first-class `FileHandlerInterface` method; PDFNet can only open a local path), and ran tests on the VM: `PageSpecParserTest` 17/17 green, while the `PDFTools/Split` integration tests are blocked by a pre-existing, repo-wide EM-853 `MatchLoA` test-container compile failure (confirmed via `lint:container --env=test`), not from this branch.

## Details

- **Demo to Deon:** positive; floated the zone-2 (production-linked) VM and asked which branch. Branch was local-only, which prompted the push and surfaced the migration.
- **Personal IDEAS.md removed:** `git rm docs/IDEAS.md`, commit `b220b4e19`. Its two open items (permanent Azure blob-fallback for `streamOcrXodAction`; a reproducible seed+teardown command for the demo) preserved in the `project_mri-134-branch` memory.
- **Demo hacks:** committed as-is with their "revert before commit" comments (`f623629ce`) so the branch could go up, then reverted byte-identically to the pre-hack state (`f0314aea1`) once confirmed the subset render does not depend on them (the RecordsViewer `withPageSubset` hook rewrites any resolved route to the page-subset endpoint when `?pages=` is present).
- **Bitbucket->GitHub migration:** Confluence guide 1056079874 section 2. Bitbucket rejected the new-branch push (pre-receive hook); GitHub accepted it. GitHub SSH already worked (`rowan-reid-medbrief`), so no key setup. GitHub already had a differently-named MRI-134 branch (`feature/MRI-134-Date-Filter-...`, the ticket auto-name), distinct from this pdf-split branch.
- **copy-to-local review:** production-correct, reused by DiscloseProject / MatchExpertLoASend; Rowan chose to leave it over the leaner direct-path alternative (keeps it storage-portable if native/ocr/optimized ever move to Azure like XOD did).
- **Tests (VM `docker-php-1`):** PageSpec unit tests pass at the restored 500 cap. The Split integration tests error 4/11 in `setUp` because the whole test-env container will not compile (`MatchLoA::$companyLetterheadLogoImageFs` fails to autowire despite the bind at `config/services.yaml:75`, byte-identical on develop); every kernel-booting test is affected. EM-853's issue, not MRI-134's. Local Mac test-running deferred (no composer/Docker/vendor); staying on the Mutagen-synced VM.
