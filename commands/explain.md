---
description: Capture screenshot and get AI analysis
---

1. Use `superbased_capture_image` with `mode: "fullscreen"` and `resolution: "half"`.
2. Use `superbased_ai` with the `captureId` from step 1. Set `instruction` to $ARGUMENTS if provided, otherwise use "/explain".

Supported AI instructions: `/extract` (get text), `/summarize`, `/code` (extract code), `/explain`, `/translate`, `/table` (extract tabular data), `/edit`, `/reformat`.

Return the AI analysis to the user.
