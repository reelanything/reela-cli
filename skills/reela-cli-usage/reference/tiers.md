# Reela Quality Tiers

Tiers control video quality, rendering speed, and credit cost. Higher tiers produce better visuals but cost more credits and take longer.

## Available Tiers

| Tier  | Quality      | Speed     | Credits/min | Best For           |
| ----- | ------------ | --------- | ----------- | ------------------ |
| photo | Basic stills | Fast      | 1           | Quick previews     |
| lite  | Medium-Low   | Fast      | 3           | Quick iterations   |
| pro   | High         | Moderate  | 8           | Production content |
| max   | Very High    | Slow      | 12          | Premium content    |
| ultra | Ultra        | Very Slow | 24          | Cinema quality     |

## Recommendations

- **Testing/Drafts**: Use `photo` or `lite` (save credits during iteration)
- **Standard production**: Use `pro` (best quality/cost balance)
- **Premium output**: Use `max` or `ultra`
- **Always use `--dry-run` first** to check credit cost before committing
