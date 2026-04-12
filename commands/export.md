---
description: Export a recording session as zip, markdown, PDF, HTML, or GIF
---

Use `superbased_export` with a `sessionId` and `format`.

If $ARGUMENTS contains a session ID, use it. Otherwise, list sessions with `superbased_sessions` and ask which to export.

**Formats:**
- "zip": full archive with all frames and metadata
- "markdown" or "md": markdown report with embedded images
- "pdf": PDF document
- "html": interactive HTML report
- "gif": animated GIF of all frames

Default to "markdown" if no format specified. If $ARGUMENTS mentions a format, use it.

Consider running `superbased_redact` on the session before exporting if it may contain sensitive data.
