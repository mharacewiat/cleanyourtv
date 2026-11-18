---
name: eufy-cameras
description: "User's eufy cameras and the 2026-11-03 conclusion on showing snapshot tiles/live view on the TV (research only, nothing built)"
metadata:
  node_type: memory
  type: project
  modified: 2026-11-18T17:57:15.738Z
---

Cameras: **S120 Solar Wall Light Cam** (battery+solar, outdoor), **S100 Wired Wall Light Cam** (outdoor). Planned: **HomeBase 3**
and **Indoor Cam E30** (wired). Wanted: eufy-app-like tiles with last snapshot, live only on OK — *not* an always-live
home-screen strip (security concern). No Home Assistant, no Pi/NAS/always-on machine.

Conclusion: S120/S100 have no RTSP and poor `eufy_security`/HA support → no open way to get their picture onto the TV.
E30s likely support RTSP — check before buying (app: Camera settings → Storage → RTSP/NAS). If so, a TV-only add-on
(in `addons/`, last-viewed frame on tile, OK → RTSP live, Back disconnects) could work for them. Zero-effort fallback:
Google Home + "Hey Google, show …" — but katniss (Assistant) was disabled in [[tv-cleanup-state]].
Repo option if HA ever exists: add a Cameras section to `addons/smart-home`. Don't recommend buying a Pi for this.
