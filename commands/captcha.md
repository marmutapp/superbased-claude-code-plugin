---
description: Solve a CAPTCHA challenge blocking a GUI automation flow
---

Surface the **captcha-solving** skill in the agent's working context and apply the right pattern for the challenge type.

**Identify the CAPTCHA class first** (capture the screen with `superbased_screenshot`, then identify):

| Challenge | Pattern |
|---|---|
| "Select all squares with X" (reCAPTCHA / Turnstile image grid) | Vision-identifies, single batched `superbased_sequence` of clicks ending in Verify |
| Drag puzzle (slider-to-fit, "drag piece to gap") | Vision returns delta, then `superbased_drag` in **one motion** with `humanize: 'light'` |
| Rotation puzzle ("rotate image upright") | Calibrate-then-execute: vision returns angle, then `superbased_drag` in one motion |
| Checkbox-only ("I'm not a robot" with no follow-up) | Single `superbased_click` with `humanize: 'human'`, then `superbased_wait_for` success state |
| Audio CAPTCHA | Surface to user — SuperBased can't decode audio |

**Critical rules:**
- Drag-puzzle drops MUST use `humanize: 'light'` (not `'off'`) — drop velocity is the main signal
- Rotation puzzles MUST be one drag, not multiple sub-drags — calibrate the full delta first
- Image-grid clicks MUST be batched into one `superbased_sequence` — separate clicks score as bot cadence
- Don't loop blindly — if a CAPTCHA fails twice, stop and ask the user before retrying

**What can't be defeated** (be honest with the user when applicable):
- Server-side fingerprinting (TLS, IP reputation, browser fingerprint) — the user's IP is the user's IP; no humanization helps
- hCaptcha enterprise mode — try Pattern 1 with `humanize: 'paranoid'` once; if it loops, escalate
- Phone / SMS / email verification — not a CAPTCHA but the same wall — surface and wait for user

See the full **captcha-solving** skill for detailed patterns and the honest "what humanization can't defeat" list.
