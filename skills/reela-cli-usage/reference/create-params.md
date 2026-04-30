# Reela Create — Supplementary Notes

> For the full parameter list, run `reela create -h`.

## Visual Combinations

Multiple visual types can be combined with commas: `--visual avatar,original-clip,ai-video`

| Scenario | `--visual` value | Additional flags |
|---|---|---|
| AI explainer | `ai-video` | — |
| Avatar talking-head | `avatar,ai-video` | `--avatar <id>` |
| Clip remix + AI filler | `original-clip,ai-video` | `--file video-source:...` |
| Avatar + clips | `avatar,original-clip,ai-video` | `--avatar <id>` + `--file video-source:...` |
| MV from user's song | `ai-video` | `--file background-music:...` |
| AI-generated MV / music video | `ai-video` | `--music-video` |
| Synced video edit | `original-sync` | `--file video-audio:...` |
| Pure clips (no AI) | `original-clip` | `--file video-source:...` |
| Image animation | `image-video` | `--file original-image:...` |
| Image as style ref | `ai-video` | `--file reference-image:...` |

## Music Video / MV Mode

`--music-video` enables AI-generated music video / MV mode. It does **not** mean "add background music" to a normal video. Default: off.

- Use `--music-video` only when the user explicitly asks for an MV, music video, AI-generated song/music track, or a song-led video.
- Do **not** add `--music-video` just because a normal promo, explainer, product, or social video would benefit from background music.
- For ordinary background music, leave `--music-video` unset and describe the desired mood/style in the prompt if needed.
- If the user supplies a music file for MV creation, use `--file background-music:...` instead, and do **not** combine it with `--music-video`.

```bash
reela create "Create an AI-generated city-pop MV about a rainy neon street" --visual ai-video --music-video --duration 60
```

## Session & Collection Grouping

Videos created with the same `--session` name share a collection. The session-to-collection mapping is stored locally at `~/.config/reela/sessions.json`.

- Default session: `{hostname}-{username}-{YYYY-MM-DD}` (daily rotation)
