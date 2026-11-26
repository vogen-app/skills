*Create expressive voices. Bring characters to life.*

# VoGen Agent Skills

| Skill | Use |
|---|---|
| [`vogen-setup-api-key`](vogen-setup-api-key/) | Configure and validate a VoGen API key. |
| [`vogen-voice-library`](vogen-voice-library/) | Find voices and their Voice IDs. |
| [`vogen-voice-cloning`](vogen-voice-cloning/) | Clone a private voice from reference audio. |
| [`vogen-emotion-library`](vogen-emotion-library/) | Find emotion references for V1 speech. |
| [`vogen-text-to-speech`](vogen-text-to-speech/) | Generate speech with V2 or V1. |
| [`vogen-sound-effects`](vogen-sound-effects/) | Find and download sound effects. |
| [`vogen-talking-avatar`](vogen-talking-avatar/) | Make an existing avatar speak. |
| [`vogen-voice-design`](vogen-voice-design/) | Design and save a private voice from a description. |
| [`vogen-voice-rewrite`](vogen-voice-rewrite/) | Replace, insert, or delete words in a recording. |
| [`vogen-speech-to-text`](vogen-speech-to-text/) | Transcribe audio with optional timestamps. |

## Install

```bash
npx skills add vogen-app/skills
```

For a manual install, extract [vogen-skills-2.0.0.zip](https://static.vogen.app/skills/vogen-skills-2.0.0.zip) and copy the skill folders to `.agents/skills/` for Codex or Cursor, or `.claude/skills/` for Claude Code. Use the equivalent directory under your home directory for a personal install. When upgrading from 1.x, replace the old unprefixed folders with the new `vogen-*` folders.

## Configure

Create a key and read the API reference at [vogen.app/app/api-keys](https://vogen.app/app/api-keys). Set `VOGEN_API_KEY` in your local environment.

```bash
curl --fail-with-body https://api.vogen.app/v1/user \
  -H "Authorization: Bearer $VOGEN_API_KEY"
```

Keep the key in your local environment. Your agent needs an HTTP or terminal tool to call VoGen. [Pricing and plans](https://vogen.app/pricing)
