---
name: music
description: >- Use when this capability is needed.
metadata:
  author: guaardvark
---

# Music and sound effects with Guaardvark

Read `setup` first; needs the `audio_foundry` plugin. `B=${GUAARDVARK_URL:-http://localhost:5000}`.
ACE-Step takes ~10 GB VRAM; the orchestrator evicts other models while it runs.

## A song

```bash
curl -s -X POST $B/api/audio-foundry/generate/music -H 'Content-Type: application/json' -d '{
  "style_prompt": "indie folk, fingerpicked acoustic guitar, warm male vocal, 96 bpm, intimate",
  "lyrics": "[verse]\nLines here\n[chorus]\nHook here",
  "negative_prompt": "distorted, muddy, synth",
  "duration_s": 90, "instrumental_only": false,
  "output_format": "wav", "seed": 1234, "async": true
}'
```
- `style_prompt` uses ACE-Step's tag vocabulary: genre, instruments, mood, tempo, vocal type.
  Vague words ("professional", "futuristic") drift to the model's prior; be concrete, and use
  `negative_prompt` to push away from it. `POST $B/api/audio-foundry/rewrite-music-prompt`
  turns plain English into the tag form when the user wants help.
- `lyrics` with `[verse]` / `[chorus]` / `[bridge]` markers; omit or set `instrumental_only: true`.
- `duration_s` up to 240. Always send `"async": true` for anything over a few seconds.
- Response `202 {"job_id"}` → poll `GET $B/api/audio-foundry/jobs/<job_id>`; done when `status`
  is `done`, with `path`, `document_id`, `duration_s`, `seed`. Reuse the seed to reproduce a take.

## A sound effect or ambience

```bash
curl -s -X POST $B/api/audio-foundry/generate/fx -H 'Content-Type: application/json' -d '{
  "prompt": "rain on a tin roof, distant thunder, no music", "duration_s": 20, "output_format": "wav", "async": true
}'
```
`duration_s` up to 47. Same job polling.

## Then

- A finished song can go straight into the music skill-video as the `song`.
- Jobs: `GET $B/api/audio-foundry/jobs` lists, `DELETE` clears finished ones.
- Attribution comes back in the job result; keep it with the file if the user publishes.

---
> Source: [guaardvark/guaardvark](https://github.com/guaardvark/guaardvark) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-13 -->
