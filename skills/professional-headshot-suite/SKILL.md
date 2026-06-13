---
name: professional-headshot-suite
description: Generate a nine-image professional headshot suite from 2-3 identity reference photos, using a local codex-gpt-image skill as the image generation backend and saving polished executive, editorial, LinkedIn, CEO, cinematic, high-fashion, and dramatic portrait outputs to Documents. Use when the user asks for a full professional headshot set from reference images through Codex OAuth instead of a separate OpenAI API key.
---

# Professional Headshot Suite

Create a 9-look professional headshot package from 2-3 identity reference images of the same person. Use a local `codex-gpt-image` skill as the image-generation source and save outputs under `~/Documents` by default when generation is explicitly requested.

## Required Inputs

- 2-3 clear identity reference images of the same person.
- Preferred default location for the person's photos: `assets/person-reference-images/` inside this skill folder.
- Absolute local paths can also be passed with repeated `--image` flags.
- Prefer one close face image, one upper-body image, and one alternate angle.
- Do not proceed with unrelated people, heavily filtered references, or screenshots where the face is too small unless the user explicitly accepts the identity risk.

## Visual Style References

Use `assets/reference-images/` only as an optional text-free visual style board. Do not pass visual style images as identity `--image` inputs unless the user explicitly asks for style-reference image conditioning and accepts the identity-contamination risk. The runner defaults to `assets/person-reference-images/` for subject photos.

## Core Workflow

1. Check Codex image auth:

   ```bash
   python3 ~/.agents/skills/codex-gpt-image/scripts/codex_gpt_image.py auth-status
   ```

2. If auth is missing, use the login flow from `$codex-gpt-image`; never print tokens.

3. If the user has placed the person's photos in `assets/person-reference-images/`, generate without image flags:

   ```bash
   python3 ~/.agents/skills/professional-headshot-suite/scripts/generate_headshot_suite.py
   ```

4. Or generate with absolute image paths:

   ```bash
   python3 ~/.agents/skills/professional-headshot-suite/scripts/generate_headshot_suite.py \
     --image /absolute/path/ref-face.jpg \
     --image /absolute/path/ref-body.jpg \
     --image /absolute/path/ref-angle.jpg
   ```

5. If the user asks to preview commands without spending image generations, add `--dry-run`.

6. Report the output directory, generated filenames, model, size, and any failed looks.

## Output Contract

The runner creates a timestamped directory in `~/Documents`, unless `--out-dir` is provided:

```text
~/Documents/headshot-suite-YYYYMMDD-HHMMSS/
|-- 01-editorial-headshot.png
|-- 02-cinematic-headshot.png
|-- ...
|-- 09-dramatic-headshot.png
|-- prompts/
|   |-- 01-editorial-headshot.prompt.txt
|   `-- ...
`-- manifest.json
```

## Prompt Source

Use `references/headshot_prompt_pack.md` for the 9 looks.

Identity rules:

- Treat the reference images as the source of truth.
- Preserve face shape, eye shape, nose, lips, jaw, skin tone, age, body proportions, and hairstyle unless the user explicitly requests a change.
- Grooming cleanup is allowed only for professional polish: reduced oiliness, realistic matte skin, natural pores, neat facial hair where present or requested.
- Do not add text, logos, watermarks, fake muscles, cartoon style, or visible AI artifacts.

## Quality Pass

After generation:

- Confirm all 9 PNGs exist and are non-empty.
- Open or inspect representative files before presenting results when possible.
- Regenerate only the failed or visibly weak look; do not rerun the full suite unless needed.
- If identity drift appears, strengthen the next prompt with: "The reference identity is mandatory; do not beautify, age-shift, change facial geometry, or blend with a model face."

## Common Commands

Dry run using in-skill reference images:

```bash
python3 ~/.agents/skills/professional-headshot-suite/scripts/generate_headshot_suite.py --dry-run
```

Dry run using explicit references:

```bash
python3 ~/.agents/skills/professional-headshot-suite/scripts/generate_headshot_suite.py \
  --image /absolute/path/ref1.jpg \
  --image /absolute/path/ref2.jpg \
  --dry-run
```

Custom output folder:

```bash
python3 ~/.agents/skills/professional-headshot-suite/scripts/generate_headshot_suite.py \
  --image /absolute/path/ref1.jpg \
  --image /absolute/path/ref2.jpg \
  --out-dir ~/Documents/founder-headshots
```
