---
trigger: always_on
description: This project uses **AGENTS.md** as the primary guidance file for all AI coding agents.
---

# Windsurf Rules for morphir-dotnet

This project uses **AGENTS.md** as the primary guidance file for all AI coding agents.

## 📚 Primary Guidance

**Start here**: [AGENTS.md](../../AGENTS.md)

AGENTS.md is the authoritative source containing:
- Project overview and architecture
- Agent scope and responsibilities
- Build, test, and deployment procedures
- Coding conventions and standards
- Morphir-specific modeling guidelines
- Testing strategy with TDD practices
- Decision policies and escalation rules
- Specialized guidance links

## 🎯 Specialized Topics

For domain-specific deep dives, see [.agents/](../../.agents/) directory:

### QA Testing
**File**: [.agents/qa-testing.md](../../.agents/qa-testing.md)

Comprehensive QA guidance including:
- Pre-commit and PR verification checklists
- Test plan templates and bug report templates
- Regression, feature, build, and package testing playbooks
- BDD (Reqnroll) and unit testing (TUnit) standards
- Test coverage requirements (>= 80%)
- F# test automation scripts

### Future Topics
The `.agents/` directory will expand to include:
- Deployment and release management
- Security testing and compliance
- Documentation and ADR writing
- Performance testing and benchmarking

## 🚀 Quick Reference

### Essential Commands

```bash
# Format code
./build.sh Format

# Run linter
./build.sh Lint

# Run all tests
./build.sh Test

# Full CI workflow simulation
./build.sh DevWorkflow

# Package everything
./build.sh PackAll
```

### Testing Workflow

```bash
# Quick smoke test (~2 minutes)
dotnet fsi .claude/skills/qa-tester/smoke-test.fsx

# Full regression test (~10-15 minutes)
dotnet fsi .claude/skills/qa-tester/regression-test.fsx

# Validate packages
./build.sh PackAll
dotnet fsi .claude/skills/qa-tester/validate-packages.fsx
```

## 🧪 Test-Driven Development (TDD)

**Required**: Follow RED → GREEN → REFACTOR cycle (AGENTS.md Section 9.1)

1. **RED**: Write failing test first
   - BDD scenario (Gherkin) for features
   - Unit test (TUnit) for components
   - Run tests, confirm they fail

2. **GREEN**: Implement minimal code to pass
   - Focus on making tests pass
   - Don't over-engineer

3. **REFACTOR**: Improve while keeping tests green
   - Clean up implementation
   - Remove duplication
   - Run tests after each change

### Testing Frameworks
- **Unit Tests**: TUnit (in `tests/*.Tests/`)
- **BDD Tests**: Reqnroll (Gherkin features in `tests/*/Features/*.feature`)
- **E2E Tests**: CLI execution tests (in `tests/Morphir.E2E.Tests/`)

## 🏗️ Coding Principles

From AGENTS.md Section 5:

### Immutability First
```csharp
// ✅ Good: Immutable record
public readonly record struct TypeId(string Value);

// ❌ Bad: Mutable class
public class TypeId { public string Value { get; set; } }
```

### No Nulls - Use Option<T>
```csharp
// ✅ Good: Option type
public Option<User> FindUser(string id);

// ❌ Bad: Nullable reference
public User? FindUser(string id);
```

### Make Illegal States Unrepresentable
```csharp
// ✅ Good: ADT with exhaustive cases
public abstract record ValidationResult
{
    public sealed record Valid(Document Document) : ValidationResult;
    public sealed record Invalid(List<ValidationError> Errors) : ValidationResult;
}

// ❌ Bad: Boolean flags
public class ValidationResult
{
    public bool IsValid { get; set; }
    public Document? Document { get; set; }
    public List<ValidationError>? Errors { get; set; }
}
```

### Pure Domain, Effects at Edges
```csharp
// ✅ Good: Pure function
public static ValidationResult Validate(Document doc, Schema schema);

// ❌ Bad: Side effects in domain
public async Task<ValidationResult> Validate(Document doc)
{
    await _logger.LogAsync("Validating..."); // Side effect!
    // ...
}
```

## 🔧 CLI Logging Standard

**CRITICAL**: CLI tools must never write logs to stdout

```csharp
// ✅ Good: Serilog configured to stderr
Log.Logger = new LoggerConfiguration()
    .WriteTo.Console(standardErrorFromLevel: LogEventLevel.Verbose)
    .CreateLogger();

// ❌ Bad: Console.WriteLine for logs
Console.WriteLine("Processing..."); // This goes to stdout!
```

**Why**:
- Stdout is for command output only (JSON, formatted results)
- Stderr is for diagnostics and logging
- Enables: `./morphir ir verify file.json --json | jq .`

See AGENTS.md Section 5 for complete details.

## ⚠️ Escalation Rules

**DO NOT** implement without human approval:
- Breaking public API changes
- IR/JSON compatibility changes without ADR
- Security/auth/crypto changes
- Destructive migrations

See AGENTS.md Section 2 for complete escalation rules.

## 📁 Project Structure

```
morphir-dotnet/
├── AGENTS.md                 # ← Primary guidance (START HERE)
├── .agents/                  # ← Specialized topics
│   ├── qa-testing.md         # QA and testing guidance
│   └── README.md             # Navigation and index
├── .windsurf/                # ← You are here
│   └── rules/morphir.md      # This file
├── .cursorrules              # Cursor pointer
├── .github/
│   └── copilot-instructions.md  # Copilot pointer
├── CLAUDE.md                 # Claude Code pointer
├── src/
│   ├── Morphir/              # CLI/host application
│   ├── Morphir.Core/         # Core domain model

<!-- Content truncated to meet Windsurf 6KB limit -->

---
> Converted and distributed by [TomeVault](https://tomevault.io/claim/finos) — claim your Tome and manage your conversions.
<!-- tomevault:4.0:windsurf_rules:2026-04-13 -->
