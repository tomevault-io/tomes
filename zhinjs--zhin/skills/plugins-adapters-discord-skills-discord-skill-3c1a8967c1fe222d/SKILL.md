---
name: discord
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# Discord 服务器管理技能

Discord 的管理模型围绕「角色」和「权限」展开，与 QQ 的 admin/member 模型不同。

## 核心原则

### ID 获取链

Discord 操作需要精确的 ID（用户 ID、角色 ID）。两步获取：
- **用户 ID**：`discord_list_members` → 匹配昵称
- **角色 ID**：`discord_list_roles` → 匹配角色名

**Example:**
```
用户: 给小明加个"管理员"角色
步骤1: discord_list_members → 找到小明的 user_id
步骤2: discord_list_roles → 找到"管理员"角色的 role_id
步骤3: discord_add_role(user_id, role_id)
```

### 角色优先思维

Discord 中几乎所有权限都由角色控制。用户说「给他管理员」不一定是设管理员，可能是授予某个有管理权限的角色。理解用户意图后选择正确的工具。

## 工具分类

### 成员管理

| 工具 | 用途 | 说明 |
|------|------|------|
| `discord_kick_member` | 踢出成员 | 被踢后可通过邀请重新加入 |
| `discord_ban_member` | 封禁 | 阻止重新加入 + 可选删除历史消息 |
| `discord_unban_member` | 解除封禁 | — |
| `discord_mute_member` | 禁言 | — |
| `discord_set_nickname` | 改昵称 | 服务器内昵称，非全局 |
| `discord_list_members` | 成员列表 | — |
| `discord_get_group_info` | 服务器/频道信息 | — |

### 角色管理

| 工具 | 用途 | 说明 |
|------|------|------|
| `discord_add_role` | 授予角色 | 需 role_id |
| `discord_remove_role` | 移除角色 | 需 role_id |
| `discord_list_roles` | 角色列表 | 获取所有角色及其 ID |

### 内容与互动

| 工具 | 用途 | 说明 |
|------|------|------|
| `discord_create_thread` | 创建线程 | 从消息或频道创建讨论线程 |
| `discord_react` | 表情反应 | 支持 Unicode emoji 和自定义 emoji |
| `discord_send_embed` | Embed 富文本 | title/description/color/fields 等字段 |
| `discord_forum_post` | 论坛帖子 | 在论坛频道发布帖子 |

## 易错点

1. **Discord 昵称是服务器级别的**，一个用户在不同服务器可以有不同昵称。
2. **角色操作需要角色 ID**，不能用角色名直接操作。先 `list_roles` 查。
3. **Embed 消息不是普通文本**，它有固定结构（title/description/color/fields），用于发送富文本格式的消息。
4. **Bot 只能操作低于自身角色的成员**。如果目标用户的最高角色高于 Endpoint 的角色，操作会失败。

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
