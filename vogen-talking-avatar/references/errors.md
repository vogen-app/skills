# Talking avatar errors

- `API_KEY_REQUIRED`, `INVALID_API_KEY`: validate the local key with `vogen-setup-api-key`.
- `CHARACTER_LOOK_NOT_FOUND`: list the user's existing avatars and select an active look.
- `TTS_TASK_NOT_FOUND`: check that the audio task exists and belongs to the account.
- If V2 source audio is unavailable, check the audio task and wait for it to complete before submitting.
- `AUDIO_DURATION_LIMIT`, `DIGITAL_HUMAN_FREE_AUDIO_TOO_LONG`, `DIGITAL_HUMAN_AGENT_AUDIO_TOO_LONG`: ask for a shorter audio source.
- `INSUFFICIENT_CREDITS`: report the limit and link to [VoGen pricing](https://vogen.app/pricing).
- If polling or download stalls, check the existing task again and refresh the signed link. A lost submission response is not a reason to submit automatically again.
