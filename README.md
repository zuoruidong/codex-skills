# Codex Skills

Public collection of reusable Codex skill packages.

## Included skills

### `NB-figure-studio`

A unified scientific-figure workflow for:

- creating data plots, multi-panel figures, vector schematics, graphical
  abstracts, and publication artwork;
- reading and interpreting paper figures;
- auditing scientific integrity, visual hierarchy, accessibility, and export
  quality;
- revising figures from source code, editable artwork, or raster images;
- imitating a reference figure's visual system without copying its evidence;
- running a complete make → audit → revise → deliver loop.

## Installation

Clone the repository:

```bash
git clone https://github.com/zuoruidong/codex-skills.git
```

Copy or move the skill into your Codex skills directory:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R codex-skills/nb-figure-studio \
  "${CODEX_HOME:-$HOME/.codex}/skills/"
```

Restart or refresh Codex if the new skill does not appear immediately.

## Usage

Invoke the skill explicitly when you want the full workflow:

```text
Use $nb-figure-studio to create a publication-ready multi-panel figure
from my data, then audit and revise it at final physical size.
```

It is also designed for focused requests:

```text
Use $nb-figure-studio to audit this figure and rank fixes by severity.
Use $nb-figure-studio to revise this plot without changing any values.
Use $nb-figure-studio to imitate the composition and visual grammar of
these reference figures with my own data.
```

## Principles

The skill protects source data, raw images, uncertainty, transformations, and
statistical meaning. Reference-style adaptation transfers reusable design
conventions, not the source's claims, measurements, or protected assets.

Journal rules change over time. When the exact venue and submission phase are
known, verify the current official author instructions before calling a figure
submission-compliant.
