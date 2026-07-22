---
name: time
description: | Use when this capability is needed.
metadata:
  author: x-cmd
---

# time — skill0

Measure command execution time. From single-shot microsecond timing to multi-run statistical analysis.

## Quick Start

```bash
# With x-cmd
x time <command>                      # Single microsecond timing
x time stress -c 100 <command>        # 100-run statistics
x time cmp 'cmd1' 'cmd2' 'cmd3'      # Compare commands

# Without x-cmd — use shell built-ins
time <command>                        # Basic timing
# For benchmarking, use a loop:
for i in $(seq 1 100); do
  start=$(date +%s%N)
  <command>
  end=$(date +%s%N)
  echo $(( end - start ))
done
```

## What's Available

| Command | Description |
|---------|-------------|
| `x time <cmd>` | Single run, microsecond precision |
| `x time getms <cmd>` | Millisecond precision |
| `x time stress -c N <cmd>` | N runs with full stats |
| `x time stress -b N <cmd>` | Auto-decide runs within budget |
| `x time cmp 'c1' 'c2'` | Compare multiple commands |

## Output Formats

- `--csv` CSV for programmatic analysis
- `--tsv` Tab-separated
- `--yml` YAML

## This skill0 grows

Starting with the essentials. Will add:
- Benchmarking patterns
- Statistical interpretation guide
- Common performance anti-patterns

---
> Source: [x-cmd/x-cmd](https://github.com/x-cmd/x-cmd) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
