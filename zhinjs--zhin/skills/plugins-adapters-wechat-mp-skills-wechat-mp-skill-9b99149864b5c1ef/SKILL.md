---
name: wechat-mp
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# 微信公众号适配器

纯消息通道，收发微信公众号用户消息。无 AI 工具可调用。

## 能力

- 通过 HTTP 回调接收微信推送的用户消息事件
- 自动刷新 Access Token，无需手动维护
- 支持签名验证和 AES 消息加解密
- 回复通过常规 `$reply` 发送

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
