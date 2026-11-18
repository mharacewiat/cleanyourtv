---
name: tv-cleanup-state
description: "What was applied to the user's Xiaomi TV in the Oct 2026 cleanup, where the undo files live, and what is still pending (Private DNS, closing ADB)"
metadata:
  node_type: memory
  type: project
  modified: 2026-11-18T17:56:53.404Z
---

Cleanup done 2026-10-26/27 following PROMPT.md. Full log: `work/LIVE.md` (gitignored). TV: [[tv-xiaomi-mitv-mssp3]].

**Files to keep (all gitignored / outside repo):**
- `work/debloat.txt` — the applied list (copy of the android9 example, user keeps commented out, + `com.google.android.music`).
- `~/.cleanyourtv/recovery-192.168.1.114-76c83b92.json` — disable.sh's undo record (keyed by the *old* IP .114).
- `backup/` — pre-change package lists, getprop, settings, meminfo (baseline: 0 disabled, MemAvailable ~456 MB).
- `shots/` 00–28 screenshots; `work/theme-reduced-motion/config.json` = `{ "reduced_motion": true }`.
- Undo: `TV_HOST=<ip> tools/restore.sh work/debloat.txt com.google.android.tvlauncher`; theme undo `tools/theme.sh --reset`.

**Disabled (18):** miui.tv.analytics, xiaomi.statistic, google.android.feedback, mitv.tvhome.atv (PatchWall),
xm.webcontent, xiaomi.floatingframe, google.android.tvrecommendations, android.autoinstalls.config.xiaomi.amelie,
xiaomi.mitv.tvmanager, google.android.katniss (voice), xiaomi.mimusic2, play.games, google.android.videos, mitv.gallery,
leanbacklauncher, leanbacklauncher.recommendations, google.android.music, google.android.tvlauncher.
Survived reboot; katniss stays off on PI.4663.

**Kept by user choice:** Netflix + netflixobserver, Prime Video, YouTube, Chromecast (mediashell), firmware updater,
Ambient screensaver (backdrop), Media Player (mediaexplorer).

**Tweaks:** animation scales 0.5 (window/transition/animator; restore.sh resets them); launcher `reduced_motion` theme pushed.
Result: MemAvailable ~860–870 MB, swap no longer full. Power-on goes straight to the new launcher.

**Pending:**
- Step 8 Private DNS: became the Pi-hole task, see [[pihole-dns-for-tv]].
- Step 9 close ADB: user said they'd do it themselves "after a couple of days"; still open as of 2026-11-17. Remind them
  (USB debugging off, revoke authorisations, reboot, `tools/adb-closed.py <ip>`).

Launcher dock: [[launcher-dock-config]].
