---
description: List recording sessions and view session frames
---

If $ARGUMENTS contains a session ID, use `superbased_sessions` with `action: "frames"` and that `sessionId` to show all frames in the session.

Otherwise, use `superbased_sessions` with `action: "list"` to show all past recording sessions with their IDs, names, frame counts, and timestamps.

For detailed AI descriptions of each frame, use `superbased_describe_frames` with the `sessionId`.
