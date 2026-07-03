---
tags: [claude-code, skills, packaging, check-model, harden-plan, team-sharing]
repos: [ObsidianVault]
parent: null
model_check: not-needed
---

# Share check-model + harden-plan skills as a team package

Built a self-contained, shareable package of the `check-model` and `harden-plan` skills for Rowan's team. Genericised both (embedded the model/effort complexity matrix directly into check-model so it no longer needs the private CLAUDE.md; replaced "Rowan" with "the user" and softened profile/ and sibling-skill dependencies in harden-plan), wrote a beginner-oriented README for teammates new to AI and skills, copied the sweep_sidecars.sh script + its test suite (16/16 pass), and zipped it to `demo1/claude-skills-pack.zip` (20K).

Decisions: self-contained genericisation over faithful-copy; zip format; README pitched at non-technical users. Note: the package lives in a non-git demo dir, so it is not version-controlled; the deliverable is the zip. check-model's matrix now uses generic model bands (lightest/mid-tier/most capable) rather than Rowan's exact routing, flagged in the README as the one spot to edit for a house standard.
