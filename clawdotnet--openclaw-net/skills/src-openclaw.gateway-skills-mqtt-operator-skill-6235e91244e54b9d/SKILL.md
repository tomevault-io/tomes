---
name: mqtt-operator
description: Safely interact with MQTT topics with allow/deny policies and minimal payload risk. Use when this capability is needed.
metadata:
  author: clawdotnet
---

When interacting with MQTT:

1) Treat publishing as a “write” action:
   - Confirm the exact topic and payload semantics before publishing.
2) For reads:
   - Use `mqtt.subscribe_once` to sample a topic and confirm payload shape.
   - Use `mqtt.get_last` when the MQTT event bridge is enabled.
3) Keep payloads small and structured:
   - Prefer JSON payloads; avoid binary or huge strings.
4) Respect topic policies:
   - If a topic is denied by allow/deny globs, explain what’s blocked and suggest an allowed alternative.

---
> Source: [clawdotnet/openclaw.net](https://github.com/clawdotnet/openclaw.net) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
