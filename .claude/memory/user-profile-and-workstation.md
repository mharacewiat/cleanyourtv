---
name: user-profile-and-workstation
description: "Who the user is in this repo (fork user cleaning their own TV, not a contributor) and their Linux workstation/toolchain setup"
metadata:
  node_type: memory
  type: user
  modified: 2026-11-18T17:56:31.593Z
---

**Role here:** forked and cloned Gathin23/cleanyourtv (2026-10-26) to clean *their own* TV, not to contribute.
Local branch `home` (ahead of `main`) holds personal commits, e.g. `0710b481 chore: local changes` = dock config
(see [[launcher-dock-config]]). Separate homelab project at `~/Projects/homelab` (see [[home-network]]).

**Household:** family uses the TV daily. Has eufy cameras (see [[eufy-cameras]]).

**Workstation:** Ubuntu 24.04 laptop, Wi-Fi iface `wlp2s0`, login shell fish (Bash tool runs bash). No passwordless
sudo — system installs (apt) must be run by the user. Installed for this repo (2026-10-27):
- openjdk-17-jdk 17.0.20.1 (has jlink)
- Android SDK at `~/Android/Sdk` (cmdline-tools/latest, platforms;android-34, build-tools;34.0.0); `launcher/local.properties` points there
- `tools/venv` with `tools/requirements.txt` (adb-shell). **No stock `adb` binary** — use `tools/venv/bin/python tools/tv.py`.
- ADB key in `tools/adbkey/` (gitignored), trusted on the TV with "Always allow".
- Launcher test build works: `ANDROID_HOME=~/Android/Sdk ./gradlew --no-daemon assembleRelease` (~1.5 min, APK ~535 KB).
  Harmless warning "SDK XML version 4" from cmdline-tools mismatch.

**Preferences:** wants the repo author's documented procedure followed exclusively ("don't reinvent anything"),
fail early, backups first, a local live log (`work/LIVE.md`); for new features prefers native, community-driven,
opinionated solutions with minimal tinkering. See [[tv-writes-need-approval]].
