---
name: email
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# 邮件适配器

纯消息通道，通过 SMTP 发送、IMAP 接收邮件。无 AI 工具可调用。

## 能力

- 通过 IMAP 定时轮询收取新邮件，转为 Zhin 消息事件
- 通过 SMTP 发送回复，支持附件和 TLS/SSL 加密
- 消息通过常规 `$reply` 发送，无需专用工具

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
