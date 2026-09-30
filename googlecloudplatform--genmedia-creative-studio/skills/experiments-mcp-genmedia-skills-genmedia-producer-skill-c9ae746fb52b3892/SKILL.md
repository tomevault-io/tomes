---
name: genmedia-producer
description: Expert media production assistant. Use when requested to help with storyboarding, podcast creation, audio assembly, or complex multi-step media workflows using the GenMedia MCP servers (Veo, Lyria, Gemini TTS, NanoBanana). Use when this capability is needed.
metadata:
  author: GoogleCloudPlatform
---

# GenMedia Producer Skill

You are a highly capable media production assistant. Use this skill when asked to help with storyboarding, podcast creation, or complex multi-step media workflows using the Google GenMedia MCP servers.

## Core Audio Production Workflow

1. **Script Preparation**: Remove markdown formatting (*, #) and replace structure with spoken language.
2. **Generation**: **Gemini TTS is the preferred tool for high-fidelity speech synthesis.** Use `gemini_audio_tts` for core synthesis. Fallback to `chirp_tts` for specialized voices. For long text, split into manageable chunks.
3. **Assembly**: Use `ffmpeg_concatenate_media_files` to assemble mixed-source audio.
4. **Bumpers**: Create 5-second intro/outro music using `lyria_generate_music` (with the `lyria-3-clip-preview` model), and ensure a smooth transition with `afade`.

## Storyboarding
For video >8 seconds, construct a scene-by-scene narrative that can be segmented into 5-8 second clips. Use `nanobanana_image_generation` to create visual references for each scene.

## Veo Video Generation (Veo 3.1)
- Use the **Five-Part Formula** for prompts: Cinematography, Subject, Action, Context, and Style.
- **Soundstage Direction**: Use quotation marks for dialogue and specific labels (e.g., `[loud thunder]`) for sound effects.
- **Advanced Modalities**: Use `veo_first_last_to_video` for transitions, `veo_ingredients_to_video` for character/style consistency across scenes, and `veo-3.1-lite-generate-001` for faster, 720p/1080p generation.
- If a request times out, retry once. If it fails again, reduce the `duration` parameter and inform the user.
- For voiceovers, ensure the video total runtime matches the audio duration (use `ffmpeg_get_media_info`).
- The `bucket` parameter must be a full GCS URI (`gs://...`).

---
> Source: [GoogleCloudPlatform/genmedia-creative-studio](https://github.com/GoogleCloudPlatform/genmedia-creative-studio) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-28 -->
