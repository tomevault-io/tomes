---
name: dd-browser-sdk
description: > Use when this capability is needed.
metadata:
  author: datadog-labs
---

# Datadog Browser SDK

RUM, Logs, and Session Replay instrumentation for browser applications.

## Skills

| Task | Skill |
|------|-------|
| Upgrade from v4 to v5 | `dd-browser-sdk/upgrade-v5` |
| Upgrade from v5 to v6 | `dd-browser-sdk/upgrade-v6` |
| Upgrade from v6 to v7 | `dd-browser-sdk/upgrade-v7` |

## Routing

**Upgrading from v4 to v5** (removed options like `proxyUrl`, `sampleRate`, `replaySampleRate`, `premiumSampleRate`, `allowedTracingOrigins`, deprecated APIs like `addRumGlobalContext`, `removeUser`, or `/v4/` CDN paths):

**Immediately read** `.claude/skills/dd-browser-sdk/upgrade-v5/SKILL.md` — do not proceed from memory.

**Upgrading from v5 to v6** (removed options like `useCrossSiteSessionCookie`, `sendLogsAfterSessionExpiration`, dropping IE11 support, or `/v5/` CDN paths):

**Immediately read** `.claude/skills/dd-browser-sdk/upgrade-v6/SKILL.md` — do not proceed from memory.

**Upgrading from v6 to v7** (removed options like `betaEncodeCookieOptions`, `allowFallbackToLocalStorage`, `trackBfcacheViews`, `usePciIntake`, or `/v6/` CDN paths):

**Immediately read** `.claude/skills/dd-browser-sdk/upgrade-v7/SKILL.md` — do not proceed from memory.

---
> Source: [datadog-labs/agent-skills](https://github.com/datadog-labs/agent-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
