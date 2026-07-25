---
name: scaffold-python-recipe
description: > Use when this capability is needed.
metadata:
  author: google
---

# Scaffolding a New Python ADK Sample

Use this skill to scaffold a new Python ADK sample recipe inside this repository using the automated script at `scripts/scaffold.py`.

---

## Rules

1. **No Manual Boilerplate Writing**: Always use `scripts/scaffold.py` to create the recipe. Never write the boilerplate files manually.
2. **Do Not Modify After Scaffolding**: Once the script runs successfully, do not make any further changes to the recipe in this turn.
3. **Use the Correct Terminology (Recipe)**: Always refer to what is being created as a **recipe**, never as a "project". Ensure all output messages, instructions, and explanations to the user use "recipe" exclusively.

---

## Inputs

You **must** have both pieces of information below before running the script. If either is missing or was not explicitly provided by the user, **ask for it** — do not assume or use a default.

### 1. Output Directory (Required — must ask if not provided)

The user must choose one of these two valid locations:
- `contrib/`
- `core/python/`

If the user has not specified which directory, ask them to choose. Do not proceed until a valid choice is confirmed.

### 2. Recipe Name (Required — must ask if not provided)

The recipe name must satisfy **all** of the following rules:
- Contains only lowercase letters and hyphens (`a-z`, `-`)
- Is 30 characters or less
- Does not start or end with a hyphen

If the user provided a name, validate it against these rules before proceeding. If it is invalid, explain which rule it violates and ask for a corrected name. Do not proceed until a valid name is confirmed.

---

## Run

Execute the scaffold script:
```bash
python3 .agents/skills/scaffold-python-recipe/scripts/scaffold.py --name <RECIPE_NAME> --output-dir <OUTPUT_DIRECTORY>
```
*The script accepts exactly two flags: `--name` (required) and `--output-dir` (required). Do not pass any other flags.*

---
## Respond

Once the script succeeds, inform the user the recipe is ready and highlight the following required next steps:

1. **Update `manifest.yaml`**: Fill in the `description`, `ownership.team`, and `ownership.poc` fields (placeholders are marked with `TODO:`). This file is validated by CI and must not contain placeholder values. Use the `generate-manifest` skill if you want it populated automatically from the source code.
2. **Update `README.md`**: Replace the generic title and description with details specific to this recipe (ownership/POC live in `manifest.yaml`, above — not in the README).

Then, provide these quick-start commands:
```bash
cd <OUTPUT_DIRECTORY>/<RECIPE_NAME>
uv sync                  # install dependencies
uv run pytest            # run the test suite
uv run adk run app       # run the agent interactively
```
Do not make any further changes. End your turn.

---
> Source: [google/adk-samples](https://github.com/google/adk-samples) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
