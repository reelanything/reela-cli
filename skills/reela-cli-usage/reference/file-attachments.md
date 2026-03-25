# File Attachments

Attach your own media (images, videos, music) as source material for video creation using the `--file` flag.

## Syntax

`reela create "prompt" --file ROLE:PATH [--file ROLE:PATH ...]`

## Roles

| Role              | Description                               | Formats        |
| ----------------- | ----------------------------------------- | -------------- |
| `video-source`    | Video clip (visual only, audio muted)     | mp4, mov       |
| `video-audio`     | Video (preserve audio-visual sync)        | mp4, mov       |
| `reference-image` | Reference image (style/composition guide) | jpg, png, webp |
| `original-image`  | Source image (for image-to-video)         | jpg, png, webp |
| `background-music` | Background music track                   | mp3, wav       |

## Examples

Image to video: `reela create "Animate this photo" --visual image-video --file original-image:./photo.jpg`
With reference: `reela create "Video in this style" --visual ai-video --file reference-image:./style.png`
With music: `reela create "Product demo" --visual avatar --file background-music:./bgm.mp3`
Multiple files: `reela create "Edit this" --visual original-clip --file video-source:./clip1.mp4 --file video-source:./clip2.mp4`
