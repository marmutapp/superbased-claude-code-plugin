---
description: Record from microphone and transcribe speech to text
---

Use `superbased_dictate` with `mic: true` and `cleanup: true`.

Default `duration` to 10 seconds. If $ARGUMENTS contains a number (e.g., "30"), use that as `duration`. If $ARGUMENTS contains a language code (e.g., "en-US"), pass as `language`.

Return the transcribed text. If the user asked to dictate into a file, write the transcription to the specified path.

Requires a microphone and SoX (headless) or the desktop app's audio capture.
