---
description: Manage AI instruction presets (saved templates with shortcuts)
---

Parse $ARGUMENTS:
- No arguments: `superbased_presets` with `action: "list"` to show all saved presets
- "create NAME INSTRUCTION": `superbased_presets` with `action: "create"`, `name`, and `instruction`
- "delete ID": `superbased_presets` with `action: "delete"` and `id`
- A preset name and new instruction: `superbased_presets` with `action: "update"`, `id`, and `instruction`

Presets are reusable AI instruction templates, optionally bound to keyboard shortcuts.
