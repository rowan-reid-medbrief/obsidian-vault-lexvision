---
date: 2026-04-23
project: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
session: Create project-level run-pipeline skill for Claude Code
type: handoff
tags: skills, claude-code, run-pipeline, MD-304
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
    commit: a272f44
domain: medbrief
---

## Session Summary

Short session to create `.claude/skills/run-pipeline/SKILL.md` — a project-level Claude Code skill encoding the correct way to run the Trust-centre pipeline (venv path, `--no-progress` flag, SESSION_LIMIT guidance, pre-run `.env`/`.venv` checks, optional post-run validation). User chose project-level `.claude/skills/` over the global `~/.claude/skills/` when prompted. Skill is committed; whether the harness auto-loads project-level skills is untested and is the first thing to verify in the next session.

## Continuation Prompt

## Continuation: Test run-pipeline project skill

**Parent session:** 2026-04-23-run-pipeline-skill.md

### Context
We're building a data pipeline for the MedBrief Trust-centre ML dataset (MD-304), currently on a progressive SESSION_LIMIT scaling strategy. This session created a Claude Code skill to encode the correct way to run the pipeline.

### What was done this session
- Created `.claude/skills/run-pipeline/SKILL.md` in the `data_pipelines` project root — a project-level Claude Code skill covering: pre-run `.env`/`.venv` checks, SESSION_LIMIT guidance (dev vs production), correct invocation (`.venv/bin/python scripts/run_pipeline.py --no-progress`), output interpretation, and optional post-run validation
- Committed to `data_pipelines` at `a272f44`
- Saved feedback memory: prefer project-level `.claude/skills/` for project-specific skills

### Current state
- Skill file committed at `a272f44`, not yet pushed to remote
- SESSION_LIMIT progression so far: 10 → 50 → 200 → 500 → 1000; next planned: unlimited/full dataset

### Where we left off
Skill created but **not yet tested** — we don't know if the Claude Code harness auto-loads skills from a project's `.claude/skills/` directory.

### Next steps
1. **Test the skill**: type `/run-pipeline` in this session and see if it's recognised. If yes, run the pipeline (confirm SESSION_LIMIT intent first). If not, move the skill to `~/.claude/skills/run-pipeline/SKILL.md` and test again.
2. If the skill works, run the pipeline for the next scaling step (unlimited/full dataset).

### Key references
- Skill file: `data_pipelines/.claude/skills/run-pipeline/SKILL.md`
- Run script: `data_pipelines/scripts/run_pipeline.py`
- Validation: `data_pipelines/scripts/validate_trust_pipeline.py`
