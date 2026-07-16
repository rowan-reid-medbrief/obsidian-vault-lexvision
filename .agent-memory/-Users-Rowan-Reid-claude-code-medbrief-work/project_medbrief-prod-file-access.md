---
name: medbrief-prod-file-access
description: How Rowan reaches MedBrief production document files (Azure Files shares) via the jumphost or portal; both access gates confirmed open 2026-07-10
metadata: 
  node_type: memory
  type: project
  originSessionId: 03c9fc96-e611-44ef-b719-b8df5fd9343a
---

MedBrief production document files live on **Azure Files** SMB shares (account `msrstandard`, shares `natives`, `optimized-pdf`, `ocr`, `page`, etc.), mounted on the processor/app VMs under `/medbrief/data/...`. **Only XOD** is in Azure Blob (`xod_blob_fs`). Full map + all access routes: `docs/storage-architecture.md` in this workspace.

Two ways in (data plane is firewalled from the laptop):
- **Jumphost SSH:** `az ssh vm -n Jumphost -g jumhosts` then hop `az ssh vm -n processor-22bsgt7is62mw--zone-1 -g medbrief-secure-review-production`. Subscription `MedBrief Secure Review` (`7b66abb8-...`) is already the right one.
- **Azure Portal:** `msrstandard` → File Shares → download; needs the storage-account IP whitelist.

Jumphost has **two gates**: (1) an NSG IP allow rule on `Jumphost-nic-nsg` (RG `jumhosts`), per-person home IPs; (2) `Infra_VM_login_user` EntraID group for login. **Both confirmed open for Rowan 2026-07-10** — added NSG rule `RowanHome` (priority 1080, his home IP), and SSH then connected, so he is already in the AD group. Caveat: the NSG rule is his home IP, so re-add/update if it rotates.

**Azure RBAC across the estate (checked 2026-07-16, read-only).** Rowan holds **subscription-root Contributor on MedBrief Secure Review** (`7b66abb8-…`), unconditional, so he can create storage accounts, resource groups, and Cognitive Services resources **anywhere in the production subscription himself**. `Microsoft.Storage` and `Microsoft.CognitiveServices` are both Registered and no policy assignment carries a Deny. The one ceiling everywhere: he **cannot create role assignments** (Contributor excludes `Microsoft.Authorization/*/Write`), so anything needing a managed-identity grant needs Owner or User Access Administrator. Elsewhere: only resource-scoped roles in **Azure DevTest** (no create rights; plus Owner on `stgsalli3odev`), and **no access at all** to Foundation A.I. or MedBrief Analytics.

**Worth re-checking any "needs Deon's Azure access" assumption against this.** It was wrong for [[project_ai-2066-translation]], where a "cannot self-serve storage" finding was true only of DevTest and had quietly blocked the workstream for days. [[project_mri-134-branch]]'s sibling MRI-133 thread carries a similar "corpus expansion needs Deon's Azure Blob / jumpbox access" claim that may be the same mistake; verify before treating it as blocked.

Contacts for access changes: Laura (NSG contributor), Jarek Olechno (AD groups); Deon routes. See [[medbrief-dev-vm-access]] (the separate personal DigitalOcean dev VM, not this prod path).
