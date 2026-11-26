---
name: vogen-speech-to-text
description: Transcribe local audio with VoGen or align a corrected transcript to its audio. Use for speech-to-text, timestamped transcripts, and locating words for VoGen voice rewrite.
compatibility: Requires internet access and VOGEN_API_KEY.
---

# VoGen speech to text

Upload one file as `audio` to `POST https://api.vogen.app/v2/speech-to-text` with Bearer authentication. Supported audio formats are WAV, MP3, FLAC, OGG, M4A, and WebM, up to 90 MiB and 60 minutes. `language` defaults to `auto`; explicit languages use names such as `English` or `Chinese`. `enable_timestamps` defaults to true. To align corrected text, send `transcript` (up to 4,000 characters and two minutes of audio).

```bash
curl --fail-with-body -X POST https://api.vogen.app/v2/speech-to-text \
  -H "Authorization: Bearer $VOGEN_API_KEY" \
  -F "audio=@recording.wav" \
  -F "enable_timestamps=true"
```

Poll `GET /v2/speech-to-text/tasks/{task_id}`. Deliver `text` as plain text or a file as requested. `time_stamps` contains `text`, `start_time`, and `end_time` in seconds when available for the detected language. Keep the task ID when passing the recording to `vogen-voice-rewrite`. Report unavailable timestamps where needed and resume a running task by ID.

Use `vogen-setup-api-key` if needed.
