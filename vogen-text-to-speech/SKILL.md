---
name: vogen-text-to-speech
description: Generate speech with VoGen from a named or cloned voice. Use for narration, voiceovers, announcements, multilingual speech, and dialogue. Defaults to V2 and supports V1 for explicit language or emotion controls.
compatibility: Requires internet access and VOGEN_API_KEY.
metadata:
  openclaw:
    requires:
      - VOGEN_API_KEY
    primaryEnv: VOGEN_API_KEY
---

# VoGen text to speech

Use the Voice ID copied from VoGen or resolve a name to `voice_hash` with `vogen-voice-library`. A Voice ID for V2 is a 64-character hash. Use `vogen-setup-api-key` if the key is missing.

## Generate with V2

1. Submit once to `POST https://api.vogen.app/v2/text-to-speech/{voice_id}` with Bearer authentication and JSON. Send `text` (1–2,000 characters) and optionally `reference_text` (the exact transcript of the voice's reference recording).
2. Keep the returned `task_id`. Poll `GET /v2/audio/tasks/{task_id}` until `completed`, `failed`, or `cancelled`. Allow several seconds between polls. Resume a running job using its task ID.
3. On completion, call `GET /v2/audio/tasks/{task_id}/download`. Download the signed `url` promptly without forwarding the API key. Save the WAV and verify it plays. For `vogen-talking-avatar`, pass the completed task ID as `source_audio_task_id`.

```bash
curl --fail-with-body -X POST "https://api.vogen.app/v2/text-to-speech/VOICE_HASH" \
  -H "Authorization: Bearer $VOGEN_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"text":"Welcome to the studio."}'
```

## When to use V1

Use [V1 options](references/options.md) when the user explicitly requests V1 or needs its language selection, automatic translation, or emotion controls. V1 accepts both numeric IDs and hashes, streams MP3, and returns `X-Vogen-Task-Id` for composition as `source_tts_task_id`.

For a default V2 request, V1 fallback is allowed once when the V2 route is absent, the API explicitly reports queue unavailability before accepting the job, or the job is terminal `failed` with `credits_cost=0` and no result. Use fallback only when V1 can preserve the requested options. Honor explicit V2 requests. Auth, voice access, credits, validation, and queue limit errors require their own resolution. On a transport timeout or unknown submission result, avoid automatic resubmission or fallback. Keep a known task ID and check its status.

See [errors](references/errors.md) for handling a failed or incomplete MP3 response.
