---
description: Browse, search, and manage capture gallery
---

Parse $ARGUMENTS:
- A search query: `superbased_gallery` with `action: "search"` and `query` set to $ARGUMENTS
- A capture ID number: `superbased_gallery` with `action: "get"` and that `captureId`
- "stats": `superbased_gallery` with `action: "stats"`
- No arguments: `superbased_gallery` with `action: "list"` and `limit: 10`

Include capture IDs, timestamps, and tags in the output so the user can reference specific captures. Use `superbased_gallery_image` to view a saved capture's image.
