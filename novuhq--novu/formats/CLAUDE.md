# novu

> When creating a new pull request on GitHub, use this to specify the contents

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/novu/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:


### Pull Request Rules

**Title format**: `type(scope): Description fixes NOV-<ticket-id>`

- Examples: `feat(dashboard): add workflow trigger button fixes NOV-123`, `fix(api-service): handle null subscriber case fixes NOV-456`
- Omit the `fixes NOV-XXX` suffix when no Linear ticket is in context

**Scopes**: `dashboard`, `api-service`, `worker`, `shared`, `js`, `react`, `react-native`, `nextjs`, `providers`, `root`

**Description**: Summarize what changed and why. List breaking changes. Add screenshots for UI changes. For non-trivial logic or architecture changes, include a concise Mermaid diagram (flow, sequence, or component) so reviewers can grasp the change at a glance.

**Enterprise packages**: When changes touch `enterprise/`, also open a matching PR in `novuhq/packages-enterprise` on a branch from `next`.

---
> Converted and distributed by [TomeVault](https://tomevault.io/claim/novuhq)
> This is a context snippet only. You'll also want the standalone SKILL.md file — [download at TomeVault](https://tomevault.io/claim/novuhq)
<!-- tomevault:4.0:claude_md:2026-04-08 -->
