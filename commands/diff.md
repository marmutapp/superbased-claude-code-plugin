---
description: Compare two recording sessions for visual regressions
---

If $ARGUMENTS contains two session IDs: use `superbased_diff` with `baselineSessionId` (first) and `currentSessionId` (second).

If one session ID: use `superbased_baseline` with `action: "get"` to find the baseline for the associated workflow, then diff.

If no IDs: use `superbased_sessions` with `action: "list"` to show available sessions and ask which two to compare.

Report: frames that changed, what changed, overall similarity score, and whether changes appear expected or are regressions.
