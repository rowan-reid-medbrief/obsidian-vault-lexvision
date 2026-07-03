---
name: medbrief-dev-vm-access
description: "SSH/ZeroTier connection details for Rowan's MedBrief DigitalOcean dev VM"
metadata: 
  node_type: memory
  type: reference
  originSessionId: 558c9501-5f64-4e14-8ad9-f1fe341a0b6b
---

Rowan's personal MedBrief dev VM, set up per the Confluence "Developer VM Environments" guide (MDC space, `847511553`):

- Hostname: `rowan-dev.medbrief.net`
- ZeroTier IP: `10.40.87.204` (network "Rowan's MSR Dev Envs", nwid `743993800f277320`)
- SSH: `ssh 10.40.87.204` (configured in `~/.ssh/config`: user `root`, key `~/.ssh/rowanreid_do`)
- Code lives at `~/Codebox/medbrief` on the VM (root-owned)
- Docker stack: `docker-app-1`, `docker-php-1`, `docker-db-1`, `docker-db_test-1`, `docker-mailcatcher-1`; cold-start with `cd ~/Codebox/medbrief/docker && docker compose up -d`

See [[medbrief-dev-environment-bridge]] for how this bridges to the local Claude Code project via Mutagen.
