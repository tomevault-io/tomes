---
name: uniapp-page-skill
description: uni-app 页面模板技能。包含聊天页、商品页、列表页、详情页、登录页、弹窗等。 Use when this capability is needed.
metadata:
  author: jiushiwon
---

# uniapp-page-skill

> uni-app 页面模板技能。

## 核心案例

| 类型 | 说明 |
|------|------|
| chat | 聊天页面 |
| product | 商品页面 |
| base-popup | 弹窗组件（底部/顶部/左侧/右侧弹出） |

## 列表页 (6 种)

| 风格 | 触发词 |
|------|--------|
| 好友列表 | 好友列表、联系人列表 |
| 关注列表 | 关注列表、粉丝列表 |
| 获赞与收藏列表 | 获赞列表、收藏列表 |
| 设置列表 | 设置页、偏好设置 |
| 订单列表 | 订单页、售后列表 |
| 积分中心 | 积分页、钱包页 |

## 详情页 (6 种)

| 风格 | 触发词 |
|------|--------|
| 商品详情 | 商品详情页、产品详情 |
| 活动详情 | 活动详情、动态详情 |
| 帖子详情 | 帖子详情、内容详情 |
| 个人中心详情 | 个人主页、用户主页 |
| 钱包详情 | 钱包页、资产页 |
| 结果页 | 结果页、支付结果、成功页 |

## 搜索页 (4 种)

| 风格 | 触发词 |
|------|--------|
| 搜索页 | 搜索页、搜索入口 |
| 搜索结果 | 搜索结果、列表页 |
| 带筛选搜索 | 筛选搜索、高级搜索 |
| 无结果 | 搜索无结果、空结果 |

## 登录页 (7 种)

| 风格 | 触发词 |
|------|--------|
| 标准账号登录 | 登录页、账号登录 |
| 手机号登录 | 手机号登录、验证码登录 |
| 微信登录 | 微信登录、一键登录 |
| 极简登录 | 极简登录、清爽登录 |
| 渐变登录 | 渐变登录、动态登录 |
| 主题图登录 | 主题图登录、大图登录 |
| 浮动登录 | 浮动登录、圆形浮动登录 |

## 自定义 TabBar (5 种)

| 风格 | 触发词 |
|------|--------|
| 标准 TabBar | 标准 TabBar、底部导航 |
| 凸起 TabBar | 凸起 TabBar、发布中心 |
| 毛玻璃 TabBar | 毛玻璃 TabBar、模糊导航 |
| 悬浮药丸 TabBar | 悬浮 TabBar、药丸导航 |
| 分栏 TabBar | 分栏 TabBar、侧边导航 |

## 文件结构

```
uniapp-page-skill/
├── SKILL.md
├── README.md
├── chat.md
├── product.md
├── base-popup.md
└── demo-components/
    ├── list/
    ├── detail/
    ├── layout/
    └── more/
```

## 设计规范

### 容器原则

> **所有涉及内容容器的组件，都必须使用 base-card 作为容器**

- 弹窗内容 → base-card 包裹
- 列表项 → base-card 承载每行内容
- 页面区块 → base-card 作为卡片容器

**即：base-card 是所有页面组件的容器基底。**

---
> Source: [jiushiwon/wg-skills](https://github.com/jiushiwon/wg-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
