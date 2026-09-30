---
name: mcode-tools-master
description: >- Use when this capability is needed.
metadata:
  author: MiniMax-AI
---

# mcode-tools Master

Use the `mcode-tools connector` subcommands through the `bash` tool. The launcher is already on the
current runtime process PATH when this skill is available.

For every multimodal generation or understanding request, search Connector tools before saying the
capability is unavailable. Useful discovery keywords include `image`, `photo`, `video`, `audio`,
`music`, `document`, `generate`, `understand`, and `analyze`.

For an ordinary direct call to a connected plugin or MCP tool already present in the model's tool
list, call that tool directly and do not load this skill solely for access. Use this skill for those
tools only when the task must combine them with Bash scripts, pipes, local files, loops, batch
processing, or other CLI automation.

## Get a Drive Asset URL

When you have a Matrix Drive `node_id` and need a fresh download URL, use the top-level command:

```bash
mcode-tools get_asset_url <node_id>
# Equivalent kebab-case spelling:
mcode-tools get-asset-url <node_id>
```

The command returns JSON such as:

```json
{
  "node_id": "429422773780544",
  "download_url": "https://example.invalid/short-lived-url"
}
```

Unless the user explicitly instructs otherwise, download the asset directly into the current working
directory instead of only returning the `download_url`, then report the saved local path to the
user.

## Upload a Local File

Upload a local file and get a temporary URL with the top-level command:

```bash
mcode-tools upload_temp_url <file_path>
# Equivalent kebab-case spelling:
mcode-tools upload-temp-url <file_path>
# Optional MIME type override:
mcode-tools upload-temp-url <file_path> --mime-type <type>
```

Use the returned `temp_url`.

## Bash Tool Timeout

For generation commands—such as image, video, audio, music, or document generation—invoke `bash`
with `timeout: 600` (10 minutes). In the Bash tool input, `command` and `timeout` are sibling
fields:

```json
{
  "command": "mcode-tools connector call <tool_name> --args-file <path>",
  "timeout": 600
}
```

`timeout` is a top-level `bash` tool input field outside the command string. Never put `--timeout`,
`timeout=600`, or any other timeout argument in the command string: `mcode-tools connector call` has
no timeout option. Discovery and schema inspection commands can use the normal Bash timeout.

## Workflow

1. Discover candidate tools. List all tools only when the task is broad; otherwise narrow the list
   with a keyword:

   ```bash
   mcode-tools connector tools
   mcode-tools connector tools --keyword <text>
   ```

   Do not run `mcode-tools list` or `mcode-tools connector list`; those are not valid discovery
   commands.

2. Inspect the selected tool before calling it. Use the returned `input_schema` to construct the
   arguments and `output_schema` to interpret a successful result; never guess field names or types:

   ```bash
   mcode-tools connector tool <tool_name>
   ```

3. Call the tool with exactly one JSON object. Use inline JSON for small arguments and a file for
   complex, generated, or cross-platform arguments:

   ```bash
   mcode-tools connector call <tool_name> --args '{"key":"value"}'
   mcode-tools connector call <tool_name> --args-file <path>
   mcode-tools connector call <tool_name> --args-file -
   ```

   `--args` and `--args-file` are mutually exclusive. Omitting both sends `{}`. Arrays, scalars, and
   `null` are not valid top-level arguments.

4. A successful `mcode-tools connector call` directly writes the top-level JSON value described by
   the inspected `output_schema` to stdout. Parse that value and return the useful output. Do not
   look for or unwrap `content` or `structuredContent` unless the `output_schema` declares those
   fields. If the command exits non-zero, surface its error code and message. Do not silently switch
   tools or repeatedly retry authentication errors.

## Selection Rules

- Tool names are returned as `tool_name`; pass that exact value to `tool` and `call`.
- Prefer `--keyword` before scanning a large tool catalog. It searches names and descriptions.
- Inspect `input_schema` again when validation fails instead of inventing extra arguments.
- Prefer `--args-file` when shell quoting would be fragile, especially on Windows.

---
> Source: [MiniMax-AI/minimax-code](https://github.com/MiniMax-AI/minimax-code) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-28 -->
