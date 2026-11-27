---
name: vogen-text-to-speech
description: Generate speech with VoGen from a named or cloned voice. Use for narration, voiceovers, announcements, multilingual speech, and dialogue. Defaults to V2, annotating the script with a short opening direction and emphasis before synthesis. Supports V1 for explicit language or emotion controls.
metadata:
  openclaw:
    requires:
      - VOGEN_API_KEY
    primaryEnv: VOGEN_API_KEY
---

# VoGen text to speech

Use the Voice ID copied from VoGen or resolve a name to `voice_hash` with `vogen-voice-library`. Send the value as returned. Use `vogen-setup-api-key` if the key is missing.

## Generate with V2

Prepare the user's script before sending it. Keep every spoken character and its punctuation. Add delivery markup only, using [delivery tags](references/delivery-tags.md).

1. Start with one short square-bracket direction in the script's language. One phrase, at most 48 characters. It describes how to speak the line and is not spoken. Do not use a preset tag name there.
2. Wrap the short words or phrases a listener should notice in `<emphasis>...</emphasis>`. Use it often. A normal sentence often needs more than one.
3. Add another listed tag only when the line clearly needs that emotion or pace. Place an inline tag before a clause, followed by a space. Do not nest span tags.
4. Remove any other bracket or angle tag. If a short opening direction is already present, keep that one.
5. Submit that annotated string once to `POST https://api.vogen.app/v2/text-to-speech/{voice_id}` with Bearer authentication and JSON. `text` is 1–2,000 characters including the tags. Optionally send `reference_text` (the exact transcript of the voice's reference recording). If the user explicitly asks for the wording with no delivery markup, send the original text unchanged.
6. Keep the returned `task_id`. Poll `GET /v2/audio/tasks/{task_id}` until `completed`, `failed`, or `cancelled`. Allow several seconds between polls. Resume a running job using its task ID.
7. On completion, call `GET /v2/audio/tasks/{task_id}/download`. Download the signed `url` promptly without forwarding the API key. Save the WAV and verify it plays. For `vogen-talking-avatar`, pass the completed task ID as `source_audio_task_id`.

```bash
curl --fail-with-body -X POST "https://api.vogen.app/v2/text-to-speech/VOICE_HASH" \
  -H "Authorization: Bearer $VOGEN_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"text":"[clear and welcoming] Welcome to the <emphasis>studio</emphasis>."}'
```

## When to use V1

Use [V1 options](references/options.md) when the user explicitly requests V1 or needs its language selection, automatic translation, or emotion controls. Use `?voice_id_type=hash` when passing a `voice_hash` to V1. V1 streams MP3 and returns `X-Vogen-Task-Id` for composition as `source_tts_task_id`.

For a default V2 request, V1 fallback is allowed once when the V2 route is absent, the API explicitly reports queue unavailability before accepting the job, or the job is terminal `failed` with `credits_cost=0` and no result. Use fallback only when V1 can preserve the requested options. Honor explicit V2 requests. Auth, voice access, credits, validation, and queue limit errors require their own resolution. On a transport timeout or unknown submission result, avoid automatic resubmission or fallback. Keep a known task ID and check its status.

See [errors](references/errors.md) for handling a failed or incomplete MP3 response.
