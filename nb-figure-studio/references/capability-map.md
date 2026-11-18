# Current Figure Capability Map

Use existing specialist skills when they are installed and their data contract
matches. The studio owns routing, continuity, and the final review; it does not
pretend that every specialist script ran.

Resolve the skills root from `CODEX_HOME` when set, otherwise use the user's
standard Codex skills directory. Do not expose private local paths or filenames in
the final figure, caption, or user-facing report unless the user asks for an audit
trail.

## Core routing

| Need | Source skill | Use |
|---|---|---|
| Python/R manuscript plotting, multi-panel alignment, PDF collision audit, vector schematic audit | `nature-figure` | Primary scientific plotting and rendered QA engine |
| Matplotlib/Seaborn/Plotly truthfulness, palette, missing data, export provenance | `scientific-visualization` | Design and validation standards |
| Coherent publication style, review checklist, AI revision prompt | `publication-figure-style` | Style system and revision checklist |
| Read paper figures panel by panel | `scientific-figure-reader` | Evidence labels, figure-family checks, interpretation |
| Differential-expression volcano | Internal [reference-figure-recipes.md](reference-figure-recipes.md#volcano-plot) | Validate the DE table contract, thresholds, labels, and display cap |
| Circular/L-axis/hull UMAP, multi-track evidence wheel | Internal [reference-figure-recipes.md](reference-figure-recipes.md#figure-family-router) | Choose the structural recipe before coding |
| Open-ended figure style selection | Internal [variant-gallery.md](variant-gallery.md) | Render 2–4 data-invariant variants and let the user choose |
| Script/template/adaptation provenance, statistical report, QA boundaries | Internal [asset-routing-and-reproducibility.md](asset-routing-and-reproducibility.md) | Record semantic matching, adaptation level, reproducibility, and checks |
| DE diagnostic plots | `de-visualization` | MA, volcano, PCA, distance heatmap, dispersion |
| Enrichment plots | `enrichment-visualization` | GO/KEGG/GSEA redundancy and plot choice |
| AI raster image generation/editing | `imagegen` | Illustrations, graphical abstracts, targeted raster edits |
| Academic illustration generation framework | `paper-banana` | Only when installed/configured and explicitly appropriate |
| Hand-built editable diagrams | `drawio` or `nature-figure` vector route | Architecture, pipeline, mechanism, workflow |
| Slide/graphic design | `visualize` | Only for web/interactive explanatory visuals, not manuscript data plots |

## Common command routes

Adjust the script path to the installed skills root. Prefer the source skill's own
instructions over copying snippets from memory.

### Nature Figure

Before plotting, read its `SKILL.md`, `manifest.yaml`, and always-load core files.
Use only the selected backend's fragment.

Common QA:

```bash
python <skills-root>/nature-figure/scripts/validate_figure.py figure.py
python <skills-root>/nature-figure/scripts/audit_pdf_text.py figure.pdf --min-pt 5
python <skills-root>/nature-figure/scripts/audit_figure_collisions.py figure.pdf \
  --json-out figure.collision-audit.json \
  --overlay-pdf figure.collision-audit.pdf
python <skills-root>/nature-figure/scripts/audit_svg_schematic.py figure.svg
```

For a multi-panel figure, also run the backend's panel-alignment measurement and
the matching JSON auditor as described by `nature-figure`. Do not claim alignment
passed from a visual glance.

### Scientific Visualization

Use its metadata, palette, export-plan, and style-preview helpers when useful.
The strongest non-duplicated contribution is its explicit treatment of missing
data, missing observations, transformation guards, static/interactive distinction,
and provenance-rich export.

### Scientific Figure Reader

For PDF papers, use its preparation helper when available, then visually inspect
the rendered pages and ambiguous crops. OCR or extracted text is not a substitute
for viewing marks, layout, color, overlap, and image evidence.

### Internal Figure Recipes

Read the matching section of
[reference-figure-recipes.md](reference-figure-recipes.md) before implementing one
of these chart families:

- volcano plot;
- circular UMAP;
- L-axis UMAP;
- irregular dashed-hull UMAP;
- multi-track evidence wheel.

Use the supplied/derived data contract for that exact family. Do not route a
categorical evidence wheel to a genomic-coordinate renderer, or treat a sparse
demo dataset as proof that a dense reference style cannot be reproduced.

## Fallbacks

If a source skill is unavailable:

- continue with the studio's shared contract, design system, and QA rubric;
- do not claim its specialized audit ran;
- do not fabricate missing scripts or output;
- adapt the source code in the task workspace, preserving provenance;
- for a high-risk final figure, report the unavailable specialist as a remaining
  validation gap.

If a source skill's instructions conflict with this entrypoint, preserve the
specialist's stricter scientific or technical rule for its own tool/script, and
surface the conflict to the user.

## Scope boundaries

- Use code for quantitative plots and exact text/statistics.
- Use vector editing for deterministic diagrams.
- Use raster generation for illustration, not data fidelity.
- Use the reader for interpretation, not to reverse-engineer hidden data.
- Use style references for design patterns, not as evidence for new claims.
