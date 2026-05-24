**[CRITICAL SECURITY WARNING]**
**Vulnerability Identified:** "I leave everything open for now, when I'm done I will activate it."
**Risk:** Implementing an "allow all" rule between VLANs during the configuration phase neutralizes the purpose of network segmentation. If your Protectli router has an active WAN connection, or if a compromised device exists on your local network, your Proxmox management interface and other critical infrastructure are exposed to lateral movement. Setting up external access (via your newly purchased domain) while the internal network is "open" drastically multiplies this risk.
**Remediation:** Implement a **Default Deny** policy immediately. Create explicit allow rules strictly for your designated Main PC IP address to access the Proxmox management GUI and OPNsense via the designated management VLAN. Do not expose services externally until internal isolation is fully enforced.

---

# 🎯 Project: OPNsense VLAN Segmentation & DHCP Migration

**Date:** May 24, 2026 | **Category:** Infrastructure Security & Networking | **MITRE Tactic:** Mitigation for TA0008 (Lateral Movement)

## 1. Objective

Establish rigid network segmentation via VLANs to isolate the Proxmox hypervisor environment from standard network traffic, designating a single management node. Resolve OPNsense DHCP assignment failures across segregated subnets to ensure reliable IP allocation.

## 2. Environment & Tools

* **Infrastructure:** Protectli Vault (Firewall/Router), Proxmox VE (Hypervisor), Managed Switch
* **Target OS:** OPNsense, Arch Linux (Main PC / Management Node)
* **Tools Used:** OPNsense WebGUI, KEA DHCPv4, ISC DHCPv4

## 3. Methodology & Execution

1. Configured 802.1Q VLAN tagging on the managed switch to logically separate the network into two distinct VLANs.
2. Provisioned corresponding VLAN interfaces within the OPNsense routing table.
3. Enabled OPNsense Next-Gen KEA DHCPv4 server for IP assignment on the newly created VLANs.
4. Diagnosed DHCP failure (clients failing to receive IP leases).
5. Disabled KEA DHCPv4 and reverted to the legacy ISC DHCPv4 service.
6. Assigned static routing policies to grant the Main PC exclusive administrative access to the Proxmox management interface.
7. Prepared external access architecture (Domain Name acquired) for future secure reverse proxy / VPN deployment.

## 4. Results & Artifacts

* Two functional VLANs established and recognized by the managed switch and OPNsense.
* DHCP IP allocation fully operational via legacy ISC daemon.
* Main PC successfully provisioned as the sole authorized management node for hypervisor administration.
* Proxmox management interface isolated from standard LAN traffic.

## 5. Lessons Learned & Troubleshooting

* **Challenge:** Extended 5-hour debugging session due to newly provisioned VLANs failing to issue IP addresses to connected clients. Root cause traced to bugs/instability in the OPNsense KEA DHCPv4 implementation.
* **Solution:** Abandoned the KEA DHCPv4 engine. Falling back to the deprecated but stable ISC DHCPv4 legacy service immediately resolved all broadcast and lease assignment failures.
