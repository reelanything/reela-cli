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
| AI background music | `ai-video` | `--auto-music` |
| Synced video edit | `original-sync` | `--file video-audio:...` |
| Pure clips (no AI) | `original-clip` | `--file video-source:...` |
| Image animation | `image-video` | `--file original-image:...` |
| Image as style ref | `ai-video` | `--file reference-image:...` |

## Auto Music

`--auto-music` enables AI-generated background music for the video. When set, the platform automatically selects and generates music that fits the video content. Default: off.

- Use `--auto-music` when no user-supplied music track is provided and background music is desired.
- If the user attaches `--file background-music:...`, do **not** combine with `--auto-music` — user-supplied music takes precedence.

```bash
reela create "Product launch highlight reel" --visual ai-video --auto-music --duration 60
```

## Session & Collection Grouping

Videos created with the same `--session` name share a collection. The session-to-collection mapping is stored locally at `~/.config/reela/sessions.json`.

- Default session: `{hostname}-{username}-{YYYY-MM-DD}` (daily rotation)
