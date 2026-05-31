# azka-homelab
Personal homelab project using Proxmox, Debian, Cloudflare Tunnel, and cybersecurity infrastructure.

🚀 Azka Homelab Documentation

«Personal Homelab Project for Cybersecurity, Networking, Linux, and Self-Hosted Infrastructure»

---

📌 Project Overview

This repository documents the development of my personal homelab environment using Proxmox VE, Debian Linux, and Cloudflare Tunnel for secure remote access.

The main purpose of this homelab is:

- Learning Linux server administration
- Practicing cybersecurity and networking
- Building self-hosted infrastructure
- Creating a secure remote-access environment
- Running monitoring, cloud, and NAS services
- Preparing a future cybersecurity lab

This project is designed to be:

Secure
Budget-conscious
Migration-friendly
Scalable
Educational

---

👨‍💻 Author

Azka Erlangga Putra
S1 Teknik Telekomunikasi

Interest Areas:

Cybersecurity
Networking
Linux Administration
Self-Hosting
Server Infrastructure
Homelab

---

🖥️ Hardware

Current server hardware:

Device      : Dell Inspiron 3458
Role        : Home Server
CPU         : Intel Processor
RAM         : (Upgradeable)
Storage     : HDD (future SSD upgrade planned)
OS Hypervisor : Proxmox VE

Upgrade Plan

Planned future upgrades:

✓ Thermal paste replacement
✓ Internal cleaning
✓ LAN cable optimization
⬜ SSD SATA 2.5"
⬜ DDR3L RAM Upgrade
⬜ Battery replacement (if necessary)

---

🎯 Homelab Goals

Priority roadmap:

Phase 1 — Infrastructure

✓ Secure remote access
✓ Virtualization
✓ Domain integration
✓ HTTPS access

Phase 2 — Monitoring

⬜ Uptime Kuma
⬜ Beszel
⬜ Dashboard

Phase 3 — Cybersecurity Lab

⬜ Kali Linux
⬜ Pentesting tools
⬜ Vulnerable environments
⬜ Network analysis

Phase 4 — Cloud / NAS

⬜ Nextcloud
⬜ NAS
⬜ File sharing
⬜ Private cloud

---

🏗️ Current Architecture

Current infrastructure:

Internet
    │
    ▼
Cloudflare DNS
    │
    ▼
Cloudflare Tunnel
    │
    ▼
azka-pve (Proxmox Host)
    │
    └── debian-lab (Debian Core)

Planned future architecture:

Internet
    │
    ▼
Cloudflare
    │
    ▼
Cloudflare Tunnel
    │
    ▼
azka-pve (Proxmox)
│
├── Debian Core
│   ├─ Monitoring
│   ├─ Docker
│   ├─ Nginx
│   ├─ Dashboard
│   ├─ Utility Server
│   └─ SSH Jump Host
│
├── Kali Lab
│   └─ Cybersecurity Lab
│
└── Debian Cloud
    ├─ Nextcloud
    ├─ NAS
    └─ File Storage

---

🖥️ Proxmox Installation

Step 1 — Install Proxmox VE

Proxmox VE was installed on:

Dell Inspiron 3458

Hostname:

azka-pve

Main objective:

Run multiple VMs
Create isolated lab environments
Build secure homelab infrastructure

---

Step 2 — Initial Networking

Initial local access:

https://<local-ip>:8006

After successful configuration:

https://192.168.x.x:8006

Successfully accessed:

✓ Proxmox Web UI
✓ Node management
✓ VM management

---

🌐 Domain Setup

Purchased domains:

azkapve.my.id
azkapve.web.id

Purpose:

.my.id  → infrastructure & homelab
.web.id → future website

---

☁️ Cloudflare Setup

Cloudflare was integrated for:

DNS management
HTTPS encryption
Cloudflare Tunnel
Secure remote access

Configured nameservers:

emma.ns.cloudflare.com
otto.ns.cloudflare.com

Successfully activated:

✓ DNS propagation
✓ Cloudflare integration
✓ HTTPS support

---

🔐 Cloudflare Tunnel Setup

Main purpose:

Secure remote access
without port forwarding

Tunnel created:

proxmox

Tunnel destination:

Proxmox Web UI

Remote URL:

https://proxmox.azkapve.my.id

Cloudflare Tunnel benefits:

✓ No port forwarding
✓ Public IP hidden
✓ HTTPS encryption
✓ More secure access
✓ Accessible anywhere

Successfully tested from:

✓ Different Wi-Fi
✓ Mobile data
✓ Outside local network

---

⚠️ Challenges & Troubleshooting

During setup, multiple issues were encountered.

1. DNS Resolution Problem

Issue:

ERR_NAME_NOT_RESOLVED

Cause:

DNS propagation delay
Local DNS cache

Solution:

ipconfig /flushdns

---

2. Cloudflare Tunnel Error

Issue:

Error 1033
Cloudflare Tunnel Error

Cause:

Tunnel inactive

Solution:

cloudflared tunnel run proxmox

---

3. SSL Certificate Issue

Issue:

ERR_SSL_VERSION_OR_CIPHER_MISMATCH

Cause:

Cloudflare TXT validation issue
Duplicate records

Solution:

Reset DNS validation
Rebuild tunnel
Clean TXT records

---

4. NXDOMAIN Problem

Issue:

NXDOMAIN

Cause:

Local router DNS cache

Solution:

dig proxmox.azkapve.my.id @1.1.1.1

---

🐧 Debian VM Setup

Created VM:

debian-lab

Role:

Debian Core

Current functions:

Monitoring
Docker host
Utility server
Dashboard
SSH jump host
Linux playground

Current status:

✓ Installed
✓ Running
✓ Internet access
✓ SSH access
✓ Reachable remotely

Current IP:

192.168.0.201

---

🧪 Current Progress

Completed:

✓ Proxmox installed
✓ Cloudflare Tunnel working
✓ Remote access working
✓ HTTPS domain working
✓ Debian VM running
✓ SSH remote access
✓ External internet access
✓ Domain & DNS configured

Current working URL:

https://proxmox.azkapve.my.id

---

📅 Next Steps

Planned immediate tasks:

Debian Core Setup

Docker

Install Docker

Monitoring

Uptime Kuma
Beszel

Dashboard

Homepage Dashboard

Web Foundation

Nginx Reverse Proxy

Security

Fail2Ban
Firewall
SSH Hardening

---

🧠 Lessons Learned

Things learned during this project:

Linux server basics
Cloudflare Tunnel
DNS propagation
HTTPS setup
Remote access
Troubleshooting
SSH management
Virtualization
Networking

---

📍 Current Status

Infrastructure Phase:

[✓] Infrastructure Ready
[✓] Remote Access Ready
[✓] Secure HTTPS Access
[✓] First VM Running
[ ] Monitoring Stack
[ ] Cybersecurity Lab
[ ] Cloud/NAS

---

🔥 Future Vision

Long-term homelab vision:

Cybersecurity Lab
VPN Server
Remote Management
Monitoring Infrastructure
Private Cloud
NAS Storage
Network Visibility
Self-hosted Services

Goal:

Build a fully functional cybersecurity-focused homelab
for learning, experimentation, and self-hosting.
