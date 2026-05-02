---
name: docker-lint
description: This skill uses **hadolint** (Dockerfile linter) to check Docker image build files for best practices, ensuring: Use when this capability is needed.
metadata:
  author: y1feng200156
---
---
name: docker-lint
description: Dockerfile best practices check - Use hadolint to validate Dockerfile security, performance, and compliance
---

# Docker Lint Skill

## 📋 Overview

This skill uses **hadolint** (Dockerfile linter) to check Docker image build files for best practices, ensuring:

- 🔒 Security (non-root user, minimal privileges)
- ⚡ Performance optimization (layer caching, multi-stage builds)
- 📏 Standard compliance (Docker official best practices)
- 🐛 Common error detection (typos, invalid instructions)

## 🔧 Prerequisites

| Tool | Min Version | Check Command | Installation |
|------|-------------|---------------|--------------|
| Docker | 20.10+ | `docker --version` | [docker.com](https://www.docker.com/) |
| hadolint | 2.12+ | `hadolint --version` | See installation below |

### Installing hadolint

**Windows (Scoop recommended):**

```powershell
scoop install hadolint
```

**Linux:**

```bash
wget -O /usr/local/bin/hadolint https://github.com/hadolint/hadolint/releases/latest/download/hadolint-Linux-x86_64
chmod +x /usr/local/bin/hadolint
```

**macOS:**

```bash
brew install hadolint
```

**Docker (all platforms):**

```bash
docker pull hadolint/hadolint
```

> **Note**: The script will auto-detect and prompt for installation, supporting Docker container run mode.

## 🚀 Usage

### Method 1: Use AI Assistant

```
"Use docker-lint skill to check my Dockerfile"
```

### Method 2: Run Script Directly

**Check single Dockerfile:**

```powershell
# Windows
.\.agent\skills\docker-lint\scripts\lint.ps1

# Linux/Mac
./.agent/skills/docker-lint/scripts/lint.sh
```

**Check specific file:**

```powershell
# Windows
.\.agent\skills\docker-lint\scripts\lint.ps1 -File ".\docker\Dockerfile.prod"

# Linux/Mac
./.agent/skills/docker-lint/scripts/lint.sh docker/Dockerfile.prod
```

**Check all Dockerfiles in directory:**

```powershell
# Windows
.\.agent\skills\docker-lint\scripts\lint.ps1 -Path ".\containers" -Recursive

# Linux/Mac
./.agent/skills/docker-lint/scripts/lint.sh -r containers/
```

## 🎯 What It Checks

### Security Checks

- ✅ **DL3002**: Prohibit running container as root user
- ✅ **DL3008**: Pin apt-get package versions
- ✅ **DL3013**: Pin pip package versions
- ✅ **DL3059**: Multi-stage build health check
- ✅ **SC2046**: Shell script injection protection

### Performance Optimization

- ✅ **DL3003**: Use `WORKDIR` instead of `cd`
- ✅ **DL3009**: Clean apt cache
- ✅ **DL3015**: Avoid unnecessary package updates
- ✅ **DL3020**: Use `COPY` instead of `ADD`
- ✅ **DL3045**: Layer cache optimization

### Standard Compliance

- ✅ **DL3006**: Specify base image tag
- ✅ **DL3007**: Avoid using `latest` tag
- ✅ **DL3025**: Use JSON format for CMD/ENTRYPOINT
- ✅ **DL4000**: `MAINTAINER` is deprecated

## 📊 Output Example

```
🐳 Docker Lint - Checking Dockerfile...

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📁 File: Dockerfile
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Dockerfile:1 DL3006 warning: Always tag the version of an image explicitly
FROM python:3
     ^


Dockerfile:5 DL3008 warning: Pin versions in apt-get install
RUN apt-get update && apt-get install -y git
                                         ^


Dockerfile:15 DL3002 error: Last USER should not be root
USER root
^

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 Check Results:
   ❌ Errors: 1
   ⚠️  Warnings: 2
   💡 Info: 0
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 Suggestions:
1. Pin base image version: FROM python:3.11-slim
2. Pin apt package version: git=1:2.34.1-1ubuntu1.10
3. Use non-root user: USER appuser
```

## ⚙️ Configuration

Create `.hadolint.yaml` in the project root to customize rules:

```yaml
# .hadolint.yaml
ignored:
  - DL3008  # Allow unpinned apt package versions (dev environment)

trustedRegistries:
  - docker.io
  - gcr.io
  - ghcr.io

label-schema:
  author: email
  version: semver

# Custom severity
override:
  error:
    - DL3002  # root user is error level
  warning:
    - DL3008  # unpinned version is warning level
  info:
    - DL3015  # package update suggestion is info level
```

## 🛠️ Dockerfile Fix Example

**Problem Dockerfile:**

```dockerfile
FROM python:3
RUN apt-get update && apt-get install -y git
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
USER root
CMD python app.py
```

**Fixed Dockerfile:**

```dockerfile
# Pin base image version
FROM python:3.11-slim

# Create non-root user
RUN groupadd -r appuser && useradd -r -g appuser appuser

# Pin package versions and clean cache
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        git=1:2.34.1-1ubuntu1.10 && \
    rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Copy dependency file first (leverage caching)
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Then copy application code
COPY --chown=appuser:appuser . .

# Switch to non-root user
USER appuser

# Use JSON format
CMD ["python", "app.py"]
```

## 🔗 CI/CD Integration

### GitHub Actions

```yaml
name: Lint Dockerfile
on: [push, pull_request]

jobs:
  hadolint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: hadolint/hadolint-action@v3.1.0
        with:
          dockerfile: Dockerfile
```

### GitLab CI

```yaml
hadolint:
  image: hadolint/hadolint:latest-alpine
  script:
    - hadolint Dockerfile
```

## 🆘 FAQ

**Q: What if hadolint is not installed?**  
A: The script will automatically try to run hadolint using Docker container

**Q: How to ignore specific rules?**  
A: Add a comment in the Dockerfile:

```dockerfile
# hadolint ignore=DL3008
RUN apt-get install -y git
```

**Q: Does it support multi-stage builds?**  
A: Fully supported, hadolint checks best practices for each stage

**Q: Can it check docker-compose.yml?**  
A: hadolint focuses on Dockerfile, use `docker-compose config --quiet` for docker-compose validation

---
> Converted and distributed by [TomeVault](https://tomevault.io) | [Claim this content](https://tomevault.io/claim/y1feng200156/ham-study)
<!-- tomevault:3.0:skill_md:2026-04-07 -->
