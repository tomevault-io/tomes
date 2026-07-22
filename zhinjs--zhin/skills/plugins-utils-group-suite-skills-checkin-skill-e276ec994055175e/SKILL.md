---
name: checkin
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# 签到积分查询技能

## 工具

| 工具 | 用途 | 说明 |
|------|------|------|
| `checkin_query` | 查询用户积分 | 当前积分、连签天数等 |
| `checkin_rank` | 积分排行榜 | 群内积分 Top 排名 |

**Example:**
```
用户: 我有多少积分？
→ checkin_query(user_id=用户ID)

用户: 群里谁积分最多？
→ checkin_rank(group_id=当前群号)
```

## 注意

- 日常签到通过聊天命令（`签到`）触发，不是 AI 工具。
- 连续签到有额外奖励，中断后重新计算。
- 积分数据依赖数据库，确保数据库服务正常。

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
