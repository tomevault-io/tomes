---
name: repeater
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# 复读机

中间件自动检测群内连续相同消息，达到阈值后 Endpoint 跟读一次。无 AI 工具可调用。

## 行为

- 默认阈值：连续 3 条相同消息触发跟读
- 跟读后进入冷却期，避免刷屏
- 通过命令 `repeater-status` 查看/切换当前群的开关状态

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
