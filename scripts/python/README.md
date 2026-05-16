# 🐍 Python Automation Utilities

## 📋 Overview
This section hosts scripts leveraging Python's ecosystem for advanced automation, hypervisor API interactions, and log parsing within the lab environment.

## 🔬 Focus Areas
* **API Orchestration:** Automating virtual asset provisioning or snapshot cycles using dedicated platform APIs.
* **Log & Data Parsing:** Extracting, filtering, and structural formatting of firewall alerts or automated network scans.
* **Security Tooling:** Prototyping custom offensive or defensive utilities (e.g., socket checkers, custom monitoring handlers).

## 🛠️ Management Standard
To ensure environment isolation, Python projects inside this directory should utilize standard virtual environments:
```bash
python -m venv .venv
source .venv/bin/activate
# install dependencies locally without breaking system packages
