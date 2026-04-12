---
description: Auto-redact secrets and PII from screenshots before sharing
---

If $ARGUMENTS contains a capture ID, use `superbased_redact` with that `captureId`.
If $ARGUMENTS contains a file path, use `superbased_redact` with that `screenshotPath`.
Otherwise, take a fresh screenshot first with `superbased_capture_image`.

**Default:** `secrets: true` (API keys, tokens, passwords), `pii: false`.

If $ARGUMENTS mentions "pii", "email", "phone", or "personal": also set `pii: true`.

Report how many regions were found and redacted. The tool returns the redacted image inline.
