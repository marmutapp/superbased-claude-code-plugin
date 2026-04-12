---
description: Manage visual regression testing baselines
---

Parse $ARGUMENTS:
- "set WORKFLOW SESSION_ID": `superbased_baseline` with `action: "set"`, `workflowName`, and `sessionId`
- "get WORKFLOW": `superbased_baseline` with `action: "get"` and `workflowName` to retrieve the baseline session
- "history WORKFLOW": `superbased_baseline` with `action: "history"` and `workflowName` to see past baselines
- No arguments: explain that baselines are named references to recording sessions used for visual regression testing

Baselines store a "known good" state. Record a session, set it as baseline, then after changes, record again and use `/superbased:diff` to compare.
