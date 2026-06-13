<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=2,3&height=210&text=Professional%20Headshot%20Suite&fontSize=42&fontAlignY=35&desc=Turn%202-3%20reference%20photos%20into%20a%20complete%20executive%20portrait%20set&descAlignY=56&fontColor=ffffff" width="100%" />

<!-- readme-gen:start:badges -->
[![Skills](https://img.shields.io/badge/skills.sh-ready-111827?style=flat-square)](https://skills.sh)
[![Skill](https://img.shields.io/badge/Codex%20Skill-professional--headshot--suite-2563eb?style=flat-square)](./skills/professional-headshot-suite/SKILL.md)
[![Python](https://img.shields.io/badge/Python-3.11%2B-3776ab?style=flat-square&logo=python&logoColor=white)](./skills/professional-headshot-suite/scripts/generate_headshot_suite.py)
[![License](https://img.shields.io/github/license/Sheshiyer/professional-headshot-suite?style=flat-square)](./LICENSE)
<!-- readme-gen:end:badges -->

</div>

**Professional Headshot Suite** is a Codex skill that turns 2-3 identity reference photos into a complete nine-look portrait package: editorial, cinematic, high-fashion, chiaroscuro, warm-light, turtleneck, authority, CEO, and dramatic. It wraps a local `codex-gpt-image` backend so agents can run one consistent, source-backed portrait workflow instead of rebuilding prompts every time.

<img src="https://capsule-render.vercel.app/api?type=rect&color=gradient&customColorList=2,3&height=1" width="100%" />

## Highlights

<table>
<tr>
<td width="50%" valign="top">

### Nine Looks, One Command

Generate a full professional suite with consistent filenames, saved prompts, and a manifest for auditability.

</td>
<td width="50%" valign="top">

### Identity-First Prompting

Every prompt anchors on preserving face shape, skin tone, proportions, age, and natural facial structure.

</td>
</tr>
<tr>
<td width="50%" valign="top">

### Private Inputs Stay Local Until Run

The repository ships placeholders only. User reference photos are intentionally ignored by Git.

</td>
<td width="50%" valign="top">

### Codex OAuth Backend

Designed to pair with a local `codex-gpt-image` skill using Codex/ChatGPT subscription authentication.

</td>
</tr>
</table>

## Install

Clone the repo and copy the skill into your agent skills directory:

```bash
git clone https://github.com/Sheshiyer/professional-headshot-suite.git
mkdir -p ~/.agents/skills
cp -R professional-headshot-suite/skills/professional-headshot-suite ~/.agents/skills/
```

This skill expects the companion `codex-gpt-image` skill to exist at:

```text
~/.agents/skills/codex-gpt-image/scripts/codex_gpt_image.py
```

## Usage

Place 2-3 identity reference images here:

```text
~/.agents/skills/professional-headshot-suite/assets/person-reference-images/
```

Then run:

```bash
python3 ~/.agents/skills/professional-headshot-suite/scripts/generate_headshot_suite.py
```

Or pass explicit images:

```bash
python3 ~/.agents/skills/professional-headshot-suite/scripts/generate_headshot_suite.py \
  --image /absolute/path/face.png \
  --image /absolute/path/upper-body.png \
  --image /absolute/path/full-body.png
```

Preview the exact generation commands without spending image calls:

```bash
python3 ~/.agents/skills/professional-headshot-suite/scripts/generate_headshot_suite.py --dry-run
```

## Output

```text
~/Documents/headshot-suite-YYYYMMDD-HHMMSS/
|-- 01-editorial-headshot.png
|-- 02-cinematic-headshot.png
|-- 03-high-fashion-headshot.png
|-- 04-chiaroscuro-headshot.png
|-- 05-warm-light-headshot.png
|-- 06-turtleneck-headshot.png
|-- 07-authority-headshot.png
|-- 08-ceo-headshot.png
|-- 09-dramatic-headshot.png
|-- prompts/
`-- manifest.json
```

## Repository Structure

<!-- readme-gen:start:tree -->
```text
professional-headshot-suite/
|-- README.md
|-- LICENSE
`-- skills/
    `-- professional-headshot-suite/
        |-- SKILL.md
        |-- agents/openai.yaml
        |-- scripts/generate_headshot_suite.py
        |-- references/headshot_prompt_pack.md
        `-- assets/
            |-- person-reference-images/.gitkeep
            `-- reference-images/.gitkeep
```
<!-- readme-gen:end:tree -->

## Safety Notes

- Do not commit personal identity photos.
- Do not pass style-board screenshots as identity references.
- Running generation sends selected reference images and prompts to the configured image backend.
- Review outputs for identity drift before using them professionally.

## Skill Indexing

This repo is arranged for skill indexers that scan repository skill folders:

```text
skills/professional-headshot-suite/SKILL.md
```

The skill name in frontmatter is:

```yaml
name: professional-headshot-suite
```

## Project Health

<!-- readme-gen:start:health -->
| Category | Status | Score |
|:--|:--:|--:|
| Skill Metadata | complete | 100% |
| Script Syntax | verified | 100% |
| Docs | README + SKILL.md | 90% |
| Privacy Hygiene | ignored personal refs | 100% |
<!-- readme-gen:end:health -->

## License

MIT. See [LICENSE](./LICENSE).

<!-- readme-gen:start:footer -->
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=2,3&height=100&section=footer" width="100%" />

Built for repeatable professional portrait generation with Codex skills.

</div>
<!-- readme-gen:end:footer -->
