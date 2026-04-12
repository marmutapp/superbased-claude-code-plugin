# SuperBased — Give Claude Code Eyes on Your Screen

Screenshot capture, AI vision, OCR, screen recording, visual regression testing, token compression, voice dictation, and proactive screen monitoring — all via 28 MCP tools, directly inside Claude Code.

## Install

### Option 1: From Marketplace

```
/plugin marketplace add AskSuperBased/claude-code-plugin
/plugin install superbased@superbased-tools
```

### Option 2: Local Plugin

```
claude --plugin-dir /path/to/superbased/plugin
```

### Option 3: MCP Server Only

Add to your project's `.mcp.json`:

```json
{
  "superbased": {
    "command": "superbased",
    "args": ["mcp"]
  }
}
```

## Prerequisites

- **SuperBased desktop app** running (Windows or macOS), OR
- **SuperBased CLI** installed globally: `npm install -g superbased`
- Node.js 20+

## Slash Commands (22)

| Command | Description |
|---------|-------------|
| `/superbased:capture` | Take a screenshot (fullscreen, window, or region) |
| `/superbased:window` | List open windows or capture a specific window |
| `/superbased:extract` | Capture + OCR to extract text from screen |
| `/superbased:explain` | Capture + AI analysis of what's on screen |
| `/superbased:ocr` | Extract text from screenshot or image file (local Tesseract) |
| `/superbased:clipboard` | Read or write system clipboard (text or image) |
| `/superbased:annotate` | Add rectangles, arrows, text labels, blur to captures |
| `/superbased:redact` | Auto-redact secrets and PII from screenshots |
| `/superbased:record` | Start, stop, or manage screen recording sessions |
| `/superbased:monitor` | Start proactive AI screen monitoring |
| `/superbased:sessions` | List recording sessions and view frames |
| `/superbased:diff` | Compare two recording sessions for visual regressions |
| `/superbased:baseline` | Manage visual regression testing baselines |
| `/superbased:export` | Export sessions as zip, markdown, PDF, HTML, or GIF |
| `/superbased:gallery` | Browse, search, and manage capture gallery |
| `/superbased:compress` | Compress text into token-efficient images |
| `/superbased:dictate` | Record from microphone and transcribe |
| `/superbased:transcribe` | Transcribe audio file to text (raw Whisper) |
| `/superbased:settings` | View or update app settings |
| `/superbased:presets` | Manage AI instruction presets |
| `/superbased:status` | Health, auth, and AI usage check |
| `/superbased:auth` | Authentication management |

## Skills (7)

Skills are invoked automatically by Claude when relevant to the task.

| Skill | When Claude Uses It |
|-------|-------------------|
| **screenshot** | Claude needs to see the screen to answer a question or verify a UI change |
| **visual-qa** | Visual regression testing: record baseline, make changes, record again, diff |
| **monitor** | Proactive screen watching during deploys, tests, or builds |
| **compress** | Large text content (>500 tokens) that would be cheaper as an image |
| **redact** | Screenshots that may contain API keys, tokens, or PII before sharing |
| **dictation** | User wants voice input, audio transcription, or speech-to-text |
| **annotate** | Highlighting areas, marking regressions, creating annotated screenshots |

## Agents (2)

Dedicated agents for complex multi-step workflows.

| Agent | Description |
|-------|-------------|
| **visual-qa** | Record baselines, capture after changes, diff, annotate regressions, export reports |
| **monitor** | Watch screen for errors during deploys/tests, flag issues proactively, summarize findings |

## Hooks

**Post-test auto-capture:** After any test command (`npm test`, `jest`, `vitest`, `pytest`, `cargo test`, `go test`), SuperBased automatically captures a screenshot at quarter resolution. This builds a visual history of test runs without manual intervention.

## MCP Tools (28)

The plugin exposes all 28 SuperBased MCP tools:

**Capture & View:** `superbased_capture`, `superbased_capture_image`, `superbased_clipboard`, `superbased_window_list`
**AI & OCR:** `superbased_ai`, `superbased_ai_usage`, `superbased_ocr`, `superbased_transcribe`, `superbased_compress_text`
**Gallery:** `superbased_gallery`, `superbased_gallery_update`, `superbased_gallery_image`
**Recording:** `superbased_recording`, `superbased_sessions`, `superbased_export`, `superbased_describe_frames`, `superbased_narrate`
**Visual Testing:** `superbased_diff`, `superbased_baseline`, `superbased_annotate`
**Dictation:** `superbased_dictate`, `superbased_dictation_history`
**Privacy:** `superbased_redact`
**Settings:** `superbased_settings`, `superbased_presets`
**Auth & System:** `superbased_auth`, `superbased_license`, `superbased_health`

## Token Savings

SuperBased optimizes token usage with resolution control:

| Resolution | 1080p Tokens | Savings vs Full |
|------------|-------------|-----------------|
| `full` | ~2,765 | baseline |
| `high` | ~1,382 | 2x |
| `half` | ~691 | 4x |
| `quarter` | ~173 | 16x |
| `thumbnail` | ~43 | 64x |

The Token Compression Engine converts large text blocks into optimized images, saving tokens when `image_tokens < text_tokens` (typically for content >500 tokens).

## Examples

### See what's on screen
```
/superbased:capture
```

### Capture a specific window
```
/superbased:window Chrome
```

### Monitor a deploy for errors
```
/superbased:monitor Flag any errors, failed health checks, or 500 status codes
```

### Visual regression test
```
/superbased:record login-flow-baseline
(navigate the login UI)
/superbased:record stop
/superbased:baseline set login-flow <session-id>
(make code changes)
/superbased:record login-flow-after
(navigate the same flow)
/superbased:record stop
/superbased:diff <baseline-id> <after-id>
```

### Redact and share a screenshot
```
/superbased:capture
/superbased:redact <capture-id>
```

## Links

- [SuperBased](https://superbased.app) — Desktop app download
- [npm package](https://www.npmjs.com/package/superbased) — Headless CLI
- [MCP Integration Guide](https://github.com/AskSuperBased/superbased/blob/main/docs/MCP_INTEGRATION_GUIDE.md) — Setup for all AI editors
