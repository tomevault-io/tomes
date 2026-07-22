---
name: test-proxy
description: Push test-proxy recordings/assets using the test-proxy CLI (e.g., test-proxy push -a assets.json). Use when publishing recordings. Use when this capability is needed.
metadata:
  author: Azure
---

# Test Proxy Recordings

Use this skill to publish recordings to the test-proxy assets repo.

## Command
```bash
test-proxy push -a assets.json
```

## Steps
1. Check if `test-proxy` is installed by running `test-proxy --version`.
   - If the command is **not found**, install it (see [Installation](#installation) below).
2. Confirm the assets file path (default: `assets.json` in the current directory).
3. If the file location is unclear, search for it or ask the user.
4. Run `test-proxy push -a <assets-file>`.
5. Report success or any errors.

## Installation

If `test-proxy` is missing, install it as a .NET global tool.

### Prerequisites
.NET 8.0 (LTS) or later must be installed. Verify with `dotnet --version`.
If missing, ask the user to install the .NET SDK from https://dotnet.microsoft.com/download.

### Install command
```powershell
dotnet tool update azure.sdk.tools.testproxy --global --prerelease --add-source https://pkgs.dev.azure.com/azure-sdk/public/_packaging/azure-sdk-for-net/nuget/v3/index.json --ignore-failed-sources
```

After installation, verify with `test-proxy --version`.

---
> Source: [Azure/azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
