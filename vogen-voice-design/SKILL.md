---
name: vogen-voice-design
description: Create a new private VoGen voice from a written description and generate a playable sample. Use for designing an original voice when no reference recording is supplied.
compatibility: Requires internet access and VOGEN_API_KEY.
---

# VoGen voice design

Send the user's description (up to 800 characters) to `POST https://api.vogen.app/v2/voice-design` with Bearer authentication. Optionally send `name`, `text` for the spoken sample (up to 80 characters), and `language` for the voice in the library. VoGen supplies any omitted title or spoken line.

```bash
curl --fail-with-body -X POST https://api.vogen.app/v2/voice-design \
  -H "Authorization: Bearer $VOGEN_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"description":"Warm, measured narrator","name":"Studio narrator"}'
```

Poll `GET /v2/audio/tasks/{task_id}`. When completed, call `GET /v2/audio/tasks/{task_id}/download` and save the signed `url` to a WAV file. Use the returned `voice_hash` with `vogen-text-to-speech`. When `save_status=slot_limit`, deliver the sample and report that it could not be saved. A running job or an ambiguous submission should not be submitted again automatically.

Use `vogen-setup-api-key` if needed.
