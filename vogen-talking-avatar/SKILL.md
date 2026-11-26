---
name: vogen-talking-avatar
description: Make an existing VoGen avatar speak from a script or audio. Use for presenter, talking-head, and lip-sync videos when the user can choose an Avatar ID or Look ID from their account.
compatibility: Requires internet access, VOGEN_API_KEY, and Python 3 for the background waiter.
metadata:
  openclaw:
    requires:
      - VOGEN_API_KEY
    primaryEnv: VOGEN_API_KEY
---

# VoGen talking avatar

1. Ask the user to choose an existing Avatar ID or Look ID if they have not supplied one. List their avatars with `GET https://api.vogen.app/v2/talking-avatar/avatars` using Bearer authentication. Show each relevant avatar name and available look previews. An Avatar ID uses its first available look. If no avatars are available, say so.
2. Choose one audio source. Use the supplied local audio, a completed `source_audio_task_id` from V2, or a completed `source_tts_task_id` from V1. For a script, use `vogen-text-to-speech`. Confirm that duration fits the account limit of 5 seconds on Hobby or 30 seconds on an eligible paid plan.
3. Send one multipart request to `POST /v2/talking-avatar/tasks` and keep the returned task ID. Supply either `avatar_id` or `look_id`. Start the bundled waiter to query status and download the video. If the waiter times out, resume the same task.

```bash
curl --fail-with-body -X POST "https://api.vogen.app/v2/talking-avatar/tasks" \
  -H "Authorization: Bearer $VOGEN_API_KEY" \
  -F "look_id=LOOK_ID" \
  -F "source_audio_task_id=42" \
  -F "aspect_ratio=16:9"
```

```bash
python3 "<skill-directory>/scripts/wait_for_video.py" --task-id "$TASK_ID"
```

Report the downloaded MP4 path, or the current status and expected output path if generation continues in the background. Read [options](references/options.md) and [errors](references/errors.md) when needed.
