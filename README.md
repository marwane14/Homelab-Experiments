# 🛡️ Homelab & Cybersecurity Research Environment


## 🎯 Overview

This repository serves as the operational blueprint and research log for a hybrid cybersecurity homelab. Designed to bridge the gap between theoretical concepts and practical execution, this environment is built to simulate real-world attack vectors, engineer robust defensive architectures, and validate security postures through continuous testing.


---


## 🏗️ Architecture & Stack

The infrastructure enforces a strict Zero Trust network model, leveraging a combination of bare-metal appliances and virtualized environments to ensure complete isolation and high-fidelity traffic analysis.


### Edge & Physical Layer

* **Perimeter Security:** Protectli Vault running OPNsense (IDS/IPS, deep packet inspection, and stateful firewalling).

* **Network Segmentation:** 802.1Q VLAN tagging via a managed switch for isolated operational zones.

* **Compute Node:** Dedicated bare-metal hypervisor (Proxmox VE) optimized for secure, isolated workload execution.


### Virtualized Operations

* **Offensive Operations:** Kali Linux and custom attack environments.

* **Enterprise Infrastructure:** Active Directory domains, Linux server deployments, and containerized services (Docker).

* **Testing Grounds:** Ephemeral vulnerable targets and CTF simulation environments.


---


## 📂 Repository Navigation

* 🕸️ **[`/infrastructure`](./infrastructure/)**: Network topology diagrams, firewall routing logic, and hypervisor resource allocation strategies.

* 📝 **[`/writeups`](./writeups/)**: Post-mortem reports on vulnerability exploitation, CTF methodologies, and defensive tuning.

* ⌨️ **[`/scripts`](./scripts/)**: Custom Python and Bash utilities for environment automation, log parsing, and security tooling.

* 🎨 **[`/assets`](./assets/)**: Centralized media storage, topology diagrams, and documentation graphics.


---


## 🚀 Strategic Objectives

* **Offensive Engineering:** Execute advanced reconnaissance, map attack surfaces, and develop reliable exploitation methodologies.

* **Defensive Hardening:** Design strictly segmented networks, tune intrusion detection systems, and implement robust access controls.

* **Continuous Automation:** Streamline lab provisioning and operationalize security monitoring routines.
