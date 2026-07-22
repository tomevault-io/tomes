---
name: component-chat-layout
description: Develop ChatLayout (header, content, footer) for chat UI in @ant-design/agentic-ui. Use when building chat page layout, message area, or input footer. Triggers on ChatLayout, chat layout, header content footer, chat page. Use when this capability is needed.
metadata:
  author: antdigital-ai
---

# ChatLayout 组件开发

聊天界面布局：头部、内容区、底部固定区域（如输入框）。

## 源码位置

- 主组件：`src/ChatLayout/index.tsx`
- 类型：`src/ChatLayout/types.ts`（ChatLayoutProps、ChatLayoutRef）
- 子组件：`FooterBackground` 等见 `src/ChatLayout/components/`

## 主要能力

- 头部（标题、折叠、分享等）、内容区（BubbleList 等）、底部固定
- `useAutoScroll`、`useElementSize` 等 Hooks 配合
- ref 暴露方法见 `ChatLayoutRef`

## 开发规范

- 样式使用 `createStyles` 与 token；支持 `classNames`/`styles`。
- 与 Bubble、MarkdownInputField、History 等组合时保持结构一致。

修改聊天布局时，参考 `src/ChatLayout/` 与 `AGENTS.md`。

---
> Source: [antdigital-ai/agentic-ui](https://github.com/antdigital-ai/agentic-ui) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
