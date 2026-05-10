# 🏗️ Infrastructure & Network Architecture

## 📋 Overview
This directory serves as the technical blueprint for the Homelab. It contains all network topology diagrams, hypervisor configurations, and edge firewall rules required to deploy, maintain, and rebuild the environment.

## 🕸️ Network Topology & Segmentation
The network is strictly segmented using an OPNsense physical firewall and a managed switch, ensuring isolation between production endpoints and vulnerable targets.

### VLAN Configuration
* **VLAN 01 (`VLAN_SERVEURS`):** Dedicated to the Proxmox VE hypervisor and its virtual machines (Attack boxes, CTF targets, Infrastructure servers). Subnet: `192.168.10.0/24`
* **VLAN 02 (`VLAN_PERSONNEL`):** Dedicated to trusted personal devices (e.g., Arch Linux host). Subnet: `192.168.20.0/24`

*Traffic between VLANs is heavily restricted and inspected by the OPNsense Intrusion Prevention System (IPS).*

## 📂 Directory Contents

### `/networks`
* **`network-diagram.png`**: Visual representation of the physical and logical data flow.
* **`opnsense/`**: Sanitized firewall rules, NAT configurations, and VLAN definitions.

### `/proxmox-configs`
* **`interfaces.txt`**: Host network configuration (Linux Bridges and VLAN tagging).
* **Hardware Specs:** Dedicated Mini-PC compute node documentation.

---
> 🔒 **Security Note:** All exported configuration files in this directory are sanitized. No plaintext credentials, private keys, or public IP addresses are stored in this repository.
