---
trigger: always_on
description: - [Change Management](#change-management)
---


# SandrasRules (Global Rulebook)

## Table of Contents
- [Change Management](#change-management)
- [Development Workflow](#development-workflow)
- [FastMCP 2.10 Repository Standards](#fastmcp-210-repository-standards)
- [DXT Packaging Standards](#dxt-packaging-standards)
- [Bug & Research Handling](#bug--research-handling)

## Change Management

### Rule to prove this was read
- Add "lgr1 " to cascade outputs

### Change Control
- Never remove, rewrite, or break major functionality without explicit user instruction
- Always clarify and confirm before making breaking changes
- Provide explicit diffs and summaries for all major edits
- Follow user-specified workflow preferences strictly
- Set up safety nets like auto-staged commits when possible

## Development Workflow

### Windows/PowerShell Script Syntax

#### 1. File System Operations

##### Directory Operations
```powershell
# Create directory (and parent directories if needed)
New-Item -ItemType Directory -Force -Path "path\to\directory"

# Remove directory (recursively)
Remove-Item -Path "path\to\directory" -Recurse -Force

# Change directory
Set-Location -Path "path\to\directory"
# Or use cd (alias for Set-Location)
cd "path\to\directory"
```

##### File Operations
```powershell
# View file content
Get-Content -Path "file.txt"

# View last N lines of a file
Get-Content -Path "file.log" -Tail 10

# View first N lines of a file
Get-Content -Path "file.log" -TotalCount 10

# Check if file exists
Test-Path -Path "file.txt"
```

#### 2. Command Chaining

##### Correct (PowerShell)
```powershell
# Sequential commands
command1; command2; command3

# Conditional execution (run command2 only if command1 succeeds)
command1 -ErrorAction Stop; if ($?) { command2 }

# Pipeline chaining
Get-Process | Where-Object { $_.CPU -gt 10 } | Sort-Object -Property CPU -Descending
```

##### Incorrect (Linux-style)
```bash
# Don't use Linux-style chaining
command1 && command2
command1 || command2
```

#### 3. Common Command Equivalents

| Linux Command | PowerShell Equivalent | Notes |
|---------------|----------------------|-------|
| `ls` | `Get-ChildItem` or `dir` | `dir` is an alias for `Get-ChildItem` |
| `cat` | `Get-Content` | |
| `grep` | `Select-String` or `sls` | `sls` is an alias for `Select-String` |
| `find` | `Get-ChildItem -Recurse` | For finding files |
| `pwd` | `Get-Location` or `pwd` | `pwd` is an alias for `Get-Location` |
| `rm -rf` | `Remove-Item -Recurse -Force` | |
| `chmod` | `icacls` or `Set-Acl` | |
| `echo` | `Write-Output` or `echo` | `echo` is an alias for `Write-Output` |

#### 4. Environment Variables

```powershell
# Set environment variable (current session)
$env:VARIABLE_NAME = "value"

# Set persistent environment variable (user scope)
[System.Environment]::SetEnvironmentVariable("VARIABLE_NAME", "value", "User")

# Get environment variable
$value = $env:VARIABLE_NAME
```

#### 5. Error Handling

```powershell
try {
    # Command that might fail
    Remove-Item -Path "nonexistent.txt" -ErrorAction Stop
} catch {
    Write-Error "Failed to remove file: $_"
    # Handle error
}
```

#### 6. Script Execution Policy

```powershell
# Check current execution policy
Get-ExecutionPolicy

# Set execution policy (requires admin)
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

#### 7. Path Handling

```powershell
# Join paths (cross-platform compatible)
$fullPath = Join-Path -Path "C:\parent" -ChildPath "child"

# Get absolute path
$absolutePath = Resolve-Path -Path "./relative/path"
```

#### 8. Best Practices
- Always use full cmdlet names in scripts (e.g., `Remove-Item` instead of `rm`)
- Use `-WhatIf` parameter to test destructive commands
- Prefer `-Filter` over `Where-Object` for better performance with file operations
- Use `-ErrorAction Stop` for critical commands that should terminate on failure
- Always validate paths with `Test-Path` before operations

### 1. Version Control
- Use feature branches for all changes
- Write clear, descriptive commit messages
- Open pull requests for code review
- Keep main branch stable and deployable

### 2. Code Style
- Follow language-specific style guides
- Use consistent indentation (spaces)
- Include comments for complex logic
- Keep lines under 120 characters

## Basic Memory Notes

**CRITICAL**: All Basic Memory notes MUST include a timestamp in their title or at the start of content. This is required for proper sorting and retrieval.

### 1. Note Structure
- **Title Format**: `[YYYY-MM-DD HH:MM] Clear, descriptive title`
- Start with a brief summary
- Use hierarchical headers for organization
- **Always include**:
  - Creation timestamp (if not in title)
  - Last updated timestamp
  - Author/initials
  - Relevant project/topic tags
- Add relevant categorization tags

### 2. Content Guidelines
- Be concise but thorough
- Use bullet points for lists
- Include code blocks with language specification
- Add context and reasoning, not just facts
- Note sources and references

## Docker Standards

### 1. Containerization
- Use multi-stage builds to minimize image size
- Specify exact versions for base images
- Run as non-root user when possible
- Use `.dockerignore` to exclude unnecessary files
- Keep containers ephemeral

### 2. Docker Compose
- Use version 3.x+ syntax
- Define resource limits

<!-- Content truncated to meet Windsurf 6KB limit -->

---
> Converted and distributed by [TomeVault](https://tomevault.io/claim/sandraschi) — claim your Tome and manage your conversions.
<!-- tomevault:4.0:windsurf_rules:2026-04-13 -->
