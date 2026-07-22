---
name: qrcode
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# 二维码生成技能

## 工具

| 工具 | 用途 | 参数 |
|------|------|------|
| `qrcode_generate` | 生成二维码图片 | `text`（要编码的文本或 URL） |

**Example:**
```
用户: 把这个链接做成二维码 https://example.com
→ qrcode_generate(text="https://example.com")
```

生成 300×300 像素的 PNG 图片，支持任意文本和 URL。

## 注意

- 二维码扫描功能通过聊天命令 `扫码 <url>` 使用，不是 AI 工具。
- 文本过长可能导致二维码密度过高、难以扫描。建议先 `short_url` 缩短链接再生成。

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
