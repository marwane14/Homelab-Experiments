# 🏗️ Infrastructure Overview

## Purpose
This section documents the foundational layers of the Homelab environment. The primary goal is to provide a stable, secure, and reproducible platform for cybersecurity research and network testing.

## Core Components

### 1. Physical Layer (Edge Security)
* **Perimeter Firewall:** A dedicated physical appliance (Protectli Vault) running OPNsense for advanced routing, firewalling, and IDS/IPS capabilities.
* **Switching:** Managed hardware allowing for physical device isolation and IEEE 802.1Q VLAN tagging.

### 2. Virtualization Layer (Compute)
* **Hypervisor:** Proxmox VE running on a dedicated node.
* **Role:** Orchestrates the deployment of offensive tools, defensive monitors, and vulnerable targets in a controlled environment.

## Network Strategy
The infrastructure relies on **Strict Segmentation**. Instead of a single flat network, the environment is divided into distinct security zones (VLANs) based on trust levels:
* **Management & Trusted:** For hypervisor control and personal administrative devices.
* **Lab & Research:** For experimental VMs, CTF targets, and potentially unsafe traffic.

---
## 📂 Documentation & Assets
* **[Networks/](./networks/):** Detailed topology diagrams and firewall logic.
* **[Proxmox-Configs/](./proxmox-configs/):** Hypervisor network bridge settings and hardware specs.

> *Refer to the [Network Diagram](./networks/network-diagram.png) for specific addressing and VLAN mapping.*
