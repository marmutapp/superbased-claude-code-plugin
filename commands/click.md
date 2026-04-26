---
description: Click an on-screen element by label, role, or coordinates
---

Use `superbased_click` to click a UI element on the user's screen. Always pass `confirm: true`.

**Reliability pyramid — pick the most stable target you can find:**
1. `automationId` (Windows AutomationId / macOS AXIdentifier) — never changes
2. `role` + `name` (e.g. `role: "button", name: "Submit"`) — survives layout changes
3. Visible text/label only — brittle on minor wording tweaks
4. `coords: { x, y }` — last resort, survives nothing

**Workflow when starting fresh on an app:**
1. Call `superbased_ui_dump` first to see the AX tree (returns `automationId` / `role` / `name` / `center.{x,y}` for every element).
2. Pick the most reliable target from the dump.
3. Call `superbased_click` with that target.

**Based on $ARGUMENTS:**
- A button label (e.g. "Submit", "OK", "Cancel"): try `name: "<label>", role: "button"` first
- A text label (e.g. "Email"): try as `name`; if it's a label adjacent to a field you actually want to click, find the field's `automationId` via `_ui_dump`
- "x,y" coordinates: pass as `coords: { x, y }` — only when AX has no entry for the target
- A hint like "primary action" / "submit button": call `_ui_dump` first, identify, then click

**Humanization:** default `humanize: 'light'` is fine for most apps. Bump to `'human'` for sites with bot detection — see the **humanization** skill.

**After clicking, capture a screenshot** (`superbased_screenshot`, `resolution: "half"`) to verify the click reached the intended end-state. The audit log shows your action; the screenshot shows the outcome.
