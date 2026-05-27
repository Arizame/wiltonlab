# 🌐 Networking

Detailed view of the network configuration across the main and lab environments.

---

## Main Network

Managed end-to-end by the UniFi ecosystem.

### Hardware

| Role | Device | Notes |
|------|--------|-------|
| Gateway | UDM Pro Max | Router, firewall, IDS/IPS, UniFi Protect NVR |
| Core switch | USW Pro Max | All uplinks, PoE for cameras / APs |
| Edge switch | UniFi Flex Mini | Bedroom workstation/console drop |

### VLANs

| VLAN | Subnet (example) | Name | Devices | Inter-VLAN |
|------|------------------|------|---------|-----------|
| 1 | `192.168.1.0/24` | Management | UniFi gear, switches | Restricted |
| 10 | `192.168.10.0/24` | Trusted | Personal laptops, phones, Apple TV | Full out |
| 20 | `192.168.20.0/24` | IoT | UniFi Protect cameras, eufy doorbell, Meross garage | No internet to/from trusted except via HomeBridge |
| 30 | `192.168.30.0/24` | Guest | Guest Wi-Fi | Internet only |
| 40 | `192.168.40.0/24` | Servers | `WIL-SER01`, `WIL-SER02` | Selective |
| 99 | `192.168.99.0/24` | Lab | Catalyst 2960-X, Cisco 1900, future Proxmox | Isolated from Trusted by default |

> Replace example subnets with your actual ranges before publishing publicly.

### Firewall Rules (high-level)

| # | From | To | Action | Purpose |
|---|------|----|----|---------|
| 1 | IoT | Trusted | Block (established/related allowed) | Stop cameras phoning home into trusted devices |
| 2 | Guest | Any local | Block | Guests get internet only |
| 3 | Lab | Trusted | Block | Lab can't reach prod |
| 4 | Trusted | Lab | Allow | Admin from main desktop |
| 5 | Any | Servers:HomeBridge | Allow specific ports | HomeKit bridge access |

### Port Forwards

| External Port | Internal Target | Service |
|--------------|----------------|---------|
| _(fill in)_ | `WIL-SER02:<port>` | Game server |
| _(fill in)_ | _(future)_ | Reverse proxy entry point |

⚠️ **Security note:** Keep external exposure minimal. Prefer a reverse proxy (Caddy / Traefik / NPM) with TLS once Proxmox is online.

---

## Lab Network (WIP)

Separate L2/L3 domain for learning enterprise networking.

### Topology

```
UDM Pro Max  ─── trunk (VLAN 99) ───  Cisco 1900 ISR
                                          │
                                    Catalyst 2960-X
                                          │
                                      4RU Proxmox host
                                      (planned VMs)
```

### Planned Config

- Cisco 1900 acts as the L3 gateway for lab subnets
- Catalyst 2960-X handles VLAN trunking and access ports for the Proxmox host
- A single uplink VLAN between UDM and Cisco 1900 carries lab traffic
- DHCP served by the Cisco 1900 (or pushed onto a lab VM)

---

## DNS

- **Primary:** Pi-hole on `WIL-SER01` (VLAN 40)
- **Upstream:** Cloudflare / Quad9
- **Conditional forwarding:** Local UDM domain for reverse lookups

---

## UniFi Protect

- All cameras on **VLAN 20 (IoT)**
- NVR hosted on the UDM Pro Max internal storage
- Access only from VLAN 10 (Trusted) and HomeBridge on `WIL-SER01`
