---
description: Take a screenshot (fullscreen, window, or region)
---

Use `superbased_capture_image` to take a screenshot.

**Defaults:** `mode: "fullscreen"`, `resolution: "half"` (saves ~4x tokens vs full).

**Based on $ARGUMENTS:**
- No arguments: fullscreen capture at half resolution
- A window name (e.g., "Chrome", "VS Code"): first call `superbased_window_list` to verify the window exists, then capture with the `window` parameter
- Coordinates like "100,200 300x200": use `mode: "region"` with x, y, width, height
- "full" or "high-res": use `resolution: "full"`
- "quarter" or "thumbnail": use that resolution for minimal token usage

After capturing, briefly describe what you see and note the capture ID for future reference.
