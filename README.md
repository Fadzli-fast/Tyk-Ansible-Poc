
# Tyk-Ansible-PoC

This repository provides an **Ansible-based automation** to deploy the **Tyk API Gateway**, **Tyk Dashboard**, **Tyk Pump**, and **Tyk Developer Portal** on **Ubuntu servers**.  
It also supports integration with **PostgreSQL** and **Redis** for persistent storage.
You will need to have dependencies deployed beforehand.

---

## 🚀 Features
- Automates installation of:
  - Tyk Gateway
  - Tyk Dashboard
  - Tyk Pump
  - Tyk Developer Portal
- Configures APT repositories and GPG keys for secure installation.
- Deploys custom configuration files for each component.
- Uses roles for modular, reusable Ansible structure.
- Supports version pinning for Tyk components.

---

## 📂 Repository Structure
```
.
├── ansible.cfg               # Ansible configuration
├── inventory.yaml            # Inventory file for defining hosts
├── playbook.yaml             # Main Ansible playbook
├── group_vars/
│   └── all.yaml              # Global variables (versions, paths)
└── roles/
    ├── gateway/              # Role for Tyk Gateway
    │   └── tasks/main.yaml
    ├── dashboard/            # Role for Tyk Dashboard
    │   └── tasks/main.yaml
    ├── pump/                 # Role for Tyk Pump
    │   └── tasks/main.yaml
    └── portal/               # Role for Tyk Developer Portal
        └── tasks/main.yaml
```

---

## ✅ Prerequisites
- **Ubuntu 20.04+** servers for Tyk components
- **Ansible 2.10+**
- **PostgreSQL** (External or installed manually)
- **Redis** (External or installed manually)
- Access to GitHub repository
- sudo privileges on target servers

---

## 🔧 Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/Fadzli-fast/Tyk-Ansible-Poc.git
cd Tyk-Ansible-Poc
```

### 2. Update Inventory
Edit `inventory.yaml`:
```yaml
all:
  hosts:
    gateway:
      ansible_host: <GATEWAY_SERVER_IP>
    dashboard:
      ansible_host: <DASHBOARD_SERVER_IP>
    pump:
      ansible_host: <PUMP_SERVER_IP>
    portal:
      ansible_host: <PORTAL_SERVER_IP>
```

### 3. Define Variables
Update `group_vars/all.yaml` with component versions and configuration details:
```yaml
tyk_gateway_version: "5.8.1"
tyk_dashboard_version: "5.8.1"
tyk_pump_version: "1.8.0"
tyk_portal_version: "1.14.0"
```

### 4. Run the Playbook
```bash
ansible-playbook -i inventory.yaml playbook.yaml
```

---

## 🛠 Supported Platforms
- Ubuntu 20.04+

---

## 📜 License
This project is licensed under the MIT License.
