---
name: launcher-dock-config
description: "The user's personal launcher config (dock apps) lives as a local commit on branch `home`; how the launcher was installed"
metadata:
  node_type: memory
  type: project
  modified: 2026-11-18T17:56:57.988Z
---

`launcher/app/src/main/res/values/config.xml` `dock_apps` = Netflix, YouTube (`com.google.android.youtube.tv`),
Disney+ (`com.disney.disneyplus`), Max (`com.wbd.stream`) — replaced the defaults Prime Video and Hotstar.
Committed on local branch `home` as `0710b481 chore: local changes` (2026-11-18). Never push this / never put it in a PR.
When rebasing `home` onto a newer `main`, keep this commit on top.

Install: `TV_HOST=<ip> launcher/build-and-install.sh`. On 2026-10-27 the Claude Code permission classifier blocked it
("Modify Shared Resources"), so the **user ran it themselves** with `!`; expect the same and offer the command.
After install, verify Home via `dumpsys activity activities | grep mFocusedApp`, and ask the user to press the real
remote Home / Input / Netflix buttons (they worked). Related: [[tv-cleanup-state]].
