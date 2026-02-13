---
name: image
description: Generate images using DALL-E 3 via the dalle-generate script
user-invocable: true
disable-model-invocation: true
---

# /image — DALL-E 3 Image Generator

Generate images using the `dalle-generate` script.

## Usage

```
/image a golden lotus flower on cream background, minimalist style
```

## Steps

1. Take the user's description (everything after `/image`)
2. If no description provided, ask for one
3. Run the command: `~/bin/dalle-generate "description"`
4. Report the result to the user
5. The image will be saved to `~/Downloads/` and opened automatically

## Parameters

The script accepts optional parameters:
- **Size**: 1024x1024 (default), 1792x1024, 1024x1792
- **Quality**: standard (default), hd

To use custom size or quality, run manually:
```bash
dalle-generate "prompt" "1792x1024" "hd"
```

## Examples

```
/image a serene mountain landscape at sunset
/image minimalist bell notification icon, warm orange colors
/image open door with golden light, welcoming atmosphere
```

## Notes

- Requires `OPENAI_API_KEY` environment variable to be set
- Images are saved to `~/Downloads/generated_dalle_YYYYMMDD_HHMMSS.png`
- Cost: ~$0.04 per image (standard) or ~$0.08 (hd)
