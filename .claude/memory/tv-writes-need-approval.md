---
name: tv-writes-need-approval
description: "Any write/flash/state-changing operation on the user's TV needs explicit per-step approval; work step by step, revertable"
metadata:
  node_type: memory
  type: feedback
  modified: 2026-11-18T17:57:20.747Z
---

Never run a write or state-changing command on the user's TV (pm disable-user, installs, settings put, reboot, theme push, disable.sh, build-and-install.sh, `am start` of a screen, key injection) without the user explicitly approving that step first. Read-only commands (getprop, pm list, dumpsys, screencap/screenshot, backups pulled to the computer) are fine.

**Why:** User said mid-session (2026-10-26, Xiaomi MiTV-MSSP3 cleanup): "Any write/flash operation to my TV need to be approved by me." Also: "carefully, step by step, revertable — i need my tv to stay operational so rollback when an error comes out and you can't carry on." The family uses the TV; an `am start` once popped Settings over Netflix.

**How to apply:** Present the exact command(s)/list for each batch, wait for a yes, then run. Approval for one batch does not cover the next. A reboot authorisation ("authorized to reboot when needed", 2026-10-27) was given for that cleanup session — re-confirm in new sessions. Check `mCurrentFocus` before anything that changes the screen. See [[tv-xiaomi-mitv-mssp3]].
