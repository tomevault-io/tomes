---
name: short-url
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# 短链接生成技能

## 工具

| 工具 | 用途 | 参数 |
|------|------|------|
| `short_url` | 缩短 URL | `url`（原始链接，必须是 http/https） |

**Example:**
```
用户: 帮我缩短 https://very-long-domain.com/path/to/something?with=params&and=more
→ short_url(url="https://very-long-domain.com/path/to/something?with=params&and=more")
→ 返回: https://is.gd/xxxxx
```

使用 is.gd 服务生成短链接。

## 注意

- 输入必须是合法的 http/https URL。
- 展开短链查看原始地址的功能通过聊天命令 `展开 <url>` 使用。

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
