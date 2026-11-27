# V2 delivery tags

Annotate the script before `POST /v2/text-to-speech/{voice_id}`. The spoken words, language, and punctuation stay identical to the user's text. Tags are not spoken.

## Opening direction

Every script starts with exactly one square-bracket direction:

- Same language as the script.
- One short phrase, at most 48 characters.
- Describes how to speak the line. A single preset label is not a direction: `[自信]` and `[confident]` are wrong.
- Not spoken aloud.

`[语气清晰自然，像在耐心介绍功能]`

Keep an existing short direction. Do not add a second one. Drop a direction longer than 48 characters.

## Emphasis

Wrap exactly one or two short words that carry the point in `<emphasis>...</emphasis>`. Do not mark every clause, and do not wrap a whole phrase when one word is enough. A paragraph with no emphasis, or with emphasis on every phrase, is wrong.

## Other tags

Add these only when the line clearly needs that emotion or pace.

Inline tags go before a clause, followed by a space:

`[angry]` `[sad]` `[embarrassed]` `[excited]` `[confident]` `[disappointed]` `[relieved]` `[worried]` `[bored]` `[whispering]` `[breathy]` `[laughing]` `[chuckling]` `[sobbing]` `[crying loudly]` `[groaning]` `[sighing]` `[sighs]` `[gasps]` `[pause]` `[clear throat]`

Use a single brief `[pause]` only where an extra break is needed.

Span tags wrap a short phrase. Do not nest them:

`<whisper>...</whisper>` `<emphasis>...</emphasis>` `<stress>...</stress>` `<slow>...</slow>` `<fast>...</fast>`

Remove every other bracket or angle tag. `emphasis` is the span to reach for first.

## Example

User text:

`这是一个可以克隆自己声音的网站，你只需要上传一段自己的清晰语音。`

Annotated text:

`[语气清晰自然，像在耐心介绍功能] 这是一个可以克隆自己声音的网站，你只需要上传一段自己的<emphasis>清晰</emphasis>语音。`
