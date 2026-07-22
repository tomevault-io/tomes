---
name: milky
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# Milky 群管理技能

Milky 是 QQ 生态中的一种协议实现，提供标准群管理工具集。

## 核心原则

### 先查后操作

只有昵称时，先 `milky_list_members` 获取 QQ 号再操作。

**Example:**
```
用户: 禁言那个叫"阿强"的
步骤1: milky_list_members → 找到 user_id = 654321
步骤2: milky_mute_member(user_id=654321, duration=600)
```

## 工具详解

| 工具 | 用途 | 权限 | 关键参数 |
|------|------|------|----------|
| `milky_kick_member` | 踢出成员 | admin | `user_id` |
| `milky_mute_member` | 禁言/解禁 | admin | `user_id`, `duration`（秒，**0=解禁**） |
| `milky_mute_all` | 全员禁言/解除 | admin | `enable` |
| `milky_set_admin` | 设/取消管理员 | owner | `user_id`, `enable` |
| `milky_set_nickname` | 改群名片 | admin | `user_id`, `nickname` |
| `milky_set_group_name` | 改群名 | admin | `name` |
| `milky_list_members` | 成员列表 | user | — |
| `milky_get_group_info` | 群信息 | user | — |

## 易错点

1. **禁言 duration=0 是解禁**，不是永久禁言。
2. **管理员设置需要群主权限**（owner），管理员无法设置其他管理员。

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
