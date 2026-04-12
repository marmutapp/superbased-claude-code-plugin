---
description: Read or write system clipboard (text or image)
---

Parse $ARGUMENTS:
- "read" or no arguments: `superbased_clipboard` with `action: "read"` to get clipboard text
- "image" or "screenshot" or "paste": `superbased_clipboard` with `action: "readImage"` to see what image is on the clipboard
- Any other text: `superbased_clipboard` with `action: "write"` and `text` set to $ARGUMENTS

For `readImage`, describe what you see in the clipboard image.
