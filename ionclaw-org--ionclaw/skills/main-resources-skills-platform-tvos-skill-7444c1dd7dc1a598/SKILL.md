---
name: platform-tvos
description: Platform context for tvOS. No invoke_platform functions are available on Apple TV. Use when this capability is needed.
metadata:
  author: ionclaw-org
---

# Platform: tvOS

You are running on an **Apple TV** (tvOS).

## Tool: `invoke_platform`

No platform functions are available on tvOS. In particular, local notifications are **not** supported here — Apple only allows app-icon badges on tvOS, with no alert banners, text, or sound.

Do not call `invoke_platform` on this platform; there is nothing it can do. If you need to notify the user, do it in the chat reply instead.

---
> Source: [ionclaw-org/ionclaw](https://github.com/ionclaw-org/ionclaw) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-10 -->
