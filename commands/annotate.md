---
description: Add annotations (rectangles, arrows, text labels, blur) to a capture
---

Requires a `captureId`. If $ARGUMENTS contains a capture ID, use it. Otherwise, take a fresh screenshot with `superbased_capture_image` first.

Use `superbased_annotate` with the `captureId` and an `annotations` array.

**Annotation types:**
- `rectangle`: `{type:"rectangle", x, y, width, height, color:"#ff0000"}`
- `highlight`: `{type:"highlight", x, y, width, height, color:"#ffff00"}`
- `blur`: `{type:"blur", x, y, width, height}`
- `text`: `{type:"text", x, y, text:"label", color:"#ff0000"}`
- `arrow`: `{type:"arrow", x, y, toX, toY, color:"#ff0000"}`

Parse $ARGUMENTS for annotation instructions (e.g., "circle the error at 100,200", "blur the API key area"). Set `save: true` to save over the original.
