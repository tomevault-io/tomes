---
name: qr
description: | Use when this capability is needed.
metadata:
  author: x-cmd
---

# qr — skill0

Generate QR codes from text or URLs. Terminal display, PNG output, or pure shell encoding.

## Quick Start

```bash
# With x-cmd
x qr "Hello World"                   # Terminal QR code
x qr "https://example.com"           # URL to QR

# Without x-cmd — use Python
pip install qrcode
python3 -c "import qrcode; qrcode.make('Hello').save('qr.png')"

# Or use online API
curl -s "https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=Hello" -o qr.png
```

## What's Available

| Mode | Description |
|------|-------------|
| Terminal | Display QR in terminal |
| PNG | Generate PNG file |
| Pure shell | AWK-based encoding (no deps) |

## This skill0 grows

Starting with the essentials. Will add:
- QR encoding algorithms
- Error correction levels
- WiFi QR format

---
> Source: [x-cmd/x-cmd](https://github.com/x-cmd/x-cmd) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
