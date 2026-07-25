---
name: awesome-kubernetes
description: This skill documents the local verification, editing, and deployment procedures for the Antigravity AI Agent when pair-programming with the repository maintainer. Use when this capability is needed.
metadata:
  author: nubenetes
---
# Skill: Local Operations for Awesome-Kubernetes Maintenance

This skill documents the local verification, editing, and deployment procedures for the Antigravity AI Agent when pair-programming with the repository maintainer. 

---

## 🛠️ Local Environment & Python Context

The repository utilizes a virtual environment located in `.venv/` in the project root. Always prefix Python and CLI tool execution with the virtual environment path to ensure the correct dependencies are utilized.

*   **Python Virtual Environment**: `.venv/bin/python`
*   **MkDocs Command**: `.venv/bin/mkdocs`
*   **Pip Dependency Installer**: `.venv/bin/pip`

---

## 🧪 Local Testing & Verification

Before promoting changes to master, always verify changes locally using these commands:

### 1. Markdown Lint Checks
Verify that no syntax or styling violations are present. We ignore line length (MD013), bullet indentation (MD005/007), and other formatting conflicts. Run the linter locally:
```bash
echo '{ "MD004": false, "MD005": false, "MD007": false, "MD009": false, "MD010": false, "MD012": false, "MD013": false, "MD014": false, "MD022": false, "MD028": false, "MD030": false, "MD032": false, "MD033": false, "MD034": false, "MD036": false, "MD038": false, "MD041": false, "MD046": false, "MD047": false, "MD050": false, "MD051": false, "MD055": false, "MD060": false }' > .markdownlint.json
npx markdownlint-cli2 "docs/**/*.md" "v2-docs/**/*.md" "README.md"
```

### 2. Static Build Compilations
Verify that MkDocs compiles the site targets without warnings or invalid path errors:
```bash
.venv/bin/mkdocs build -f mkdocs.yml && .venv/bin/mkdocs build -f v2-mkdocs.yml
```

### 3. V2 Elite Portal Generation (Render-Only)
If you need to manually recompile V2 markdown files from the inventory database (`data/inventory.yaml`) without running heavy API fetches or network sweeps:
```bash
PYTHONPATH=. .venv/bin/python -m src.v2_optimizer --render-only
```

---

## 📦 Git & Release Lifecycle

Always follow this exact branch promotion sequence to ensure clean history and trigger the production pipelines:

### 1. Commit and Push to Develop
Keep the `develop` branch updated with all source modifications:
```bash
git checkout develop
git pull origin develop --no-rebase --no-edit
git add <modified_files>
git commit -m "style/feat/fix: <description>"
git push origin develop
```

### 2. Promote to Master
Promote verified changes to the master branch to trigger pages deployment:
```bash
git checkout master
git pull origin master --no-rebase --no-edit
git merge develop --no-edit
# If conflict occurs in auto-generated files (v2-docs/*), accept ours:
# git diff --name-only --diff-filter=U | xargs git checkout --ours
# git add v2-docs/ && git commit -m "merge develop into master"
git push origin master
git checkout develop
```

### 3. Generate a GitHub Release
Use the GitHub CLI (`gh`) to create a release tag:
```bash
gh release create v<major>.<minor>.<patch> \
  --title "v<major>.<minor>.<patch>: <short description>" \
  --notes "Release summary and key changes"
```

---
> Source: [nubenetes/awesome-kubernetes](https://github.com/nubenetes/awesome-kubernetes) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
