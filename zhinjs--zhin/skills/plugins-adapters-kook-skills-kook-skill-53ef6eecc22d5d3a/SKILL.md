---
name: kook
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# KOOK 服务器管理技能

KOOK 的管理模型类似 Discord，以角色为核心。此技能覆盖成员管理和角色系统。

## 核心原则

### ID 获取链

操作成员需要 KOOK 用户 ID，操作角色需要角色 ID：
- `kook_list_members` → 获取用户 ID
- `kook_list_roles` → 获取角色 ID

### 黑名单 ≠ 踢人

`kook_blacklist` 是永久性封禁，被拉黑的用户无法再加入服务器。`kook_kick_member` 只是移除，用户可以通过邀请重新加入。

## 工具详解

### 成员管理

| 工具 | 用途 | 说明 |
|------|------|------|
| `kook_kick_member` | 踢出 | 可重新加入 |
| `kook_ban_member` | 封禁 | 阻止重新加入 |
| `kook_unban_member` | 解除封禁 | — |
| `kook_set_nickname` | 改昵称 | 服务器内昵称 |
| `kook_list_members` | 成员列表 | — |
| `kook_blacklist` | 黑名单操作 | **不可逆，谨慎使用** |

### 角色管理

| 工具 | 用途 | 说明 |
|------|------|------|
| `kook_create_role` | 创建角色 | — |
| `kook_delete_role` | 删除角色 | — |
| `kook_grant_role` | 授予角色 | 需 user_id + role_id |
| `kook_revoke_role` | 撤销角色 | 需 user_id + role_id |
| `kook_list_roles` | 角色列表 | 获取所有角色及 ID |

## 易错点

1. **黑名单是永久封禁**，与普通踢人（kick）不同。用户说「把他踢了」用 kick，说「永久拉黑」才用 blacklist。
2. **角色操作需要 role_id**，先 `kook_list_roles` 查询。
3. **创建角色后还需要 grant_role 才能给成员分配**，创建 ≠ 分配。

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
