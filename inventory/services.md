# 📦 Service Inventory

Every running container, VM, and service across all hosts.

---

## WIL-SER01 — Utility Docker host

Runs on Ubuntu Server with Docker + Docker Compose.

| Service | Image / Source | Port(s) | Purpose | Notes |
|---------|---------------|---------|---------|-------|
| **Pi-hole** | `pihole/pihole` | 53 (DNS), 80 (web) | Network-wide DNS + ad blocking | Set as primary DNS in UDM |
| **HomeBridge** | `homebridge/homebridge` | 8581 (web) | Bridges non-HomeKit devices to Apple Home | Plugins: UniFi Protect, eufy, Meross |

### HomeBridge plugins

| Plugin | Bridges |
|--------|---------|
| `homebridge-unifi-protect` | UniFi cameras → HomeKit |
| `homebridge-eufy-security` | eufy Doorbell → HomeKit |
| `homebridge-meross` | Meross smart garage controller → HomeKit |

---

## WIL-SER02 — Gaming / cache host

| Service | Image / Source | Port(s) | Purpose | Notes |
|---------|---------------|---------|---------|-------|
| **Steam Cache** | `lancachenet/monolithic` | 80, 443 | LAN caching of Steam, Origin, Epic, etc. | Big SSD/HDD required |
| **Game servers** | Per-game | Varies | Dedicated game hosting | _(specify games)_ |

---

## WIL-HV01 (planned) — Proxmox VMs / LXCs

| Name | Type | Resources | Purpose | Storage backend |
|------|------|-----------|---------|----------------|
| `truenas` | VM | _(specify)_ | NAS + ZFS storage | HBA passthrough |
| `immich` | LXC or VM | _(specify)_ | Photo backup | NFS from TrueNAS |
| `jellyfin` | LXC or VM | _(specify, iGPU)_ | Media streaming | NFS from TrueNAS |
| `windc01` | VM | _(specify)_ | Windows Server / AD DC | Local SSD |
| `winclient01` | VM | _(specify)_ | Windows client for AD testing | Local SSD |

---

## UDM Pro Max — built-in services

| Service | Purpose |
|---------|---------|
| **UniFi Network** | Controller for all UniFi gear |
| **UniFi Protect** | NVR for cameras |
| **Threat Management** | IDS/IPS |

---

## Backup & Maintenance

| Task | Where | Frequency |
|------|-------|-----------|
| Docker compose volumes backup | `WIL-SER01`, `WIL-SER02` | _(specify — nightly?)_ |
| UDM config backup | Auto via UniFi cloud | Continuous |
| Proxmox `vzdump` snapshots | `WIL-HV01` (planned) | Nightly |
| Offsite copy | _(planned)_ | Weekly |
