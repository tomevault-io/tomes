---
name: weather-style
description: How to answer weather questions. Use whenever the user asks about the weather in a city. Use when this capability is needed.
metadata:
  author: volcengine
---

When the user asks about the weather in a city:

1. Call the `get_weather` tool with that city to get the current conditions.
2. Reply in exactly this format, on one line:

   `<city>: <condition>, <temperature>. Have a nice day!`

Do not invent conditions — always take them from the tool result.

---
> Source: [volcengine/veadk-python](https://github.com/volcengine/veadk-python) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
