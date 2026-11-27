---
name: vogen-voice-rewrite
description: Replace, insert, or delete speech within an existing VoGen-compatible recording up to 30 seconds. Use a time range or identify the original words to rewrite.
---

# VoGen voice rewrite

Use `POST https://api.vogen.app/v2/voice-rewrite` with Bearer authentication and multipart form fields. Use one source, `audio` (a local file up to 25 MiB and 30 seconds) or `source_stt_task_id` (completed and owned by the account). Send `edit_op=replace|insert|delete`.

- **Time range.** Provide `start_seconds`, `end_seconds`, original `source_text`, and the full edited `text` (up to 2,000 characters). A completed transcription can supply the original text. Use `vogen-speech-to-text` to build a reliable transcript and selected span when the full edited text needs to be derived from the recording.
- **Original phrase.** Use `vogen-speech-to-text` with timestamps and pass its completed `source_stt_task_id`. Send `target_phrase` and `replacement_text` for replace or insert. Insert defaults to `insert_position=after` and also accepts `before`. When the phrase repeats or lacks reliable timestamps, ask for the intended time range and original text. A corrected transcript can be aligned to obtain better timestamps.

```bash
curl --fail-with-body -X POST https://api.vogen.app/v2/voice-rewrite \
  -H "Authorization: Bearer $VOGEN_API_KEY" \
  -F "source_stt_task_id=42" \
  -F "target_phrase=Friday" \
  -F "edit_op=replace" \
  -F "replacement_text=Monday"
```

Poll `GET /v2/audio/tasks/{task_id}` until terminal. Download the completed MP3 using `GET /v2/audio/tasks/{task_id}/download`. Keep the original recording and return the edited file. Resume a running request by task ID.
