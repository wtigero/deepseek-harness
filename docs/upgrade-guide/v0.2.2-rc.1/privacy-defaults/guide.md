---
kind: upgrade-guide
description: "Session uploads, Desktop analytics, and web tools now default to disabled."
---

# Privacy defaults

English | [中文](guide.zh.md)

## Change

Session-log contributions to the DeepSeek API are disabled by default. Base-profile feedback telemetry defaults to `DISABLED`. Desktop product analytics, plugin inventory metadata, web search, and web fetch are disabled by default. Existing profile, home, or command-line overrides can still enable them. Model providers remain configurable, and remote provider requests leave the computer. These settings do not confine subprocess or plugin network access.

Auto review removal and reload now use `fallbackPreset`, defaulting to `workspace-write` with approval `ask`. Custom fallback presets must confine writes and require approval.

## Migration

On Windows, use Node.js 24.20.0 or later in the 24.x line. Node.js 24.16.0 can crash during network shutdown; the [24.20.0 release](https://nodejs.org/en/blog/release/v24.20.0) includes the task-runner fix.

1. To opt into the DeepSeek session-log contribution, enable **Settings → General → Upload Session Log when using the official model API**. Read the session-log package reference before enabling it.
2. To opt into feedback telemetry, set `DSH_TELEMETRY_MODE=FEEDBACK_ONLY` before launching. Feedback can upload earlier session context.
3. To enable web tools, set `search: true` and/or `fetch: true` on the active `tool-web` row in the profile or agent preset. Enabled fetch can access local and private network addresses.
4. To opt into Desktop analytics, set `enabled: true` for the `product-analytics` row in the Desktop profile.
5. Inspect the active profile and overrides, then verify behavior in an isolated environment. Existing overrides take precedence over these defaults.
