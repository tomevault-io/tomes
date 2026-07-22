---
name: supermachine-api
description: Generate and retrieve Supermachine AI images through its REST API using a macOS Keychain-stored API key. Use for credit-based Supermachine image work; excludes GEM and video generation. Use when this capability is needed.
metadata:
  author: RichardGeorgeDavis
---

# Supermachine API

Use this skill for Supermachine image-generation work through
`https://dev.supermachine.art/v1`.

## Plan boundary

This workspace operator has a Supermachine Lifetime Deal 3X plan with 3,000
credits per monthly cycle. It has no gems and must not use video endpoints.

- Use standard credit-based image models only.
- Do not call `POST /v1/generate/gem`, `GET /v1/videos`, or any video/GEM model.
- Before a substantial batch, check the balance with `GET /v1/user` and inspect
  available non-GEM models with `GET /v1/models`.
- Treat the returned model list and its supported resolutions as authoritative;
  model availability and credit costs can change.

## Key storage

The API key is stored only in the logged-in macOS user's Keychain:

- service: `supermachine-api`
- account: `default`

Do not place it in source, a prompt, `.env`, shell history, logs, or generated
artifacts. Install or replace it interactively:

```sh
shared/skills/supermachine-api/scripts/supermachine-keychain.sh set
```

Verify that the Keychain item exists without exposing its value:

```sh
shared/skills/supermachine-api/scripts/supermachine-keychain.sh verify
```

## API portal, key source, and authoritative documentation

- API documentation home: <https://devs.supermachine.art/>.
- API base URL: `https://dev.supermachine.art/v1`.
- Get or copy an API key: sign in at <https://supermachine.art/>, open Profile
  Settings, then copy the API key shown there. The official authentication
  guide is <https://devs.supermachine.art/authentication>.
- Test the stored key and show the plan, credits, and gems with the `status`
  command below. It uses `GET /v1/user` and does not spend credits.
- API reference: <https://devs.supermachine.art/reference>. Consult the live
  documentation before using an endpoint or option not covered by this skill.

The official documentation is the source of truth. Its relevant sections are:

| Area | Official page | Skill policy |
| --- | --- | --- |
| Authentication, rate limits, errors | [/authentication](https://devs.supermachine.art/authentication), [/rate-limits](https://devs.supermachine.art/rate-limits), [/errors](https://devs.supermachine.art/errors) | Use a Keychain key, bearer auth, and stay within the documented 10 requests/minute. |
| Images and polling | [/generate/images](https://devs.supermachine.art/generate/images), [/generate/polling](https://devs.supermachine.art/generate/polling), [/media/images](https://devs.supermachine.art/media/images) | Supported: generate, poll, list, and download. Never delete through this skill. |
| Models and image resources | [/resources/models](https://devs.supermachine.art/resources/models), [/resources/loras](https://devs.supermachine.art/resources/loras), [/resources/characters](https://devs.supermachine.art/resources/characters), [/resources/folders](https://devs.supermachine.art/resources/folders) | Read live metadata before selecting a model or resolution. |
| Credit-based image tools | [/tools](https://devs.supermachine.art/tools), [/tools/image-to-prompt](https://devs.supermachine.art/tools/image-to-prompt), [/tools/remove-background](https://devs.supermachine.art/tools/remove-background), [/tools/faceswap](https://devs.supermachine.art/tools/faceswap), [/tools/upscale](https://devs.supermachine.art/tools/upscale), [/tools/instruct](https://devs.supermachine.art/tools/instruct), [/tools/flux-img2img](https://devs.supermachine.art/tools/flux-img2img) | Check cost and obtain user approval before a billable tool run. |
| GEM/video features | [/resources/gems](https://devs.supermachine.art/resources/gems), [/generate/videos](https://devs.supermachine.art/generate/videos), [/media/videos](https://devs.supermachine.art/media/videos) | Explicitly excluded: this plan has no gems. |

## Standard workflow

1. Check plan/balance and inspect eligible models:

   ```sh
   shared/skills/supermachine-api/scripts/supermachine-images.sh status
   shared/skills/supermachine-api/scripts/supermachine-images.sh models
   ```

2. Generate an image. Select a listed, non-GEM image model and one of its
   supported resolutions:

   ```sh
   shared/skills/supermachine-api/scripts/supermachine-images.sh generate \
     --model "Supermachine NextGen" \
     --prompt "An editorial photograph of a quiet reading room at dawn" \
     --width 1024 \
     --height 768 \
     --output /absolute/path/to/reading-room.png
   ```

   Optional controls are `--negative-prompt`, `--steps`, `--guidance`,
   `--seed`, `--count` (maximum 4), `--folder-id`, `--poll-seconds`, and
   `--timeout-seconds`.

3. The helper submits `POST /v1/generate`, polls `GET /v1/images?batchId=…`,
   and downloads the completed image URL(s) only if `--output` is supplied.
   A batch downloads as `name-1.ext`, `name-2.ext`, and so on.

4. Export every completed image currently visible through the API. This is a
   download-only operation; it does not alter Supermachine or spend credits:

   ```sh
   shared/skills/supermachine-api/scripts/supermachine-images.sh download-all \
     --output-dir /absolute/path/to/supermachine-image-archive
   ```

   Add `--folder-id 123` to export one folder. The helper requests the
   documented 20-image pages, creates a `manifest.json` of API metadata, and
   writes files as `<image-id>.<extension>`. It skips already downloaded files
   by default; use `--overwrite` only to download them again.

5. Archive generation metadata without downloading image files:

   ```sh
   shared/skills/supermachine-api/scripts/supermachine-images.sh archive-metadata \
     --output-dir /absolute/path/to/supermachine-metadata
   ```

   This writes `index.md` plus one Markdown file per API `batchId`, so a
   multi-image generation is described once instead of duplicated per image.
   Each record includes the model, prompt, negative prompt, size, steps,
   guidance, seed, folder, image IDs, URLs, status, and creation times returned
   by the API. It also stores `images.json` as a faithful local source snapshot.
   Re-running the command deduplicates by image ID and rewrites a batch file
   only when its content changes. Add `--folder-id 123` to scope the archive.

## Guardrails

- Ask for explicit approval before generating a batch larger than four images
  or a run likely to materially consume credits.
- Ask for explicit approval before downloading an entire library: it may be
  large and exposes all returned prompts/metadata in the local manifest.
- Treat metadata archives as private content: prompts, image URLs, and folder
  data may be sensitive. Store them only in a user-approved local directory.
- Do not echo a bearer token. Avoid verbose curl tracing and `set -x`.
- Do not guess model names, cost, or valid dimensions: use `models` first.
- Poll every 2–3 seconds; default time limit is five minutes.
- Preserve the `batchId` and returned URLs in task output only; they are not
  credentials.
- If the key may be exposed, revoke/regenerate it in Supermachine, then run
  the Keychain setup command again.

## API facts verified on 2026-07-12

- Authentication: `Authorization: Bearer <API_KEY>`.
- User/balance: `GET /v1/user`.
- Image model catalogue: `GET /v1/models`.
- Image generation: `POST /v1/generate`.
- Image result polling: `GET /v1/images?batchId=<id>`.
- Image-library pagination: `GET /v1/images?page=<n>&perPage=20`, optionally
  filtered with `folderId`; response includes `items` and `pagination`.
- Standard images consume credits; the documentation states typical image
  generation costs of 1–4 credits depending on resolution.

Source: <https://devs.supermachine.art/>.

---
> Source: [RichardGeorgeDavis/Codex-Workspace](https://github.com/RichardGeorgeDavis/Codex-Workspace) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-22 -->
