# 🛡️ Homelab & Cybersecurity Research Environment

## Overview
This repository documents my hands-on cybersecurity research, CTF walkthroughs, and infrastructure testing. I use this hybrid environment to simulate real-world attack scenarios and master defensive configurations.

---

## 🏗️ The Lab Architecture
My setup combines dedicated physical hardware and a virtualized stack for network isolation and realistic traffic analysis.

### Hardware Layer
* **Firewall (Edge):** Protectli Vault (Physical) – Handles network segmentation, IDS/IPS, and edge security.
* **Switching:** Managed Switch for VLAN tagging and physical device isolation.
* **Compute:** Dedicated Mini-PC running **Proxmox VE**.

### Virtualization Layer (Proxmox)
* **Offensive:** Kali Linux, Parrot OS.
* **Infrastructure:** Active Directory (Windows Server), Linux Servers (Debian/Arch), Docker.
* **Targets:** Vulnerable machines (VulnHub, Metasploitable), CTF environments.

---

## 📂 Project Structure
* `infrastructure/`: Network diagrams, OPNsense configs, and Proxmox setups.
* `writeups/`: Documentation of CTF challenges, exploit analysis, and security tests.
* `scripts/`: Automation tools developed in **Python** and **Bash**.

---

## 🎯 Core Objectives
* **Advanced Reconnaissance:** Deep-dive analysis of network protocols and service discovery.
* **CTF & Exploitation:** Documenting methodologies for various capture-the-flag challenges.
* **Defensive Hardening:** Implementing and testing security policies on physical and virtual assets.
