Troubleshooting Documentation

This document contains all issues encountered during the homelab setup process and how they were solved.

The purpose of this documentation is:

Avoid repeating mistakes
Speed up recovery
Help future troubleshooting
Serve as reinstall reference

---

📌 Environment

Infrastructure:

Proxmox Host : azka-pve
VM           : debian-lab
Domain       : azkapve.my.id
Remote URL   : proxmox.azkapve.my.id
Provider     : Cloudflare Tunnel

---

❌ Problem 1 — SSL Certificate Error

Error

Browser displayed:

ERR_SSL_VERSION_OR_CIPHER_MISMATCH

---

Symptoms

Cloudflare tunnel active
Domain resolves
Website inaccessible
HTTPS failed

---

Root Cause

Problem caused by:

Duplicate TXT validation records
for _acme-challenge

Multiple old DNS TXT entries existed.

Example:

JzWN...
uCaXj...
7fDb...
dJp89...

Cloudflare certificate validation became inconsistent.

---

Diagnosis

Check TXT records:

dig TXT _acme-challenge.azkapve.my.id @1.1.1.1

Problematic output:

Multiple TXT records detected
Duplicate validation entries

---

Solution

Fix steps:

Delete duplicate TXT records
Clean Cloudflare DNS
Rebuild tunnel setup
Reconfigure DNS routing

Result:

HTTPS successfully restored

---

❌ Problem 2 — Tunnel Error 1033

Error

Cloudflare page displayed:

Error 1033
Cloudflare Tunnel Error

---

Symptoms

DNS works
Cloudflare resolves domain
Tunnel unavailable

---

Root Cause

Tunnel service not connected.

Either:

Tunnel stopped
Cloudflared not running
Broken configuration

---

Diagnosis

Run:

cloudflared tunnel run proxmox

If tunnel not active:

Cloudflare returns Error 1033

---

Solution

Start tunnel manually:

cloudflared tunnel run proxmox

Enable auto start:

cloudflared service install
systemctl enable cloudflared
systemctl start cloudflared

Verification:

systemctl status cloudflared

Expected:

active (running)

---

❌ Problem 3 — ERR_NAME_NOT_RESOLVED

Error

Browser displayed:

ERR_NAME_NOT_RESOLVED

---

Symptoms

Domain inaccessible
DNS lookup fails

---

Root Cause

Usually caused by:

Windows DNS cache
Router DNS cache
Cloudflare propagation delay

---

Diagnosis

Check local DNS:

nslookup proxmox.azkapve.my.id

Check Cloudflare DNS directly:

dig proxmox.azkapve.my.id @1.1.1.1

If:

1.1.1.1 works
but local DNS fails

Then:

local DNS cache issue

---

Solution

Flush Windows DNS:

ipconfig /flushdns

Renew IP:

ipconfig /release
ipconfig /renew

Alternative:

Use Cloudflare DNS

1.1.1.1
1.0.0.1

---

❌ Problem 4 — NXDOMAIN

Error

DNS response:

NXDOMAIN

---

Symptoms

Domain not found
No DNS answer

---

Root Cause

Local router DNS still cached:

old DNS state

while Cloudflare authoritative DNS already updated.

---

Diagnosis

Check:

dig proxmox.azkapve.my.id

May fail because:

router DNS cache

Check authoritative DNS:

dig proxmox.azkapve.my.id @1.1.1.1

If:

NOERROR

then Cloudflare is already correct.

---

Solution

Wait propagation:

1–30 minutes

or change DNS to:

1.1.1.1
8.8.8.8

---

❌ Problem 5 — Existing DNS Route Conflict

Error

Cloudflare returned:

An A, AAAA, or CNAME record
with that host already exists

---

Root Cause

Old tunnel DNS record existed:

proxmox.azkapve.my.id

---

Solution

Delete old DNS record:

proxmox.azkapve.my.id

Then rerun:

cloudflared tunnel route dns proxmox proxmox.azkapve.my.id

Expected:

Added CNAME proxmox.azkapve.my.id

---

❌ Problem 6 — Missing Tunnel Credential

Error

Tunnel commands failed.

---

Root Cause

Credentials removed:

/root/.cloudflared/*

deleted:

cert.pem

---

Solution

Re-login:

cloudflared tunnel login

Reauthenticate:

azkapve.my.id

Then recreate tunnel.

---

🧠 Lessons Learned

Important lessons from this setup:

Always verify DNS using 1.1.1.1
DNS propagation takes time
Cloudflare cache can mislead
Tunnel debugging starts with cloudflared
Do not panic during DNS failures
Remote access without port forwarding is possible

---

✅ Final Status

Successfully fixed:

✓ SSL mismatch
✓ Error 1033
✓ ERR_NAME_NOT_RESOLVED
✓ NXDOMAIN
✓ Tunnel failures
✓ DNS conflicts
✓ TXT validation issue

Final result:

https://proxmox.azkapve.my.id

Accessible securely from anywhere.
