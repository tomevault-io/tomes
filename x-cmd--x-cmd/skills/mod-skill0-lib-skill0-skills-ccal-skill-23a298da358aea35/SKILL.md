---
name: ccal
description: | Use when this capability is needed.
metadata:
  author: x-cmd
---

# ccal — skill0

Chinese calendar: lunar dates, solar terms (节气), traditional holidays, and daily almanac (黄历宜忌).

## Quick Start

```bash
# With x-cmd
x ccal                      # Interactive calendar view
x ccal info                 # Today's detailed info
x ccal info --yml 2026-05-31  # Specific date in YAML
x ccal fzm                  # Monthly solar terms and holidays

# Without x-cmd — use any Chinese calendar library
# Python: zhdate, lunardate, borax
# JS: lunar-javascript
```

## What's Available

| Feature | Description |
|---------|-------------|
| Lunar dates | 公历↔农历转换 |
| Solar terms | 24 节气查询 |
| Holidays | 传统节日、公历假日 |
| Almanac | 黄历宜忌、干支纪年 |
| Zodiac | 生肖、星座 |

## Output Formats

Supports structured output for AI agents:
- `--yml` YAML format
- `--tsv` Tab-separated
- `--csv` CSV format
- `--json` JSON format

## This skill0 grows

Starting with the essentials. Will add:
- Calendar calculation algorithms
- Holiday detection rules
- Almanac data sources

---
> Source: [x-cmd/x-cmd](https://github.com/x-cmd/x-cmd) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
