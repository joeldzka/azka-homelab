Proxmox Installation Documentation

This document explains the installation and initial setup of Proxmox VE used in the homelab environment.

---

📌 Objective

Main objective:

Create a virtualization platform
for cybersecurity lab,
monitoring,
cloud services,
and Linux experimentation.

Hypervisor chosen:

Proxmox VE

Reason for choosing Proxmox:

✓ Free & open source
✓ Easy VM management
✓ Snapshot support
✓ Web-based interface
✓ Perfect for homelab
✓ Supports VMs & Containers

---

🖥️ Hardware

Current host machine:

Device      : Dell Inspiron 3458
Role        : Homelab Server
Hostname    : azka-pve

Future upgrades planned:

✓ Thermal paste replacement
✓ Cleaning maintenance
✓ LAN cable optimization
⬜ SSD SATA upgrade
⬜ RAM DDR3L upgrade
⬜ Battery replacement (if needed)

---

💿 Proxmox Installation

Step 1 — Install Proxmox VE

Proxmox VE installed on:

Dell Inspiron 3458

Installation media:

Bootable USB

Installation completed successfully.

---

Step 2 — Hostname Configuration

Configured hostname:

azka-pve

Purpose:

Easy identification
Professional naming
Future scalability

---

Step 3 — Local Network Access

After installation, Proxmox became accessible through:

https://<server-ip>:8006

Example:

https://192.168.x.x:8006

Successfully verified:

✓ Web UI accessible
✓ Node online
✓ Login successful
✓ VM creation available

---

🌐 Network Setup

Local networking configured successfully.

Capabilities:

✓ Local browser access
✓ LAN connectivity
✓ HTTPS interface

---

🏗️ Hypervisor Role

Current role of Proxmox host:

Main virtualization server

Responsibilities:

VM Hosting
Remote management
Infrastructure foundation
Cloudflare Tunnel endpoint

---

🐧 First Virtual Machine

First VM created:

debian-lab

Role:

Debian Core

Purpose:

Monitoring
Utility server
Docker host
Linux playground
Dashboard
SSH jump host

Current status:

✓ Installed
✓ Running
✓ Network connected
✓ Internet access
✓ SSH access

Current IP:

192.168.0.201

---

🔐 Secure Remote Access

One major milestone:

Remote access outside local network

Implemented using:

Cloudflare Tunnel

Final remote URL:

https://proxmox.azkapve.my.id

Benefits:

✓ No port forwarding
✓ Secure HTTPS access
✓ Public IP hidden
✓ Access anywhere

Successfully tested:

✓ Different Wi-Fi
✓ Mobile network
✓ Outside local network

---

🧠 Lessons Learned

Things learned during Proxmox setup:

Virtualization basics
Linux server management
Networking fundamentals
VM deployment
Remote access concepts
Cloudflare Tunnel
Troubleshooting

---

🚧 Planned Infrastructure

Planned VM architecture:

azka-pve
│
├── Debian Core
│   ├─ Monitoring
│   ├─ Docker
│   ├─ Dashboard
│   └─ Utility Server
│
├── Kali Lab
│   └─ Cybersecurity Practice
│
└── Debian Cloud
    ├─ Nextcloud
    ├─ NAS
    └─ File Storage

---

📍 Current Status

Infrastructure progress:

[✓] Proxmox Installed
[✓] Local Access Working
[✓] HTTPS Working
[✓] First VM Running
[✓] Remote Access Working
[✓] Cloudflare Tunnel Working
[ ] Monitoring Stack
[ ] Cybersecurity Lab
[ ] Cloud / NAS

Current operational service:

https://proxmox.azkapve.my.id
