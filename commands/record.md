---
description: Start, stop, or manage a screen recording session
---

Parse $ARGUMENTS:
- "stop": `superbased_recording` with `action: "stop"`, report the session summary
- "status": `superbased_recording` with `action: "status"`
- "pause" / "resume": use the corresponding action
- Otherwise: start a new recording

**Starting a recording:**
Use `superbased_recording` with `action: "start"`, `mode: "smart"`, `profile: "automated_test"`.

If $ARGUMENTS contains:
- A session name: pass as `name`
- "monitor": use `mode: "monitor"` with `analysisPrompt: "Flag any errors, warnings, or unexpected states"`
- "periodic": use `mode: "periodic"`
- A number (e.g., "5s"): use as `interval`

Report the session ID so the user can reference it later.
