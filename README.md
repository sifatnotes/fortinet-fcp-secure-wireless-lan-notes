# fortinet-fcp-secure-wireless-lan-notes
Comprehensive community study guide, revision notes, core FortiAP and FortiGate configuration setups, and exam resources for the Fortinet FCP - Secure Wireless LAN 7.4 Administrator exam (FCP_FWF_AD-7.4).
# Fortinet FCP - Secure Wireless LAN Administrator (FCP_FWF_AD-7.4) Study Guide

Welcome to the open community-driven study repository for earning the **Fortinet Certified Professional (FCP) in Network Security** badge by passing the **Secure Wireless LAN Administrator** exam (`FCP_FWF_AD-7.4` / legacy NSE 5 Secure Wireless LAN).

This guide provides a structured breakdown of enterprise Wi-Fi deployment, FortiAP discovery and provisioning, CAPWAP tunnel architectures, advanced authentication, WIDS/WIPS security mechanisms, and troubleshooting commands.

---

## 📌 Certification Overview

To earn the **FCP in Network Security** certification, candidates must pass core network security requirements along with elective exams such as Secure Wireless LAN:

* **Exam Code:** `FCP_FWF_AD-7.4` (formerly aligned with NSE 5 Secure Wireless LAN)
* **Exam Title:** FCP - Secure Wireless LAN 7.4 Administrator
* **Vendor:** Fortinet / Pearson VUE
* **Question Count:** ~30–40 multiple-choice questions
* **Duration:** 60 minutes
* **Scoring:** Pass/Fail (score report provided via Pearson VUE)
* **Validity:** Certified for 3 years.

---

## 🎯 Who Should Take This Exam?

- **Network & Security Engineers:** Professionals responsible for deploying, maintaining, and managing enterprise wireless networks using FortiGate integrated controllers and standalone FortiAP access points.
- **System Administrators:** Engineers securing Wi-Fi infrastructure with WPA3-Enterprise, RADIUS/802.1X, captive portals, and WIDS policies.
- **Fortinet Channel Partners:** Technical consultants building Fortinet Security Fabric wireless solutions for SMB and enterprise customers.

---

## 📊 Exam Domain Breakdown

### Skills Measured & Subject Weights
| Domain | Exam Focus Area |
| :--- | :--- |
| **Introduction to Wireless Technology** | RF fundamentals, 802.11 standards (Wi-Fi 5/6/6E), channel planning, antenna patterns |
| **Wireless Networks Setup** | FortiAP discovery, CAPWAP tunneling, SSIDs, VLAN mapping, provisioning profiles |
| **Wireless Security & Authentication** | WPA2/WPA3 Personal & Enterprise, RADIUS authentication, Captive Portal, MPSK |
| **Advanced Wi-Fi & Centralized Management** | Bridge vs. Tunnel vs. Mesh mode, Rogue AP detection, WIDS, FortiManager integration |
| **Troubleshooting & Optimization** | CLI diagnostics, packet captures, signal strength optimization, handoff tuning |

---

## 🧠 Core Technical Concepts & Key Notes

<Image src="image_agent_tag_16937411454923231" alt="FortiGate Wireless Controller Network Topology" caption="FortiGate Integrated Wireless LAN Controller Topology" />

---

### 1. FortiAP Discovery & Deployment Modes
* **CAPWAP Tunneling:** FortiAPs establish Control and Provisioning of Wireless Access Points (CAPWAP) tunnels to the FortiGate integrated controller over UDP ports 5246 (Control) and 5247 (Data).
* **Discovery Methods:**
  - **Broadcast:** FortiAP sends broadcast packets on the local layer 2 segment.
  - **DHCP Option 138:** Supplies the IP address of the FortiGate wireless controller to FortiAPs across subnets.
  - **DNS Resolution:** FortiAP attempts to resolve `FORTICLOUD-AP-CAPWAP` or local DNS entries.
  - **Static / FortiCloud:** Pre-configured static controller IP or cloud registration.
* **Forwarding Modes:**
  - **Tunnel Mode:** All wireless client traffic is encapsulated in CAPWAP and sent directly to FortiGate for centralized firewall policy inspection.
  - **Bridge Mode:** Wireless traffic is bridged directly onto the local Ethernet switch port VLAN.
  - **Mesh Mode:** Wireless APs backhaul traffic to each other wirelessly when wired Ethernet cabling is unavailable.

### 2. Wireless Security & Authentication
* **Multiple PSK (MPSK):** Allows different preshared keys on a single SSID, assigning individual users or device types to specific VLANs without 802.1X complexity.
* **WPA3 Enterprise:** Enforces 192-bit cryptographic security suites, Protected Management Frames (PMF), and RADIUS server integration.
* **Wireless Intrusion Detection System (WIDS):** Monitors for rogue access points, ad-hoc networks, MAC spoofing, deauthentication attacks, and weak signal anomalies.

---

## 🛠️ Essential CLI Diagnostic Commands

```bash
# Check FortiAP connection status on FortiGate
diagnose wireless-controller wlac daemon status
diagnose wireless-controller wlac ap status

# Debug CAPWAP control tunnel traffic
diagnose debug application basecapwap -1
diagnose debug enable

# Monitor active wireless client connections
diagnose wireless-controller wlac client list

# Capture wireless management frames on a specific interface
diagnose sniffer packet wlan0 'type mgt' 4 0 a
