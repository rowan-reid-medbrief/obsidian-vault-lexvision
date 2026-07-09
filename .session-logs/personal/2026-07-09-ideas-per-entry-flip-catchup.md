---
tags: [config, ideas-store, migration, git, maintenance]
repos: ~/.claude @ 1bbedab
model_check: not-needed
---

# Ideas per-entry store catch-up (#sznmbe M4)

Brought this machine's `~/.claude` up to date after the #sznmbe M4 flip that converted `docs/IDEAS.md` from a single git-union-merged file into a per-entry `docs/ideas/<id>.md` store. It was a clean fast-forward (`6733cfa..1bbedab`, 39 commits) with no local commits ahead and no uncommitted IDEAS.md appends, so there was nothing to rehome and nothing to commit.

Verified no idea was lost: parser block count == store file count == **270**; all 246 standard-`[#id]` entries plus 4 mnemonic-keyed (`wd-b2`, `prosemirror`, `mgxoffshift`, `mgvis`) plus 3 upstream-stamped no-id entries (`geu3kr`, `3caoq7`, `8974d6`) resolve in the store, and the one bare `[done b798105]` bullet was archived upstream (commit `0642f22`, now in `IDEAS-ARCHIVE.md`). `OVERNIGHT_VERIFY_PASS:ideas-reader-completeness` was green.

`tests/run.sh` was 46/52 passing; the 6 failing suites are all environmental (missing doc-gen venvs for `fill-pdf`/`huble-docx`/`huble-pptx`/`medbrief-brand`, and the un-cloned `claude-cockpit` repo for `ingest-suggestions`/`self-improve`), not regressions. Captured that as a machine reference memory so a future session doesn't re-investigate the red suites.
