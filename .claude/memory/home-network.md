---
name: home-network
description: "User's home LAN — Orange Livebox 6+, address plan, guest net, homelab (Proxmox, Pi-hole, k3s) addresses; source docs in ~/Projects/homelab"
metadata:
  node_type: memory
  type: reference
  modified: 2026-11-18T17:57:04.141Z
---

Source of truth: `~/Projects/homelab/docs/network.md` and `docs/pihole.md` (re-read; values below as of 2026-11-16).

- Router: **Orange Livebox 6+**, gateway `192.168.1.1`, LAN `192.168.1.0/24`, main Wi-Fi SSID `<home ssid>`.
  Web UI in Spanish (configuración avanzada → configuración de la red → DHCP → dirección IP estática).
  Read-only helper: `~/Projects/dotfiles/livebox`. Reservations are added by the user in the web UI.
- DHCP pool `.10–.150`. Address plan: `.10–.29` computers/homelab, `.30–.39` printers, `.40–.49` gaming,
  `.50–.99` mobiles (`.50` = a phone), **`.100–.149` IoT** (TV belongs here), `.150+` other.
- Guest network `172.30.1.0/24` (unreachable from the laptop).
- Livebox DHCP **cannot hand out a custom DNS server** → Pi-hole must be set per device.
- Homelab: Proxmox `192.168.1.13` (`pve.home.arpa`), **Pi-hole LXC `192.168.1.20`** (CT 120), k3s server `.21`, agent `.22`.
  Pi-hole blocks e.g. `doubleclick.net` (verified with `nslookup doubleclick.net 192.168.1.20`).
- Earlier ARP neighbours seen: `.10`, `.30`. TV: see [[tv-xiaomi-mitv-mssp3]].
