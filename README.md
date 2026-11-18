# Paper Figure Skills

A public collection of reusable paper-figure skills, plotting recipes, review
rules, and revision workflows for Codex.

## 关于这个项目

这个公开库由 [@zuoruidong](https://github.com/zuoruidong) 维护。作者会持续把平时看到的高质量科研图、好用的绘图代码、审图经验和翻修技巧整理进
`NB-figure-studio`，让它不只是一个静态模板，而是一套会不断学习和更新的科研绘图 skill。

当前版本：**v1.2**。后续每次加入值得复用的新技巧，都会更新版本、验证技能并同步到这里。

## Included skills

### `NB-figure-studio`

**Version:** 1.2

A unified scientific-figure workflow for:

- creating data plots, multi-panel figures, vector schematics, graphical
  abstracts, and publication artwork;
- reading and interpreting paper figures;
- auditing scientific integrity, visual hierarchy, accessibility, and export
  quality;
- revising figures from source code, editable artwork, or raster images;
- imitating a reference figure's visual system without copying its evidence;
- adapting the validated R recipe router for volcano plots, three UMAP
  presentation modes, and multi-track evidence wheels while preserving data
  semantics;
- generating labelled multi-variant previews from the same data so the user can
  choose the final visual direction;
- tracking template provenance and adaptation level, with a mandatory
  statistics/reproducibility report for quantitative panels;
- running a complete make → audit → revise → deliver loop.

New reusable plotting techniques and review lessons are integrated into the
relevant reference file, validated, versioned, and pushed to this public
repository so the installed skill and GitHub copy stay in sync.

## Installation

Clone the repository:

```bash
git clone https://github.com/zuoruidong/paper-figure-skills.git
```

Copy or move the skill into your Codex skills directory:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R paper-figure-skills/nb-figure-studio \
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
Use $nb-figure-studio to recreate this circular UMAP in R, then compare structural
and data-driven fidelity separately.
Use $nb-figure-studio to generate three UMAP styles from the same Seurat object,
show them side by side, and let me choose before exporting the final PDF.
```

## Principles

The skill protects source data, raw images, uncertainty, transformations, and
statistical meaning. Reference-style adaptation transfers reusable design
conventions, not the source's claims, measurements, or protected assets.

Journal rules change over time. When the exact venue and submission phase are
known, verify the current official author instructions before calling a figure
submission-compliant.
