---
name: qq
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# QQ 官方机器人管理技能

QQ 官方机器人 API 同时支持「群聊」和「频道」两种场景，频道有 Guild/Channel 二级结构。

## 核心原则

### 群 vs 频道

QQ 官方机器人有两个独立的体系：
- **群聊**（Group）：传统 QQ 群，用 `group_id` 标识
- **频道**（Guild + Channel）：类似 Discord，Guild 是大频道，Channel 是子频道

操作前确认用户说的是「群」还是「频道」。

### 频道导航链

频道操作需要逐级获取 ID：
```
qq_list_guilds → 获取 guild_id
qq_list_channels(guild_id) → 获取 channel_id
qq_channel_info(channel_id) → 子频道详情
```

## 工具分类

### 群聊管理

| 工具 | 用途 | 说明 |
|------|------|------|
| `qq_kick_member` | 踢出成员 | — |
| `qq_mute_member` | 禁言 | — |
| `qq_mute_all` | 全员禁言/解除 | — |
| `qq_list_members` | 成员列表 | — |
| `qq_get_group_info` | 群信息 | — |

### 频道管理

| 工具 | 用途 | 说明 |
|------|------|------|
| `qq_list_guilds` | 频道列表 | 获取所有 Guild |
| `qq_list_channels` | 子频道列表 | 获取 Guild 下的 Channel |
| `qq_channel_info` | 子频道详情 | — |
| `qq_member_detail` | 成员详情 | — |

### 角色管理

| 工具 | 用途 | 说明 |
|------|------|------|
| `qq_create_role` | 创建角色 | — |
| `qq_add_role` | 授予角色 | 需 role_id |
| `qq_remove_role` | 移除角色 | 需 role_id |
| `qq_list_roles` | 角色列表 | 获取所有角色及 ID |

## 易错点

1. **频道操作需要 guild_id + channel_id 二级 ID**，不能只用一个。先 `list_guilds` 再 `list_channels`。
2. **角色操作需要 role_id**，先 `qq_list_roles` 查询。
3. **此适配器是 QQ 官方 API**，功能受限于官方开放的接口，不如 NapCat/ICQQ 灵活。

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
