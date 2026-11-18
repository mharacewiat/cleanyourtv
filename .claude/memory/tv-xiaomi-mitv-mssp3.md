---
name: tv-xiaomi-mitv-mssp3
description: "The user's TV — Xiaomi Mi TV 4S MiTV-MSSP3, Android 9 PI.4663 — identity, how to connect, installed apps, and firmware quirks learned the hard way"
metadata:
  node_type: memory
  type: project
  modified: 2026-11-18T17:56:44.441Z
---

**Device:** Xiaomi Mi TV 4S, global/Spanish variant, model `MiTV-MSSP3`, device `machuca`, board/platform `m7322`
(MediaTek/MStar), **Android 9, SDK 28, firmware `PI.4663`** (fingerprint Xiaomi/machuca/machuca:9/PI/4663).
1920x1080 @ 320 dpi, RAM 1.8 GB, swap 200 MB (zram, not changeable without root). `ro.adb.secure=1`.
Reference list in repo: `examples/xiaomi-mitv-mssp3-android9/` (its PI.4663 notes apply). The other folder
`examples/xiaomi-mitv-mssp3` is the Android 11 firmware — not ours.

**Network:** Wi-Fi only (nothing on USB). Wi-Fi MAC `<tv wifi mac>`. IP via Livebox DHCP: was `192.168.1.114`
(Oct 2026), became `192.168.1.111` by 2026-11-16 → always re-check; find via `ip neigh | rg -i <tv wifi mac>`.
See [[home-network]], [[pihole-dns-for-tv]].

**Connecting:** USB debugging alone opens 5555 (no separate network-debugging toggle). As of 2026-11-17 ADB is still
open (user deferred closing it). Usage: `TV_HOST=<ip> tools/venv/bin/python tools/tv.py '<shell cmd>'`, `--probe`,
`--screenshot shots/x.png`, `--reboot`. A new key needs the on-screen "Allow USB debugging" + "Always allow".

**Key packages:** Live TV `com.mediatek.wwtv.tvcenter`; stock launcher `com.google.android.tvlauncher` (now disabled);
Home now `com.gathin.tvhome/.MainActivity`; IME Gboard; screensaver `com.google.android.backdrop` (kept).
User apps: Spotify, Max (`com.wbd.stream`), Surfshark VPN (installed, not always-on), TVP VOD, Disney+ (`com.disney.disneyplus`), RTVE.
**Never launch:** `mediatek.factorymenu.ui`, `com.mediatek.tv.factory`.

**Firmware quirks (important):**
- Disabling several packages in one burst crashed `system_server` (SIGSEGV in libbinder `BpBinder::reportOneDeath`),
  soft reboot, disables not persisted, **and the TV forgot its saved Wi-Fi** (user had to re-enter it → ADB lost).
  → Disable **one package per run**, check system_server pid / Wi-Fi / Home between each.
- `com.google.android.tvrecommendations` must only be disabled after tvlauncher is gone (tvlauncher holds its provider).
- Screenshots return 0 bytes over Settings, Live TV and Netflix; `uiautomator dump` only shows the Live TV layer.
  So you can't drive Settings menus blind safely — ask the user to use the remote.
- Drops off Wi-Fi in standby/when off (no route to host, ARP FAILED). After power-on it may not rejoin; on 2026-11-17 it
  wasn't on the LAN at all even on the home screen (unresolved).
- `am start` of a Settings screen pops over whatever the family is watching — check `mCurrentFocus` first.
- `settings put global background_process_limit` has no effect on Android 9.
- `com.mstar.netflixobserver` starts Netflix at boot (~130 MB) — kept by user choice.

Cleanup state: [[tv-cleanup-state]].
