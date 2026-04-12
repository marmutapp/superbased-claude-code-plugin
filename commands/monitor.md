---
description: Start proactive AI screen monitoring that flags errors and issues
---

Use `superbased_recording` with `action: "start"` and `mode: "monitor"`.

**Defaults:**
- `analysisPrompt: "Flag any errors, warnings, failed tests, red status indicators, or unexpected states"`
- `analyzeEvery: 5` (AI analyzes every 5 significant frames)
- `analyzeInterval: 30` (minimum 30 seconds between AI calls)
- `analysisDetail: "low"` (512px images for fewer tokens)

If $ARGUMENTS contains:
- A custom prompt: use it as `analysisPrompt`
- "high" or "detailed": set `analysisDetail: "high"`
- A name: pass as `name`

Report the session ID. AI alerts arrive as MCP notifications. Use `superbased_recording` with `action: "get_analysis"` and the `sessionId` to retrieve all AI findings.

To stop: `/superbased:record stop`
