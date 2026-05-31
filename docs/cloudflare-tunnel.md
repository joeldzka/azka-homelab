Cloudflare Tunnel Documentation

This document explains the setup process for Cloudflare Tunnel used in this homelab to securely expose internal services to the internet without port forwarding.

---

📌 Objective

Main objective:

Secure remote access to Proxmox
without exposing home public IP
and without opening router ports.

Service exposed:

Proxmox Web UI

Public URL:

https://proxmox.azkapve.my.id

---

🏗️ Architecture

Tunnel flow:

Laptop / Phone
        │
        ▼
Cloudflare DNS
        │
        ▼
Cloudflare Tunnel
        │
        ▼
azka-pve (Proxmox)
        │
        ▼
localhost:8006

This setup allows secure access from:

✓ Mobile Data
✓ Different Wi-Fi
✓ Outside Local Network
✓ Remote Internet Access

without:

✗ Port Forwarding
✗ Exposed Public IP
✗ VPN Requirement

---

🌐 Domain Setup

Domain used:

azkapve.my.id

Cloudflare nameservers:

emma.ns.cloudflare.com
otto.ns.cloudflare.com

Cloudflare became the authoritative DNS provider.

---

☁️ Install Cloudflared

Installed on:

azka-pve (Proxmox Host)

Update package:

apt update && apt upgrade -y

Install Cloudflared:

curl -fsSL https://pkg.cloudflare.com/install.sh | bash
apt install cloudflared -y

Verify installation:

cloudflared --version

---

🔐 Login to Cloudflare

Login process:

cloudflared tunnel login

A browser window opens for authentication.

Selected zone:

azkapve.my.id

Successful login generates:

/root/.cloudflared/cert.pem

---

🚇 Create Tunnel

Tunnel created:

proxmox

Command:

cloudflared tunnel create proxmox

Tunnel ID generated:

21efc470-1f03-4ab9-b6ef-3fce74e3295b

Credential file generated:

/root/.cloudflared/21efc470-1f03-4ab9-b6ef-3fce74e3295b.json

---

🌍 Configure DNS Route

Create DNS route:

cloudflared tunnel route dns proxmox proxmox.azkapve.my.id

Expected result:

Added CNAME proxmox.azkapve.my.id

---

⚙️ Tunnel Configuration

Configuration file:

/etc/cloudflared/config.yml

Configuration:

tunnel: 21efc470-1f03-4ab9-b6ef-3fce74e3295b
credentials-file: /root/.cloudflared/21efc470-1f03-4ab9-b6ef-3fce74e3295b.json

ingress:
  - hostname: proxmox.azkapve.my.id
    service: https://localhost:8006
    originRequest:
      noTLSVerify: true

  - service: http_status:404

---

▶️ Run Tunnel

Manual test:

cloudflared tunnel run proxmox

Expected result:

INF Registered tunnel connection

---

🔄 Auto Start Service

Enable automatic startup:

cloudflared service install
systemctl enable cloudflared
systemctl start cloudflared

Check service:

systemctl status cloudflared

Expected:

active (running)

---

🧪 Verification

DNS verification:

dig proxmox.azkapve.my.id @1.1.1.1

Expected:

Cloudflare IP addresses returned

Tunnel verification:

https://proxmox.azkapve.my.id

Expected:

Proxmox login page appears

---

⚠️ Troubleshooting

Error: ERR_NAME_NOT_RESOLVED

Cause:

DNS cache issue

Fix:

Windows

ipconfig /flushdns

Linux

dig proxmox.azkapve.my.id @1.1.1.1

---

Error 1033 — Cloudflare Tunnel Error

Cause:

Tunnel offline

Fix:

cloudflared tunnel run proxmox

---

SSL Certificate Error

Error:

ERR_SSL_VERSION_OR_CIPHER_MISMATCH

Cause:

Duplicate TXT validation records

Fix:

Delete duplicate TXT DNS records
Reset tunnel
Rebuild DNS route

---

NXDOMAIN

Cause:

Local router DNS cache

Fix:

dig proxmox.azkapve.my.id @1.1.1.1

---

✅ Final Result

Successfully achieved:

✓ Secure remote access
✓ HTTPS encryption
✓ No port forwarding
✓ Public IP hidden
✓ Remote Proxmox access
✓ Access from outside local network

Final URL:

https://proxmox.azkapve.my.id
