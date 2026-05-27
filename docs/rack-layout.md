# 🗄️ Rack Layout

**Enclosure:** 22RU rack
**Power:** Eaton 1500W UPS (bottom-mounted for weight)

```
┌──────────────────────────────────────────┐
│ 22 │ [reserved]                          │
│ 21 │ Patch panel + cable management      │
│ 20 │ UDM Pro Max                         │
│ 19 │ USW Pro Max                         │
│ 18 │ [reserved / 1U brush]               │
│ 17 │ Cisco Catalyst 2960-X (Lab) [WIP]   │
│ 16 │ Cisco 1900 Router (Lab) [WIP]       │
│ 15 │                                     │
│ 14 │                                     │
│ 13 │   (available expansion bays)        │
│ 12 │                                     │
│ 11 │                                     │
│ 10 │                                     │
│  9 │                                     │
│  8 │ ┌─────────────────────────────┐     │
│  7 │ │  4RU Server                 │     │
│  6 │ │  (Proxmox - planned)        │     │
│  5 │ └─────────────────────────────┘     │
│  4 │ WIL-SER01 (HP Mini) [shelf]         │
│  3 │ WIL-SER02 (HP Mini) [shelf]         │
│  2 │ [cable management]                  │
│  1 │ Eaton 1500W UPS                     │
└──────────────────────────────────────────┘
```

## Cooling & Airflow

- Front-to-back airflow from rack-mounted gear
- HP Mini PCs sit on a vented shelf — passive cooling sufficient
- Plan to add a 1U fan tray once the 4RU server is online

## Cable Management

- CAT6 patch leads, color-coded by VLAN where practical:
  - **Blue** — Trusted / Management
  - **Yellow** — IoT
  - **Red** — Lab
  - **Green** — Server VLAN
- Velcro ties (no zip ties) so re-cabling is painless

## Power Distribution

- Eaton UPS feeds a rack PDU
- Critical gear (UDM, USW Pro Max, `WIL-SER01`) on protected outlets
- Game server and lab gear on non-critical outlets (UPS preserves battery for prod)
