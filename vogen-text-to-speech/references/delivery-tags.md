# V2 delivery tags

Annotate the script before `POST /v2/text-to-speech/{voice_id}`. The spoken words, language, and punctuation stay identical to the user's text. Tags are not spoken.

## Opening direction

Every script starts with exactly one square-bracket direction:

- Same language as the script.
- One short phrase, at most 48 characters.
- Describes how to speak the line. It is not a preset tag name.
- Not spoken aloud.

`[语气清晰自然，像在耐心介绍功能]`

Keep an existing short direction. Do not add a second one. Drop a direction longer than 48 characters.

## Emphasis

Prefer `<emphasis>...</emphasis>`. Wrap the short words or phrases a listener should notice. Use it often: a normal sentence often needs more than one. Do not wrap a whole paragraph.

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

`[语气清晰自然，像在耐心介绍功能] 这是一个可以克隆自己声音的网站，<emphasis>你只需要</emphasis>上传一段自己的清晰语音。`
