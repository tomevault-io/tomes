---
name: onebot12
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# OneBot 12 协议适配器

纯协议适配器，收发消息。无 AI 工具可调用。

## 连接模式

- **WS 正向**：Bot 主动连接 OneBot 12 服务端
- **Webhook**：OneBot 12 向配置的 URL 推送事件
- **WS 反向**：OneBot 12 主动连接 Endpoint 的 WS 服务端

## 与 OneBot11 的区别

OneBot 12 标准化了事件格式、消息段类型和 API 响应结构。如果需要群管理等 AI 工具，使用 OneBot11 适配器。

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
