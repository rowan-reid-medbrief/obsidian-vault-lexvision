---
name: project_mass-matter-import
description: "New MedBrief short-term project - bulk-import client Higgs' matters/records; briefed 2026-07-22, no ticket yet"
metadata: 
  node_type: memory
  type: project
  originSessionId: fd837c47-46a0-457f-bd01-da32fccc9b8b
  modified: 2026-07-23T06:37:50.689Z
---

Mass Matter Import: a one-off bulk import of the client **Higgs**' matters and radiology/hospital records into MedBrief, briefed by Deon Kuhn to Rowan on 2026-07-22. Build it as a Symfony console command IN the MedBrief product codebase (`repo/`), not standalone Python: matter creation means creating Doctrine entities, and the "processing queue" is just `Disc.status` polled by cron.

**No tracker ticket exists yet** (checked Jira + Azure DevOps 2026-07-22). Docs live under `docs/mass-matter-import/` with a provisional slug; rename if a ticket is cut.

Load-bearing findings (all in `docs/mass-matter-import/`, verified via gh-copilot against the source):
- **`Project::setManager()` grants NO authorisation** - the web flow separately adds `ROLE_PROJECT_{id}_PROJECTMANAGER` to the logged-in creator. A console command has no security token, so a naive import creates matters nobody can access, silently. This is the #1 thing to resolve before any creation code (DESIGN-NOTES §10.3).
- **`Project.account` is non-nullable** and a wrong value causes cross-tenant exposure. The client sheet does not carry an account value; source unresolved (§9.1, §10.1).
- Real Higgs data may run on Rowan's DigitalOcean VM (over ZeroTier), NEVER on local. Deon's binding rule (see [[project_medbrief_dev-environment]]).

The whole design was produced by aggressive gh-copilot offloading (six consults, ~1,167 credits, generate-broad-then-adversarially-verify). See `docs/mass-matter-import/copilot-briefs/` and the offload ledger. Related: [[project_ai-2066-translation]], [[project_medbrief-prod-file-access]].
