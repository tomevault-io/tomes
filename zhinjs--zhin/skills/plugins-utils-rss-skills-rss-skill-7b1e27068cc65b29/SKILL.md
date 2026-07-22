---
name: rss
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# RSS 订阅管理技能

## 工具

| 工具 | 用途 | 说明 |
|------|------|------|
| `rss_list_subscriptions` | 查看订阅列表 | 列出当前会话的所有 RSS 订阅 |
| `rss_preview_feed` | 预览 RSS 源 | 获取指定 URL 的最新条目，用于预览内容质量 |

**Example:**
```
用户: 我订阅了哪些 RSS？
→ rss_list_subscriptions()

用户: 看看这个源有什么内容 https://example.com/feed.xml
→ rss_preview_feed(url="https://example.com/feed.xml")
```

## 注意

- 订阅的增加/删除通过聊天命令（`rss-add`/`rss-remove`）管理，不是 AI 工具。
- 每个群/会话有订阅数量上限（受配置约束）。
- 定时推送由后台定时任务处理，不需要手动触发。

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
