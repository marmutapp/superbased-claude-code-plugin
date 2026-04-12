---
description: View or update SuperBased app settings
---

If $ARGUMENTS is empty, use `superbased_settings` with `action: "get"` to show current settings. API keys are never exposed.

If $ARGUMENTS contains "key=value" pairs, use `superbased_settings` with `action: "set"`, `key`, and `value`.

If $ARGUMENTS mentions "provider" or "ai", use `superbased_settings` with `action: "get_provider"` to show AI provider configuration.
