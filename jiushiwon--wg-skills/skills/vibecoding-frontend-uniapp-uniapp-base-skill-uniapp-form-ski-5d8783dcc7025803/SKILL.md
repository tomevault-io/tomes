---
name: uniapp-form-skill
description: uni-app 表单组件技能。包含输入框、单选（含开关）、下拉选择、弹窗等组件。 Use when this capability is needed.
metadata:
  author: jiushiwon
---

# uniapp-form-skill

> uni-app 表单组件技能。

## 核心组件

| 组件 | 说明 |
|------|------|
| base-input | 输入框组件 |
| base-switch | 开关组件 |
| base-radio | 单选组件 |
| base-select | 下拉选择组件 |

> 弹窗组件 (base-popup) 已移至 uniapp-page-skill（页面性质）

## 输入框 (base-input)

### 通用输入（8 种）

| 风格 | 触发词 |
|------|--------|
| 账号密码登录 | 账号密码登录、登录页 |
| 手机号+验证码 | 手机号输入、验证码输入 |
| 多行反馈 | 反馈输入、留言输入 |
| 禁用/只读 | 只读输入、禁用输入 |
| 前缀图标 | 图标输入、前缀输入 |
| 后缀图标 | 后缀输入、清除按钮 |
| OTP 验证码格子 | 验证码格子、6位验证码 |
| 浮动标签 | 浮动标签输入 |

### 搜索栏变体（6 种）

| 风格 | 触发词 |
|------|--------|
| 胶囊搜索栏 | 胶囊搜索、顶部搜索 |
| 小圆角卡片搜索栏 | 卡片搜索 |
| 弹窗卡片搜索栏 | 弹窗搜索 |
| 扁平搜索栏 | 扁平搜索、极简搜索 |
| 嵌入式搜索栏 | 嵌入式搜索 |
| 迷你胶囊搜索栏 | 迷你搜索 |

## 单选组件 (base-radio)

包含 15 种形态：10 种基础单选 + 5 种开关形态（通过 size 参数切换）

| 风格 | 触发词 |
|------|--------|
| 标准圆圈 | 圆圈单选、标准单选 |
| 打钩风格 | 打钩单选 |
| 标签排列 | 标签单选 |
| 卡片式 | 卡片单选 |
| 按钮组 | 按钮组单选 |
| 列表式 | 列表单选 |
| 切换式 | 切换开关 |
| 芯片风格 | 芯片单选 |
| 图片选项 | 图片选择 |
| 颜色选择 | 颜色选择 |

### 开关形态（通过 size 参数）

| 风格 | 触发词 |
|------|--------|
| 标准胶囊 | 胶囊开关 |
| 方形开关 | 方正开关 |
| 迷你圆点 | 迷你开关 |
| 图标按钮 | 图标开关 |
| 卡片开关 | 卡片开关 |
| 标签排列 | 标签单选 |
| 卡片式 | 卡片单选 |
| 按钮组 | 按钮组单选 |
| 列表式 | 列表单选 |

## 下拉选择 (base-select)

| 风格 | 触发词 |
|------|--------|
| 基础下拉 | 下拉框、下拉选择 |
| 弹出面板 | 弹出选择、面板选择 |
| 标签多选 | 标签多选 |
| 城市级联 | 城市选择、地址选择 |
| 搜索下拉 | 搜索下拉 |
| 宫格选择 | 宫格选择、网格选择 |

## 文件结构

```
uniapp-form-skill/
├── SKILL.md
├── README.md
├── base-input.md
├── base-switch.md
└── demo-components/
    ├── base-input/
    ├── base-switch/
    ├── base-radio/
    └── base-select/
```

## 设计规范

### 容器原则

> **所有涉及内容容器的组件，都必须使用 base-card 作为容器**

- 输入框容器 → base-card 包裹 input
- 开关容器 → base-card 包裹 switch
- 单选容器 → base-card 包裹 radio
- 下拉选择容器 → base-card 包裹 select

**即：base-card 是所有表单组件的容器基底。**

---
> Source: [jiushiwon/wg-skills](https://github.com/jiushiwon/wg-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
