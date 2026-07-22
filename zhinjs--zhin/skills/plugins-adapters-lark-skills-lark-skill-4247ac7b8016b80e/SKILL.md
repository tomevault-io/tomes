---
name: lark
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# 飞书/Lark 群聊管理技能

飞书的群聊模型偏向企业场景，有群聊创建/解散的完整生命周期管理，以及文件上传能力。

## 核心原则

### 企业级 ID 体系

飞书的用户 ID 有三种形式（open_id / union_id / user_id），不同 API 可能需要不同 ID 类型。通过 `lark_get_user` 可以查询用户详情并获取各种 ID。

### 群聊生命周期

飞书支持完整的群聊生命周期管理：创建 → 添加成员 → 设管理员 → 正常使用 → 更新设置 → 解散。

**Example — 创建项目群：**
```
步骤1: lark_create_chat(name="XX项目组", members=[user1, user2])
步骤2: lark_set_managers(chat_id, managers=[user1])  # 设管理员
```

## 工具分类

### 群聊管理

| 工具 | 用途 | 说明 |
|------|------|------|
| `lark_create_chat` | 创建群聊 | 需指定群名 + 初始成员 |
| `lark_update_chat` | 更新群设置 | 群名、群描述等 |
| `lark_dissolve_chat` | 解散群聊 | **不可逆**，需群主权限 |
| `lark_add_members` | 添加成员 | — |
| `lark_kick_member` | 移除成员 | — |
| `lark_set_managers` | 设管理员 | — |
| `lark_remove_managers` | 移除管理员 | — |
| `lark_set_group_name` | 改群名 | — |
| `lark_list_members` | 成员列表 | — |
| `lark_get_group_info` | 群信息 | — |

### 用户与文件

| 工具 | 用途 | 说明 |
|------|------|------|
| `lark_get_user` | 查询用户信息 | 可获取多种 ID 形式 |
| `lark_upload_file` | 上传文件 | 返回 file_key，可在消息中引用 |

## 易错点

1. **解散群聊不可逆**，需群主权限。确认用户意图后再执行。
2. **群聊创建至少需要群名和一个初始成员**。
3. **文件上传返回 file_key**，这个 key 用于在消息中引用文件，不是文件内容本身。
4. **飞书有 open_id / union_id / user_id 三种 ID**，操作时注意使用正确的 ID 类型。

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
