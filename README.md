# SuperBased — Eyes AND Hands for Claude Code

Screenshot capture, AI vision, OCR, screen recording, visual regression testing, token compression, voice dictation, proactive screen monitoring, **and full GUI automation with humanization v2** — all via 72 MCP tools, directly inside Claude Code.

## Install

### Option 1: From Marketplace

```
/plugin marketplace add marmutapp/superbased-claude-code-plugin
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

## Recommended: auto-approve SuperBased tools

Claude Code prompts for approval on every MCP tool call by default. For GUI-automation flows (click / type / scroll / drag / sequence / ui_dump) each prompt also steals focus back to the Claude Code window — so 20 tool calls = 20 focus breaks. Add this to `.claude/settings.json` (project) or `~/.claude/settings.json` (global) to auto-approve all SuperBased tools:

```json
{
  "permissions": {
    "allow": ["mcp__superbased"]
  }
}
```

Safe: the SuperBased server still enforces its own gates (`guiAutomation.enabled` master toggle + per-action toggles + `confirm: true` + protected-apps blocklist + NDJSON audit log). Auto-approving in Claude Code only bypasses the redundant host-side prompt, not the underlying safety rail.

## Slash Commands (26)

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
| `/superbased:click` | Click an on-screen element by label or coordinates |
| `/superbased:form` | Fill a form by label/value pairs (`superbased_form_fill`) |
| `/superbased:record-gui` | Record a multi-step GUI workflow for replay |
| `/superbased:captcha` | Open the CAPTCHA-solving guidance (rotation puzzles, drag puzzles, image grids) |

## Skills (11)

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
| **walkthrough** | Multi-frame product walkthrough: capture, narrate, export |
| **gui-automation** | "Click that", "type into this", "fill the form" — drives the desktop with click/type/hotkey/scroll/drag/form-fill/sequence |
| **captcha-solving** | reCAPTCHA / Cloudflare Turnstile / drag puzzles / rotation puzzles / image grids |
| **humanization** | Sites with bot detection — picks the right humanization profile (off/light/human/paranoid) |

## Agents (3)

Dedicated agents for complex multi-step workflows.

| Agent | Description |
|-------|-------------|
| **visual-qa** | Record baselines, capture after changes, diff, annotate regressions, export reports |
| **monitor** | Watch screen for errors during deploys/tests, flag issues proactively, summarize findings |
| **gui-automation** | Orchestrate multi-step GUI workflows with `superbased_sequence` + the click/type/drag/scroll/form-fill primitives, with the safety checklist baked in |

## Hooks

**Post-test auto-capture:** After any test command (`npm test`, `jest`, `vitest`, `pytest`, `cargo test`, `go test`), SuperBased automatically captures a screenshot at quarter resolution. This builds a visual history of test runs without manual intervention.

## Humanization v2

GUI automation actions (`click`, `type`, `drag`, `hover`) ship with a humanization layer to reduce the bot-detection signal:

- **Cursor walks** use a sin-shaped velocity envelope (Bezier-style ease-in/ease-out) — not constant-velocity
- **Click targets** get a Gaussian jitter so two clicks on the same element land on slightly different pixels
- **Pre-click settle dwell** is gamma-distributed (rare long pauses, common short ones) — humans don't click the millisecond their cursor arrives
- **Click hold** varies between 50–110 ms, **key hold** between 45–95 ms, with per-process cross-session salt mixed into the seed
- **Typo simulation** wired via `typoProb` — with the QWERTY same-row neighbor distribution that real fat-finger errors follow
- **Pre-click tremor** on the target element + occasional 2–4× micro-pauses that mimic distraction
- **Inter-action catch-up pause** between sequence steps so back-to-back clicks don't have suspiciously identical inter-arrival times
- **Opt-in idle cursor drift** via the `humanInputIdleDrift` setting

Four profiles selectable per call: `humanize: 'off' | 'light' | 'human' | 'paranoid'`. Default is `light`. Bump to `human` or `paranoid` for sites with active bot detection — see the **humanization** skill.

## CAPTCHA solving

Plugin ships proactive guidance for the four CAPTCHA classes that come up in real automation work:

- **reCAPTCHA / Cloudflare Turnstile** — checkbox + image-grid challenges. Vision identifies the matching tiles, then a single batched click sequence selects them.
- **Drag puzzles** — slider-to-fit verification (e.g. "drag the puzzle piece to the gap"). Use `superbased_drag` with `humanize: 'light'` so the drop velocity reads as human; never `'off'`.
- **Rotation puzzles** — calibrate-then-execute pattern (capture, identify the angular delta, then drag in one motion).
- **Image grids** — vision to identify, batched click to select.

Plus an honest list of "what humanization can't defeat" (server-side device fingerprinting, audio CAPTCHAs, hCaptcha enterprise mode). See the **captcha-solving** skill.

## MCP Tools (72)

The plugin exposes all 72 SuperBased MCP tools. Click each section to expand.

<details>
<summary><b>Capture & View (5)</b></summary>

`superbased_screenshot` (preferred wrapper), `superbased_capture_image` (advanced), `superbased_capture`, `superbased_gallery_image`, `superbased_window_list`

</details>

<details>
<summary><b>AI & OCR (8)</b></summary>

`superbased_ai`, `superbased_ai_usage`, `superbased_ocr`, `superbased_transcribe`, `superbased_compress_text`, `superbased_project`, `superbased_workspace_sync`, `superbased_stt_status`

</details>

<details>
<summary><b>Gallery (2)</b></summary>

`superbased_gallery`, `superbased_gallery_update`

</details>

<details>
<summary><b>Privacy & Annotations (2)</b></summary>

`superbased_redact`, `superbased_annotate`

</details>

<details>
<summary><b>Dictation & Voice (2)</b></summary>

`superbased_dictate`, `superbased_dictation_history`

</details>

<details>
<summary><b>Recording & Visual QA (7)</b></summary>

`superbased_recording`, `superbased_sessions`, `superbased_describe_frames`, `superbased_narrate`, `superbased_diff`, `superbased_baseline`, `superbased_export`

</details>

<details>
<summary><b>Settings, Auth & System (6)</b></summary>

`superbased_settings`, `superbased_presets`, `superbased_auth`, `superbased_license`, `superbased_health`, `superbased_clipboard`

</details>

<details>
<summary><b>GUI Automation (40)</b></summary>

**Read the screen:** `superbased_ui_dump` (preferred for "read the page"), `superbased_scroll_capture` (preferred for "walk the whole page"), `superbased_scroll_to` (preferred for "find X on a long page"), `superbased_accessibility_tree`, `superbased_locate`

**Drive the desktop:** `superbased_sequence` (preferred for >1 step), `superbased_click`, `superbased_type`, `superbased_hotkey`, `superbased_scroll`, `superbased_drag`, `superbased_drag_file` (scaffold), `superbased_hover`, `superbased_context_menu_select`, `superbased_form_fill`, `superbased_dialog_handle`, `superbased_open_url`, `superbased_find_in_page`, `superbased_tab_management`, `superbased_tray_click`, `superbased_virtual_desktop`

**Window & display:** `superbased_window_state`, `superbased_resize_window`, `superbased_focus_window`, `superbased_window_bounds`, `superbased_find_title_bar_drag_region`, `superbased_display_list`, `superbased_launch_app`

**Vision targeting:** `superbased_find_image`, `superbased_capture_template`, `superbased_pixel_color`

**Accessibility & invoke:** `superbased_ax_invoke`

**Timing:** `superbased_wait`, `superbased_wait_for`, `superbased_mouse_position`

**Safety / dev tools:** `superbased_dry_run`, `superbased_replay`, `superbased_doctor_gui_automation`, `superbased_undo_last`, `superbased_tools`

</details>

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

### Click a button by label
```
/superbased:click Submit
```

### Fill a login form
```
/superbased:form email=alice@example.com password=hunter2
```

### Solve a rotation CAPTCHA
```
/superbased:captcha
(then describe the puzzle to Claude — it'll calibrate the angle, then drag in one motion)
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
- [MCP Integration Guide](https://github.com/marmutapp/superbased-claude-code-plugin) — Plugin repo & setup guide
