# Talking avatar options

- Authenticate with the existing `VOGEN_API_KEY`. List owner avatars and looks at `GET /v2/talking-avatar/avatars`, with optional `search`.
- Select one `avatar_id` (first available look) or `look_id`. Both are public IDs obtained from the list.
- Provide exactly one of `audio` (local WAV, MP3, FLAC, OGG, M4A, or WebM up to 25 MiB), `source_tts_task_id` (V1), or `source_audio_task_id` (V2). Tasks must be completed and belong to the API key owner.
- Maximum input duration is 5 seconds for Hobby and 30 seconds for active Basic, Starter, Pro, Ultra, and Business. Ask for a shorter input if necessary.
- `aspect_ratio` defaults to `16:9`. Also supports `4:3`, `1:1`, `3:4`, and `9:16`. `prompt` supports up to 200 characters and `use_enhanced` defaults to false.

The waiter polls `GET /v2/talking-avatar/tasks/{task_id}` and downloads the signed `video_url` without forwarding authentication. It checks every 20 seconds for up to 90 minutes.
