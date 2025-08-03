# 🛠️ Ansible Homelab Automation

Automate your self-hosted homelab using Ansible, including Proxmox nodes, Ubuntu servers, and containers. This repo is designed for agentless SSH-based automation.

## 📁 Structure

```bash
ansible-homelab/
├── inventory/
│   ├── hosts.yml
│   └── group_vars/
├── playbooks/
├── roles/
├── ansible.cfg
└── README.md
```

## 🧩 Inventory Setup

Edit `inventory/hosts.yml` to define your nodes and groupings. You can organize them into groups like `proxmox`, `servers`, etc.

## 🔐 SSH Access

Ensure your control node (e.g., your laptop or management VM) can SSH into each host:
```bash
ssh-keygen
ssh-copy-id jay@10.1.20.10
```

Edit `group_vars/all.yml` for defaults like SSH user.

## ⚙️ Configuration

`ansible.cfg`:
```ini
[defaults]
inventory = ./inventory/hosts.yml
host_key_checking = False
retry_files_enabled = False
timeout = 20
```

## 🚀 Running Playbooks

Run a specific playbook like:

```bash
ansible-playbook playbooks/wake-pve.yml
```

Test host connectivity:

```bash
ansible all -m ping
```

## ✨ Included Playbooks

### Wake-on-LAN
Sends a WoL packet to a powered-off Proxmox node.

### Update Linux
Updates all apt packages on systems in the `servers` group.

### Install Docker
Installs Docker CE using the official repo via a reusable role.

## 📦 Roles

Reusable roles are stored in `roles/`:
- `common`: General utilities and tools
- `docker`: Handles Docker installation on Ubuntu

## 🔄 To-Do Ideas

- Automate backups
- Pi-hole and DNS setup
- VLAN-aware firewall role
- Proxmox backups and shutdown hooks

## License

MIT
