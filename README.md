
# **Tyk-Ansible-PoC**

Deploy **Tyk API Gateway**, **Tyk Dashboard**, and **Tyk Pump** using **Ansible** on Ubuntu servers.  
Includes **PostgreSQL** and **Redis** integration with support for **custom configuration files**.

---

## ✅ **Components Deployed**

This is assuming you have the dependencies deployed before deploying Tyk.
- **Tyk Dashboard**: v5.7.1
- **Tyk Gateway**: v5.7.1
- **Tyk Pump**: v1.11.1
- **PostgreSQL**: v13
- **Redis**: latest stable

---

## 🖥️ **Ansible Controller Instance**
- Ansible installed for orchestration
- SSH access to target hosts

## 🖥️ **Target Host Instance**
- Runs Tyk components, PostgreSQL, Redis
- Accessible via private key (PEM)

---

## 🔐 **Connect to Ansible Controller**
```bash
ssh -i "your-key.pem" ubuntu@your-controller-ip
```

Check **Ansible is installed**:
```bash
ansible --version
```

Clone this repository:
```bash
git clone https://github.com/Fadzli-fast/Tyk-Ansible-Poc.git
cd Tyk-Ansible-Poc
```

---

## ⚙️ **Inventory File (`inventory.yaml`)**
Edit the file and set your server details:
```yaml
all:
  hosts:
    dashboard:
      ansible_host: <DASHBOARD_SERVER_IP>
      ansible_user: ubuntu
      ansible_ssh_private_key_file: ./your-key.pem
    gateway:
      ansible_host: <GATEWAY_SERVER_IP>
      ansible_user: ubuntu
      ansible_ssh_private_key_file: ./your-key.pem
    pump:
      ansible_host: <PUMP_SERVER_IP>
      ansible_user: ubuntu
      ansible_ssh_private_key_file: ./your-key.pem
```

---

## ✅ **Test Connectivity**
```bash
ansible all -i inventory.yaml -m ping
```

---

## 🛠 **Project Structure**
```
tyk-ansible/
├── ansible.cfg
├── inventory.yaml
├── playbook.yaml
├── group_vars/
│   └── all.yml
├── roles/
│   ├── dashboard/
│   │   ├── tasks/main.yaml
│   │   └── files/tyk_analytics.conf
│   ├── gateway/
│   │   ├── tasks/main.yaml
│   │   └── files/tyk.conf
│   └── pump/
│       ├── tasks/main.yaml
│       └── files/pump.conf
└── your-key.pem
```

---

## ▶️ **Run Deployment**
```bash
ansible-playbook -i inventory.yaml playbook.yaml
```

---

## 📜 **Custom Config Files**
Replace the default configs with your own:

- **Dashboard** → `roles/dashboard/files/tyk_analytics.conf`
- **Gateway** → `roles/gateway/files/tyk.conf`
- **Pump** → `roles/pump/files/pump.conf`

These will be copied to:
- `/opt/tyk-dashboard/tyk_analytics.conf`
- `/opt/tyk-gateway/tyk.conf`
- `/opt/tyk-pump/pump.conf`

---

## ✅ **Installed Services**
- **Tyk Dashboard** → `http://<host>:3000`
- **Tyk Gateway** → `http://<host>:8080`
- **Tyk Pump** → Syncs analytics to PostgreSQL

---

## 🔐 **Security Notes**
- Use SSH keys for Ansible connections
- Secure sensitive variables with **Ansible Vault**:
```bash
ansible-vault encrypt group_vars/all.yml
```
