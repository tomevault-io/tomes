---
name: check-release
description: 检查仓库是否满足发版条件，但不执行发布 Use when this capability is needed.
metadata:
  author: bladeofgod
---

# check-release

这是 Claude Command 工作流 的 Codex 原生发现入口。执行前必须完整读取并遵守
[`Command 工作流 事实源`](../../../.claude/commands/check-release.md)。
参数映射：

- 参数提示：`[版本号或发布约束]`。
- 显式调用 `$check-release ...` 时，移除只用于选择 Skill 的
  `$check-release` token，其余用户输入作为 `$ARGUMENTS`。
- 由语义匹配触发时，完整的当前用户任务输入作为 `$ARGUMENTS`。
- 必需参数缺失时，遵守源 Command 的停止条件，不猜测输入。

不要在本文件复制或修改工作流正文。

---
> Source: [bladeofgod/flutter-ai-harness](https://github.com/bladeofgod/flutter-ai-harness) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-13 -->
