# 🖥️ Hardware Inventory

---

## Network

### UDM Pro Max
- **Role:** Main router, firewall, IDS/IPS, UniFi Protect NVR
- **Form factor:** 1U rackmount
- **Storage:** _2x 4TB Seagate Skyhawk Surveillance Drives_
- **Notes:** Runs UniFi Network + Protect controllers

### UniFi Switch Pro Max (USW Pro Max)
- **Role:** Main L2/L3 switch
- **Ports:** _24 Port_
- **PoE budget:** _400W_
- **Uplinks:** _10G Uplink to UDM_

### UniFi Flex Mini 2.5G
- **Role:** Edge switch for room
- **Ports:** 5x 2.5GbE (1 uplink + 4 downlinks)
- **PoE:** Powered via PoE from USW

### Cisco Catalyst 2960-X _(Lab — WIP)_
- **Role:** Lab L2 switch
- **Ports:** _48 Port_
- **IOS version:** _N/A_
- **Status:** Not yet racked / configured

### Cisco 1900 Series ISR _(Lab — WIP)_
- **Role:** Lab L3 router
- **Model:** _(1921 / 1941 — specify)_
- **IOS version:** _(specify)_
- **Modules:** _(any HWICs / WICs installed)_
- **Status:** Not yet racked / configured

---

## Compute

### WIL-SER01
- **Hardware:** HP Mini PC _(specify model — EliteDesk Mini / ProDesk Mini G_)_
- **CPU:** _(specify)_
- **RAM:** _(specify GB)_
- **Storage:** _(specify SSD/HDD)_
- **Network:** _(1GbE / 2.5GbE)_
- **OS:** Ubuntu Server LTS
- **Role:** Docker host
- **Key containers:** Pi-hole, HomeBridge

### WIL-SER02
- **Hardware:** HP Mini PC _(specify model)_
- **CPU:** _(specify)_
- **RAM:** _(specify GB)_
- **Storage:** _(specify — likely larger for game/cache data)_
- **Network:** _(1GbE / 2.5GbE)_
- **OS:** Ubuntu Server LTS
- **Role:** Game server, Steam Cache (lancache)

### WIL-HV01 _(planned)_
- **Hardware:** 4RU rackmount server
- **Chassis:** _Silverstone RM41-H04_
- **CPU:** _(TBD)_
- **RAM:** _(TBD - 64-128GB?)_
- **Storage:**
  - Boot: _(TBD)_
  - Data: _(TBD)_
- **NICs:** _(TBD)_
- **GPU:** _(TBD)_
- **OS:** Proxmox VE

---

## Power

### Eaton UPS (Unmanaged)
- **Model:** _Eaton 5E_
- **Capacity:** 900W / _(1500VA)_
- **Battery runtime:** _~3 Hours - Script to shut down servers present_

---

## Rack

- **Type:** 22RU
- **Brand / model:** RMS
- **Depth:** 600mm
- **Cooling:** enclosed - in A/C room
