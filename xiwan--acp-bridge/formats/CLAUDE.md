# acp-bridge

> [← Configuration](configuration.md) | [API Reference →](api-reference.md)

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/acp-bridge/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

[← Configuration](configuration.md) | [API Reference →](api-reference.md)

> **Docs:** [Getting Started](getting-started.md) · [Tutorial](tutorial.md) · [Configuration](configuration.md) · [Agents](agents.md) · [API Reference](api-reference.md) · [Pipelines](pipelines.md) · [Async Jobs](async-jobs.md) · [Webhooks](webhooks.md) · [Client Usage](client-usage.md) · [Tools Proxy](tools-proxy.md) · [Security](security.md) · [Process Pool](process-pool.md) · [Testing](testing.md) · [Troubleshooting](troubleshooting.md)

# Agents

## Compatibility Matrix

| Agent | Vendor | ACP | Mode | Status | Tests | Install |
|-------|--------|-----|------|--------|-------|---------|
| [Kiro CLI](https://github.com/aws/kiro-cli) | AWS | ✅ Native | `acp` | ✅ Integrated | 7/7 | `curl -fsSL https://cli.kiro.dev/install \| bash` |
| [Claude Code](https://github.com/anthropics/claude-code) | Anthropic | ✅ Native | `acp` | ✅ Integrated | 5/5 | `npm i -g @agentclientprotocol/claude-agent-acp` |
| [Qwen Code](https://www.npmjs.com/package/@anthropic-ai/qwen-code) | Alibaba | ✅ `--acp` | `acp` | ✅ Integrated | 6/6 | `npm i -g @anthropic-ai/qwen-code` |
| [OpenGame](https://github.com/leigest519/OpenGame) | Open Source | ✅ `--acp` | `acp` | ✅ Integrated | — | See [repo](https://github.com/leigest519/OpenGame) |
| [OpenAI Codex](https://github.com/openai/codex) | OpenAI | ✅ | `acp` | ✅ Integrated | 6/6 | `npm i -g @openai/codex @agentclientprotocol/codex-acp` |
| [Gemini CLI](https://github.com/google-gemini/gemini-cli) | Google | 🧪 Experimental | — | 🟡 Planned | — | — |
| [Copilot CLI](https://docs.github.com/en/copilot/reference/acp-server) | GitHub | ✅ `--acp` | — | 🟡 Planned | — | — |
| [OpenCode](https://github.com/opencode-ai/opencode) | Open Source | ✅ `opencode acp` | `acp` | ✅ Integrated | 6/6 | See [repo](https://github.com/opencode-ai/opencode) |
| [Harness Factory](https://github.com/xiwan/harness-factory) | Open Source | ✅ Native | `acp` | ✅ Integrated | 4/4 | See [repo](https://github.com/xiwan/harness-factory) |
| [Hermes Agent](https://github.com/NousResearch/hermes-agent) | Nous Research | ✅ `hermes acp` | `acp` | ✅ Integrated | 8/8 | `uv tool install 'hermes-agent[acp] @ git+...'` |
| [OpenClaw](https://github.com/openclaw/openclaw) | Open Source | ✅ `openclaw acp` | `acp` | ✅ Integrated | — | `sudo npm i -g openclaw` |
| [CoStrict](https://github.com/zgsm-ai/costrict) | Open Source 🇨🇳 | ✅ Native | — | 🟡 Planned | — | — |
| [Trae Agent](https://github.com/bytedance/trae-agent) | ByteDance 🇨🇳 | ❌ | `pty` | ✅ Integrated | 4/4 | `cd trae-agent && uv sync --all-extras` |
| [Aider](https://github.com/Aider-AI/aider) | Open Source | ❌ | — | ⚪ No ACP | — | — |

**Legend:** ✅ Integrated — 🟡 Planned (ACP-ready) — ⚪ No ACP support yet — 🧪 Experimental

## Integration Modes

### ACP Mode (recommended)

Agents communicate via stdio JSON-RPC. Enables process reuse, multi-turn context, structured events (thinking/tool/status), and SSE streaming.

```yaml
agents:
  kiro:
    enabled: true
    mode: "acp"
    command: "kiro-cli"
    acp_args: ["acp", "--trust-all-tools"]
    working_dir: "/tmp"
```

### PTY Mode (fallback)

For agents without ACP support. Bridge spawns a new subprocess per request and reads stdout. No process reuse, no context retention, no structured events.

```yaml
agents:
  codex:
    enabled: true
    mode: "pty"
    command: "codex"
    args: ["exec", "--full-auto", "--skip-git-repo-check"]
    working_dir: "/tmp"
```

## Agent-Specific Notes

### Kiro CLI

- Login required: `kiro-cli login`
- `--trust-all-tools` auto-approves all tool calls — remove in untrusted networks

### Claude Code

- Uses `claude-agent-acp` adapter (not the `claude` CLI directly)
- `session/request_permission` is auto-answered with `proceed_always` by Bridge
- For Bedrock: set `CLAUDE_CODE_USE_BEDROCK=1` and `ANTHROPIC_MODEL=<model-id>`
- ⚠️ `@zed-industries/claude-agent-acp` is deprecated — use `@agentclientprotocol/claude-agent-acp`

### OpenAI Codex

- PTY mode only (no ACP support)
- Requires [LiteLLM](https://github.com/BerriAI/litellm) proxy for non-OpenAI models — see [Configuration](configuration.md#codex--litellm-setup)
- Add `--skip-git-repo-check` if `working_dir` is not a git repo

### Trae Agent

- PTY mode only (no ACP support)
- Requires [LiteLLM](https://github.com/BerriAI/litellm) proxy for Bedrock models — use `openrouter` provider in `trae_config.yaml`
- LiteLLM must set `additional_drop_params: ["top_p"]` on Anthropic Claude models (Bedrock rejects `temperature` + `top_p` together, and trae always sends both)
- Config file: `~/projects/trae-agent/trae_config.yaml`

### Harness Factory

- Profile-driven: same binary + different profiles = different agents
- Dynamic creation at runtime via `POST /harness`
- Built-in model registry with `"auto"` random selection and error fallback
- Presets: `reader`, `executor`, `scout`, `reviewer`, `analyst`, `researcher`, `developer`, `writer`, `operator`, `admin`
- External skills via `skills_dir` in profile config (e.g. `s3-deploy` for static file deployment)

### OpenGame

- Fork of Qwen Code, specialized for AI web game generation
- Uses `--acp` flag (same ACP protocol as Qwen Code)
- Requires `QWEN_CODE_NO_RELAUNCH=1` to prevent subprocess relaunch in non-TTY
- Requires `authenticate(openai)` call before `session/new` — Bridge handles this automatically
- Requires `fs` client capability — Bridge provides `readTextFile` and `writeTextFile`
- Generated files written to `working_dir` (default `/tmp/opengame/`)
- Works well in sequence pipeline with harness for auto-deployment to S3

### Hermes Agent

- Also serves as webhook callback target via its webhook adapter
- Configure `format: "generic"` in Bridge webhook config to use Hermes for IM delivery

## Zero-Config Auto-Detection

When no `config.yaml` is present, Bridge scans `PATH` for known agent CLIs and registers them with default settings. Supported: `kiro-cli`, `claude-agent-acp`, `codex`, `trae-cli`, `qwen`, `opencode`, `hermes`, `harness-factory`.

## Writing a New Agent

Implement three JSON-RPC methods over stdio:

1. **`initialize`** — handshake, return agent info
2. **`session/new`** — create a conversation session
3. **`session/prompt`** — receive prompt, stream notifications, return result

See [`AGENT_SPEC.md`](../AGENT_SPEC.md) for the full protocol and [`examples/echo-agent.py`](../examples/echo-agent.py) for a minimal reference.

```bash
bash test/test_agent_compliance.sh my-agent-cli [args...]
```

## See Also

- [Configuration](configuration.md) — `config.yaml` reference
- [Process Pool](process-pool.md) — subprocess lifecycle management
- [Testing](testing.md) — compliance and integration tests

---
> Source: [xiwan/acp-bridge](https://github.com/xiwan/acp-bridge) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-06-29 -->
