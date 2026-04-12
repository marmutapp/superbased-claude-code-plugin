---
description: List open windows or capture a specific window by name
---

If $ARGUMENTS is empty, use `superbased_window_list` to list all visible windows. Report each window's name, whether it's active, and whether it's minimized.

If $ARGUMENTS contains a window name, use `superbased_capture_image` with `window` set to $ARGUMENTS and `resolution: "half"`. SuperBased will activate the window (restore if minimized), capture it, then restore focus to the previous window.

Describe what you see in the captured window.
