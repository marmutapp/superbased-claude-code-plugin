---
description: Transcribe an audio file to text (raw Whisper, no cleanup)
---

Use `superbased_transcribe` with `audioPath` set to the file path in $ARGUMENTS.

If $ARGUMENTS contains a language code (e.g., "en-US"), pass as `language`.

Returns raw Whisper transcription without filler word removal or cleanup. For cleaned-up transcription with filler removal, use `/superbased:dictate` instead.

Supported formats: wav, mp3, webm.
