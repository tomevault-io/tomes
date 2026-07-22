---
name: telegram
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# Telegram 群组管理技能

Telegram 的群组管理模型与 QQ 不同：没有「群名片」概念，有封禁（ban）/解封（unban）机制，权限体系更细粒度。

## 核心原则

### 先查后操作

Telegram 的 user_id 是纯数字，用户通常只知道用户名（@xxx）。操作具体成员前，用 `telegram_list_admins` 或从消息上下文获取 user_id。

### Telegram 权限模型

Telegram 的权限不是简单的 owner/admin/member 三级，而是细粒度的权限集合。通过 `telegram_set_permissions` 可以控制：发消息、发媒体、发投票、添加成员、置顶消息等。

## 工具分类

### 群管基础

| 工具 | 用途 | 说明 |
|------|------|------|
| `telegram_kick_member` | 踢出成员 | 踢出后用户仍可重新加入 |
| `telegram_unban_member` | 解除封禁 | 被 ban 的用户无法加入群组 |
| `telegram_mute_member` | 禁言 | duration 单位秒，**0=永久限制** |
| `telegram_set_admin` | 设/取消管理员 | — |
| `telegram_set_group_name` | 改群名 | — |
| `telegram_set_description` | 设群描述 | — |
| `telegram_set_permissions` | 设群权限 | 影响所有普通成员，管理员不受限 |
| `telegram_get_group_info` | 群信息 | — |
| `telegram_list_admins` | 管理员列表 | — |
| `telegram_member_count` | 成员数量 | — |

### 消息与社交

| 工具 | 用途 | 说明 |
|------|------|------|
| `telegram_pin_message` | 置顶消息 | 需管理员权限 |
| `telegram_unpin_message` | 取消置顶 | — |
| `telegram_create_invite` | 创建邀请链接 | 需管理员权限 |
| `telegram_send_poll` | 发起投票 | 支持匿名 + 多选 |
| `telegram_react` | 表情反应 | 对消息贴 emoji |
| `telegram_send_sticker` | 发贴纸 | — |

## 与 QQ 群管的关键差异

| 概念 | QQ（OneBot11） | Telegram |
|------|---------------|----------|
| 禁言 duration=0 | **解禁** | **永久限制** |
| 踢出 | 踢出 = 移除 | 踢出 ≠ 封禁，可重新加入 |
| 封禁 | 无独立概念 | `ban` 阻止加入 |
| 群名片 | 支持 | 不支持 |
| 群权限 | admin/member 二分 | 细粒度权限集 |

## 易错点

1. **禁言 duration=0 在 Telegram 是永久限制**，与 QQ 的「解禁」含义相反。
2. **踢人不等于封禁**：`kick_member` 移除但不阻止重新加入；要永久禁止需要 ban。
3. **投票支持匿名和多选**：用户说「发个投票」时确认是否需要匿名/多选。
4. **权限设置影响全体普通成员**，不是针对个人。管理员不受影响。

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
