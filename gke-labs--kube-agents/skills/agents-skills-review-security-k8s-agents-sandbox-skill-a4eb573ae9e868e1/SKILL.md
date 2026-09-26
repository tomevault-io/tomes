---
name: review-security-k8s-agents-sandbox
description: Reviews AI agent execution sandboxes for code escape and lateral movement risks. Use when this capability is needed.
metadata:
  author: gke-labs
---
# Task
Review execution sandboxes (e.g., Python REPLs, bash tools, WASM) for LLM agents. Treat as highly hostile due to prompt injection risks.

# Checks
## 1. Secure RuntimeClass (CRITICAL)
- **Hardened Runtimes**: Flag standard pods. Require secure `RuntimeClass` (e.g., `gvisor`, `kata-containers`) for sandboxes.

## 2. Isolation
- **Logical Separation**: Flag sandboxes sharing a container with the main agent loop, unless permissions/runtime are demonstrably strict.
- **Profiles**: Require restrictive Seccomp or AppArmor profiles blocking dangerous syscalls.

## 3. Ephemeral Lifecycles & Limits
- **Disposable**: Flag reusable sandboxes. Must be ephemeral to prevent persistence/data leaks.
- **Resource Limits**: Require aggressively low CPU/Memory/Ephemeral Storage `limits` to prevent DoS via infinite loops or memory bombs.

---
> Source: [gke-labs/kube-agents](https://github.com/gke-labs/kube-agents) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
