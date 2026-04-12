---
description: Capture screenshot and extract text via OCR
---

1. Use `superbased_capture_image` with `mode: "fullscreen"` and `resolution: "half"` to take a screenshot.
2. Use `superbased_ocr` with the `captureId` from step 1 to extract all text.
3. Return the extracted text in a code block.

If $ARGUMENTS specifies a window name, capture that window instead. If $ARGUMENTS asks about specific content, highlight the relevant parts.

**Alternative (faster, AI-powered):** `superbased_ai` with `instruction: "/extract"` does capture + extraction in one step.
