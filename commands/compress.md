---
description: Compress text into token-efficient images via the Token Compression Engine
---

Use `superbased_compress_text` with `text` set to $ARGUMENTS.

**Auto-select theme based on content:**
- CLI output, build logs: `theme: "terminal"`
- Source code, config: `theme: "dark"`
- Documentation, prose: `theme: "paper"`
- General/mixed text: `theme: "light"`
- Accessibility: `theme: "high-contrast"`

Leave `preset`, `columns`, and `render_style` as "auto" unless specified.

Report the compression ratio and token savings. Formula: `image_tokens = (width x height) / 750`.
