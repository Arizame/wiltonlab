# 🛣️ Roadmap

Detailed view of planned work, grouped by phase.

---

## Phase 1 — Lab network foundation

**Goal:** Bring the Cisco gear online and create a true separation between prod and lab.

- [ ] Rack and cable the **Catalyst 2960-X**
- [ ] Rack and cable the **Cisco 1900 ISR**
- [ ] Console into both, factory reset, baseline IOS config
- [ ] Configure trunk between UDM Pro Max ↔ Cisco 1900 (VLAN 99)
- [ ] Spin up at least one lab VLAN with DHCP via the 1900
- [ ] Document running configs in `inventory/`

---

## Phase 2 — Proxmox hypervisor

**Goal:** Stand up the 4RU server as the workhorse of the lab.

- [ ] Inventory the 4RU hardware (CPU, RAM, drive bays, NICs)
- [ ] Decide on storage layout — ZFS pool vs HBA passthrough to TrueNAS
- [ ] Install Proxmox VE on a mirrored boot SSD pair
- [ ] Join Proxmox to the lab network (trunk port from Catalyst 2960-X)
- [ ] Set up automated config backups (`vzdump` + offsite)

---

## Phase 3 — Core self-hosted services

**Goal:** Move important data away from cloud providers.

- [ ] **Immich** — Photo backup
  - LXC or VM with GPU/iGPU passthrough for ML features
  - Backed by TrueNAS dataset
- [ ] **Jellyfin** — Media streaming
  - Hardware transcoding via Intel Quick Sync or NVENC
- [ ] **TrueNAS** — Storage backbone
  - HBA passed through to a TrueNAS VM
  - ZFS pool, snapshots, and replication
- [ ] Reverse proxy (Caddy or Traefik) for clean HTTPS access

---

## Phase 4 — Windows lab

**Goal:** Build an AD environment for hands-on practice.

- [ ] **Windows Server VM** — DC, DNS, DHCP for lab subnet
- [ ] **Windows Client VM** — Domain-joined workstation
- [ ] Optionally: a second DC for replication practice
- [ ] Snapshots / templates so the lab can be rebuilt quickly

---

## Phase 5 — Quality of life

- [ ] **Monitoring** — Prometheus + Grafana, or Uptime Kuma at minimum
- [ ] **Alerting** — Push notifications when something is down
- [ ] **Secrets management** — Self-hosted Bitwarden / Vaultwarden
- [ ] **Documentation site** — Maybe MkDocs or a wiki container
- [ ] **10 GbE** between Proxmox host and TrueNAS (if not already)

---

## Stretch goals

- Off-site backup replication (friend's house, cloud, or Backblaze B2)
- Internal CA + mTLS for sensitive services
- IPv6 throughout
- BGP between UDM and Cisco gear (overkill, but fun)
