---
description: Extract text from a screenshot or image file using local OCR
---

If $ARGUMENTS contains a file path, use `superbased_ocr` with `screenshotPath` set to that path.

If $ARGUMENTS contains a capture ID, use `superbased_ocr` with that `captureId`.

Otherwise, take a screenshot first with `superbased_capture_image` (fullscreen, half resolution), then run `superbased_ocr` on the result.

OCR runs locally via Tesseract -- no data leaves the machine. Return extracted text in a code block.
