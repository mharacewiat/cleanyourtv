---
name: pihole-dns-for-tv
description: "Unfinished task (started 2026-11-16) — point the Xiaomi TV's DNS at Pi-hole with Livebox fallback via static IP; status and blockers"
metadata:
  node_type: memory
  type: project
  modified: 2026-11-18T17:57:10.538Z
---

Goal (user, 2026-11-16): TV uses Pi-hole, falling back to the router if the homelab is down.

**Plan agreed:** Android 9 has no ADB command for DNS and the Livebox can't push DNS ([[home-network]]), so set the TV's
Wi-Fi to static IP: Settings → Network → Wi-Fi → `<home ssid>` → IP settings → Static —
IP `192.168.1.111`, gateway `192.168.1.1`, prefix `24`, DNS1 `192.168.1.20` (Pi-hole), DNS2 `192.168.1.1`.
Undo = back to DHCP. Private DNS was null (good). Check with
`dumpsys connectivity | grep -oE "DnsAddresses: \[[^]]*\]"` and the Pi-hole query log.

**Status:** user said the Livebox reservation for the TV MAC → `.111` is done (2026-11-16). Static IP **not yet set**.
I opened Wi-Fi settings via `am start` but couldn't see the screen (0-byte screenshots) and it popped over Netflix;
no keys sent, nothing changed. On 2026-11-17 the TV was off the LAN entirely (MAC not in ARP even on the home screen);
asked the user which network it shows. Unresolved — start by asking/ checking whether the TV is back on the LAN and
whether the user already set the static IP with the remote. Recommend the user does it with the remote.
After it works, push for closing ADB ([[tv-cleanup-state]]).
