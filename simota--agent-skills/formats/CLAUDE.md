# agent-skills

> 102のスキルエージェントで構成されるプロンプトエンジニアリングリポジトリ。

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/agent-skills/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# claude-skills

102のスキルエージェントで構成されるプロンプトエンジニアリングリポジトリ。
成果物はコードではなく SKILL.md ファイル群。

## 構造
- 各スキル: `{skill-name}/SKILL.md` + オプションの `references/`
- 共通プロトコル: `_common/` (BOUNDARIES.md, HANDOFF.md 等)
- テンプレート: `_templates/SKILL_TEMPLATE.md`
- エージェントジャーナル: `.agents/` (gitignore対象)

## 規約
- Conventional Commits: `feat(skill-name): description`
- SKILL.md 編集時は既存の CAPABILITIES_SUMMARY コメントブロック形式を維持
- `_common/` は全スキルに影響するため慎重に変更
- Git: @_common/GIT_GUIDELINES.md

---
> Source: [simota/agent-skills](https://github.com/simota/agent-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-05-03 -->
