---
description: Fill a form by label/value pairs
---

Use `superbased_form_fill` to fill multiple form fields in one call. Always pass `confirm: true`.

**Workflow:**
1. Call `superbased_ui_dump` on the form's window to discover field labels and `automationId`s.
2. Build a `fields` array mapping label or automationId to value:
   ```json
   {
     "fields": [
       { "label": "Email", "value": "alice@example.com" },
       { "label": "Password", "value": "hunter2", "secret": true },
       { "automationId": "rememberMe", "value": true, "type": "checkbox" }
     ],
     "confirm": true
   }
   ```
3. Optionally set `submitLabel: "Sign in"` to click the submit button after filling.
4. End with a `superbased_screenshot` (`resolution: "half"`) to verify the form submitted / validation errors / success state.

**Parsing $ARGUMENTS:**
- `key=value` pairs separated by spaces: parse into `fields` array (e.g. `email=alice@example.com password=hunter2`)
- A description like "fill the login form with my creds" — ask the user for the values rather than guessing
- "submit" mentioned in the args: also pass `submitLabel: "Submit"` (or whichever button the form has)

**Sensitive values:** mark password / token / 2FA fields with `secret: true` so the audit log redacts them. Never log the raw value back to the user.

**Humanization:** form_fill respects the same `humanize` profile as `_type`. Default `'light'` is fine. For sites with active typing-cadence detection (banking login, social media), bump to `'human'` and consider setting `typoProb: 0.02` so the typing isn't suspiciously perfect.

If a field has no AX entry (canvas-rendered, custom widget, web iframe the AX layer skips), fall back to `_click` on `coords` then `_type` for that one field.
