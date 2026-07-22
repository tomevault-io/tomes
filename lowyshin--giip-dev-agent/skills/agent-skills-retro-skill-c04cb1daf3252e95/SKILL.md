---
name: retro
description: | Use when this capability is needed.
metadata:
  author: LowyShin
---

# Retro Skill

The `retro` skill helps you reflect on a completed task to extract valuable insights and prevent future mistakes.

## Workflow

1.  **Summary**: Briefly summarize the completed task.
2.  **What went well**: List the successful aspects of the implementation.
3.  **What could be improved**: Identify pain points, bottlenecks, or mistakes.
4.  **Lessons Learned**: Extract actionable advice for future tasks.
5.  **K-Layer Integration**: Automatically convert lessons into "Source-linked claims" for the Knowledge Layer.

## Usage

```bash
/retro [task-id or feature-name]
```

## Template

The retrospective should follow this structure:

### 📝 Task Retrospective: [Feature Name]
- **Completion Date**: YYYY-MM-DD
- **Related Task/Issue**: [Link]

#### 🚀 Successes
- [Item 1]
- [Item 2]

#### ⚠️ Challenges & Mistakes
- [Problem 1]: [Root Cause]
- [Problem 2]: [Root Cause]

#### 💡 Key Lessons
- [Lesson 1] -> [Action for next time]
- [Lesson 2] -> [Action for next time]

#### 🧠 K-Layer Claims
- [Claim 1]: [Source Reference]
- [Claim 2]: [Source Reference]

---
> Source: [LowyShin/giip-dev-agent](https://github.com/LowyShin/giip-dev-agent) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
