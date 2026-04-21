## Repository Overview

This is the **Opencode Workflows** repository - a collection of Opencode-based command templates and workflow patterns for building sophisticated command-based projects. The repository contains multiple workflow examples and templates that demonstrate different approaches to command architecture and tool integration.

<instructions>
## Verification Commands
This is a **workflow repository**, not a traditional application. Verification focuses on repository integrity and structural validity.

- **Audit Repository**: `/audit-repo` (Validates structure and configs via `audit_repo.py`)
- **Sync Documentation**: `/sync-docs` (Reports inventory and suggests doc updates via `sync_docs.py`)
- **Full Maintenance**: `/maintain-repo` (Runs full audit and sync cycle)

**Note**: There are no traditional `npm test`, `cargo build`, or `tsc` commands at the root level.
</instructions>

<rules>
## Process Constraints
- MUST NOT run long-running/blocking processes (dev servers, watch modes)
- Dev servers/background processes are USER's responsibility
- MUST use one-shot commands for verification (audit, sync, scripts)

## Coding Conventions
- **RFC 2119**: MUST use uppercase keywords (MUST, SHOULD, MAY) for requirements in agents and commands.
- **XML Structure**: MUST use XML tags (`<instructions>`, `<rules>`, etc.) to wrap logic blocks.
- **Modularity**: Files SHOULD NOT exceed 200 lines; functions SHOULD NOT exceed 40 lines.
- **Barrel Files**: Every module directory MUST have an `index.ts` (per `@coding-ts` guidelines).
</rules>

## Current Workflows

### Agent Templates Catalog
A focused collection of reusable agent prompts and orchestration patterns:
- **repo-maintainer**: Repository health custodian (audits, doc sync). **NOTE: This root agent is specific to the Opencode-Workflows repo.**
- **fast**: High-speed workhorse for trivial edits, running known commands, and simple file lookups.
- **smart**: Senior developer and architect for complex bug hunting, codebase refactoring, and verified implementation.
- **repo-navigator-creator**: Produces lean AGENTS.md navigation guides
- **subagent-orchestrator**: Dispatches specialized agents and manages execution plans
- **openspec-orchestrator**: Enforces strict OpenSpec formatting/validation and orchestrates subagents

Agents are designed for global installation in `~/.config/opencode/agent/` for reuse across projects.

### AI Research Tools
- AI search integration tools and patterns are demonstrated within the specialized agent packs (see `agents/opencode-configurator/`).
- Integrates with external AI services (e.g., Perplexica, OpenAI) via specialized skills.

## Architecture Patterns

### Command Structure
Commands follow Opencode's built-in `/commands` patterns (see opencode.ai/docs/commands):
- YAML frontmatter with descriptions
- Arguments section explaining $ARGUMENTS handling
- Step-by-step execution instructions
- Integration with external utilities

### Tool Integration
Commands can integrate with various external tools:
- **Script files**: JavaScript, Python, Bash executables
- **Bash tools**: System utilities, package managers, development tools
- **API endpoints**: Any curlable REST APIs or webhooks
- **Natural language workflows**: Pure LLM-driven processes

### Agent Structure
Agents follow Opencode's agent patterns with YAML frontmatter:
- **Description**: Clear guidance on when to use each agent
- **Mode**: Operation mode and tool constraints (read-only vs write)
- **Instruction Blocks**: LLM-optimized checklists and workflows
- **Global Installation**: Designed for reuse across projects via `~/.config/opencode/agent/`

<routing>
## Task Navigation
| Task | Entry Point | Key Files |
|------|-------------|-----------|
| Create AGENTS.md | /init | `agents/repo-navigator/` |
| Security Review | /security-review | `agents/security-reviewer/` |
| PRD Planning | /prd | `agents/parallel-PRD/` |
| Maintain Repo | /maintain-repo | `.opencode/command/` |
| Create Plugin | /create-plugin | `agents/create-opencode-plugin/` |
</routing>

### Configuration System
- `example-opencode.json` templates for Opencode configuration. Demonstrates disabling the legacy `general` subagent in favor of `fast`/`smart` splitting to optimize model usage:
  ```json
  "subagents": {
    "general": {
      "disable": true
    }
  }
  ```
- References to `AGENTS.md` in instructions arrays
- `package.json` in `.opencode/` for Opencode plugin dependencies
- Follows Opencode schema standards

## Model Requirements

Repository intelligence requires models with strong:
- **Context Management**: Maintaining project-level instructions throughout session
- **Instruction Following**: Precise execution of multi-step workflows
- **Agentic Capabilities**: Understanding when/how to use available commands and agents

**Recommended Models**: GPT-5.2, Claude 4.5, Gemini 3.

## Repository Structure

```
at/                          # Universal engineering guidelines (@coding-ts)
└── CODING-TS.MD             # Core development principles and standards

.opencode/                   # Root-level maintenance tools
├── agent/
│   └── repo-maintainer.md   # Health custodian
├── command/
│   ├── audit-repo.md        # Quality audit
│   ├── maintain-repo.md     # Full maintenance cycle
│   └── sync-docs.md         # Doc synchronization
└── skill/
    └── repo-maintenance/    # Maintenance logic & scripts

thinking-variants config/    # Thinking-level configurations
└── thinking-levels-opencode.json

agents/                      # Agent templates catalog
├── README.md               # Agent overview and usage guidance
├── component-engineer/      # Expert architecture package
│   └── .opencode/
│       ├── agent/
│       │   └── component-engineer.md
│       ├── command/
│       │   ├── component-create.md
│       │   └── component-review.md
│       └── skill/
│           └── component-engineering/
├── create-opencode-plugin/  # Plugin creation workflow
│   └── .opencode/
│       ├── agent/
│       │   └── plugin-creator.md
│       ├── command/
│       │   └── create-plugin.md
│       └── skill/
│           └── create-opencode-plugin/
├── generic/                # Globally useful agents
│   └── .opencode/
│       └── agent/
│           ├── fast.md                     # High-speed workhorse
│           ├── smart.md                    # Complex architecture expert
│           ├── repo-navigator-creator.md   # AGENTS.md generation
│           ├── subagent-orchestrator.md    # Multi-agent coordination
│           └── openspec-orchestrator.md    # OpenSpec workflow enforcement
├── repo-navigator/          # Repository documentation pack
│   ├── README.md            # Pack documentation
│   ├── agent/
│   │   └── repo-navigator.md    # Primary agent
│   ├── command/
│   │   └── init.md              # Unified /init with argument routing
│   └── skill/
│       ├── agent-navigation-sop/    # AI navigation workflow
│       ├── user-onboarding-sop/     # User assistance workflow
│       └── skill-creator/           # Bundled for custom skill creation
├── opencode-configurator/   # Configurator skills, agents, and commands
│   ├── agent/
│   │   └── opencode-configurator.md
│   ├── skill/
│   │   ├── agent-architect/
│   │   ├── command-creator/
│   │   ├── opencode-config/
│   │   ├── plugin-installer/
│   │   ├── skill-creator/
│   │   ├── model-researcher/
│   │   └── mcp-installer/
│   └── command/
│       ├── refactor-rfc-xml.md
│       └── permissions-update.md
├── parallel-PRD/           # Parallel PRD planning kit
│   └── .opencode/
│       ├── agent/
│       │   ├── TEMPLATE-planner.md
│       │   ├── glm-planner.md
│       │   └── parallel-prd-orchestrator.md
│       ├── command/
│       │   └── parallel-prd.md
│       └── skill/
│           └── prd-authoring/
├── security-reviewer/       # Security review tooling
│   └── .opencode/
│       ├── agent/
│       │   └── security-reviewer.md
│       └── skill/
│           ├── security-ai-keys/
│           ├── security-bun/
│           ├── security-convex/
│           ├── security-django/
│           ├── security-docker/
│           ├── security-express/
│           ├── security-fastapi/
│           ├── security-nextjs/
│           ├── security-secrets/
│           └── security-vite/
└── vite-react-ts-convex-tailwind/ # Stack-specific expert pack
    ├── CODING-TS.md
    ├── CONVEX.md
    ├── REACT19.md
    ├── TAILWIND4.md
    ├── TS59.MD
    └── .opencode/
        ├── agent/
        │   ├── VRTCT-orchestrator.md       # Stack orchestrator
        │   ├── VRTCT-brain.md              # Stack knowledge base
        │   ├── convex-database-expert.md   # Backend/DB specialist
        │   ├── react-19-master.md          # RSC/Actions expert
        │   ├── tailwind-41-architect.md    # Utility-first designer
        │   └── typescript-59-engineer.md   # Strict TS 5.9 engineer
        ├── command/
        │   ├── component-create.md
        │   └── component-review.md
        └── skill/
            ├── component-engineering/      # shadcn/ui components
            ├── convex-auth/                # Auth logic
            ├── convex-components/          # RAG & Workflows
            ├── convex-core/                # Backend patterns
            ├── convex-deploy/              # Deployment SOP
            ├── convex-runtime/             # Concurrent execution
            └── vite-shadcn-tailwind4/       # Modern frontend setup

cowork/                      # Multi-agent orchestration system
├── README.md               # Cowork system overview
├── AGENTS.md               # Cowork-specific agent navigation
├── opencode.json           # Cowork configuration
├── LESSONS-LEARNED.md      # Workflow optimization insights
├── .opencode/               # Cowork internal agents and skills
│   ├── agent/
│   │   ├── admin-assistant.md
│   │   ├── cowork-orchestrator.md
│   │   ├── data-analyst.md
│   │   ├── document-specialist.md
│   │   ├── presentation-expert.md
│   │   ├── cowork-configurator.md
│   │   └── research-specialist.md
│   ├── command/
│   │   └── cowork.md
│   └── skill/
│       ├── branding/
│       ├── comms/
│       ├── cowork/
│       ├── excel/
│       ├── pdf/
│       ├── powerpoint/
│       ├── themes/
│       ├── word/
│       └── writing/
└── vault/                  # Structured repository (Vault)
    ├── 01-Core-Identity/   # Bio.md, MASTER-STYLE-GUIDE.md
    ├── 02-Active-Work/     # 2026-01/, TEMPLATE.md
    ├── 03-Research-Intel/  # Research logs
    ├── 05-Output-Staging/  # DELIVERY-NOTES.md
    └── 06-Archive/         # Historic data

commands/                    # Additional command examples

commands2skills/             # Command→Skill migration patterns
├── COMMANDS.md
├── calculate.js
└── example-opencode.json
```

## Working with This Repository

### For Template Usage
1. Review available workflow templates in agents/ and commands/
2. Copy template elements selectively for your projects
3. Create your own `opencode.json` based on examples
4. Adapt commands and tools to specific needs
5. Install desired agents globally in `~/.config/opencode/agent/` for reuse across projects

### For Agent Usage
- Agents are designed for global installation but can be copied to project-specific `.opencode/agent/` directories
- Check YAML frontmatter to understand when to use each agent and any tool constraints
- Agents complement commands by providing specialized reasoning, research, or coordination
- Reference the relevant agent file before acting to respect mode and tool constraints

### For Workflow Development
- Commands follow Opencode `/commands` rules and patterns
- External tools should handle errors gracefully
- Documentation maintenance via specialized agents
- Model compatibility considerations for context management

## Future Development

This repository is designed to expand with additional workflow templates and patterns. Future workflows may include:
- Different command architectures and integration patterns
- Additional external tool integrations
- Alternative documentation systems
- Enhanced model compatibility patterns
- More specialized agent templates for different domains

## Key Insights

- This is a **workflow repository**, not a traditional application - no build/test/lint commands
- Focus on **reusable patterns** and **template architectures**
- Commands follow **Opencode standards** for compatibility
- Context injection currently limited to session-start (future enhancement possible)

---
> Source: [IgorWarzocha/Opencode-Workflows](https://github.com/IgorWarzocha/Opencode-Workflows) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:agents_md:2026-04-21 -->
