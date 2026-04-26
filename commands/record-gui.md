---
description: Record a multi-step GUI workflow as a replayable sequence
---

Use this command to compose a multi-step GUI workflow for the user — the result is a `superbased_sequence` that can be replayed later via `superbased_replay`.

**This is for GUI workflow automation.** For visual-regression recording sessions (capture frames over time, then `_diff` against a baseline), use `/superbased:record` instead.

**Workflow:**
1. Ask the user what the workflow should do (or parse from `$ARGUMENTS`).
2. Walk through the UI step-by-step:
   - `superbased_ui_dump` to discover targets
   - For each user action, plan the corresponding tool call: `_click` / `_type` / `_hotkey` / `_scroll` / `_drag` / `_form_fill` / `_dialog_handle`
3. Compose a single `superbased_sequence` with all steps:
   ```json
   {
     "confirm": true,
     "steps": [
       { "type": "click", "name": "File", "role": "menuitem" },
       { "type": "click", "name": "Open...", "role": "menuitem" },
       { "type": "type", "text": "/path/to/file" },
       { "type": "hotkey", "keys": "Enter" },
       { "type": "screenshot", "resolution": "half" }
     ],
     "saveAs": "<workflow-name>"
   }
   ```
4. **Always end with a `screenshot` step** — without it you have no proof the sequence reached the intended state.
5. Pass `saveAs: "<name>"` to persist the sequence; the user can later replay with `superbased_replay name="<name>"`.

**Before firing the sequence, offer dry-run:**
- `superbased_dry_run` simulates each step without firing input events. Use it to validate target resolution and step ordering before the real run, especially on flows that touch destructive UI (delete buttons, send-money, publish-post).

**Humanization:** set on the sequence root (`humanize: "light" | "human" | "paranoid"`). Override per-step if needed. See the **humanization** skill.

After the sequence completes, report: success/failure of each step, the final screenshot, and the saved name (if any) for future replay.
