# Voice library options

## Query parameters

| Parameter | Values | Default |
|---|---|---|
| `scope` | `mine`, `library`, `all` | `all` |
| `language` | language identifier | omitted |
| `gender` | `male`, `female`, `neutral` | omitted |
| `limit` | 1–100 | 50 |
| `offset` | 0 or greater | 0 |

`mine` returns private voices belonging to the API key owner. `library` returns system, shared, and public voices. `all` combines and deduplicates both sets.

## Response fields

```json
{
  "voices": [
    {
      "voice_id": 123,
      "voice_hash": "0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef",
      "name": "Warm narrator",
      "description": "Calm long-form narration",
      "source_type": "system",
      "language": "en",
      "gender": "female",
      "age": "adult",
      "accent": "en-us",
      "tags": ["warm", "narration"],
      "created_at": "2026-07-19T12:00:00"
    }
  ]
}
```

The Agent API intentionally omits storage URLs. Use `voice_hash` for synthesis. Show the voice name when asking the user to choose a voice.

Private cloned or uploaded voices can be removed with `DELETE /v1/voices/{voice_id}`. Library voices cannot be deleted.
