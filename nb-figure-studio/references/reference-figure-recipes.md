# Figure Recipe Router

Read this when recreating any of the reusable figure families learned in this
toolkit: volcano plots, circular UMAPs, L-axis UMAPs, irregular-hull UMAPs, or
multi-track evidence wheels. These are implementation patterns, not substitutes
for the user's data.

## Figure-family router

| User asks for | Read | Structural unit |
|---|---|---|
| Top-journal sizing, spacing, type, line hierarchy, export review | [design-system.md](design-system.md) | Figure-level system |
| Differential-expression volcano | [Volcano plot](#volcano-plot) | Feature rows |
| Ring UMAP with metadata tracks | [Circular UMAP](#circular-umap) | Cell-type sectors + UMAP coordinates |
| L-shaped UMAP axes with direct labels | [L-axis UMAP](#l-axis-umap-with-scrnatoolvis) | UMAP coordinates + group metadata |
| Colored irregular dashed boundaries | [Hull UMAP](#irregular-hull-umap-with-ggunchull) | UMAP coordinates + group metadata |
| One gene per sector with many evidence tracks | [Evidence wheel](#multi-track-evidence-wheel) | Feature sectors + categorical/numeric tracks |

Use the shared [design-system.md](design-system.md) for typography, palette,
density hierarchy, panel consistency, and export. The chart-specific sections below
cover only decisions that change interpretation or implementation.

## Volcano plot

### Data contract

Require one row per feature and:

- stable feature ID or symbol;
- signed `log2FoldChange`;
- adjusted P/FDR, unless the user explicitly requests raw P.

Record the contrast direction before coloring anything. Do not infer it from the
sign distribution.

### Default pattern

```r
fdr_cutoff <- 0.05
lfc_cutoff <- 1

dat$direction <- ifelse(
  dat$padj < fdr_cutoff & dat$log2FC > lfc_cutoff,
  "Up",
  ifelse(
    dat$padj < fdr_cutoff & dat$log2FC < -lfc_cutoff,
    "Down",
    "Not significant"
  )
)

dat$neglog10_padj <- -log10(pmax(dat$padj, floor_p))
dat$capped <- dat$neglog10_padj > 30
dat$y_plot <- pmin(dat$neglog10_padj, 30)
```

Use:

- neutral gray for non-significant features;
- one blue and one orange accent for down/up;
- small points with enough transparency for dense regions;
- direct labels for a small, purposeful set of genes;
- threshold lines at `padj = FDR` and `|log2FC| = cutoff`;
- triangles at the Y cap when extreme P-values compress the informative range;
- an explicit caption stating any cap, threshold, contrast, and input file.

Do not tune thresholds to obtain a preferred gene count. Keep p=0 handling,
adjusted-P choice, label sets, and output dimensions in the manifest.

## Circular UMAP

## First identify what each sector means

Before choosing a package, write down the sector/position contract:

| Reference type | Sector | Position | Typical renderer |
|---|---|---|---|
| Genomic Circos ideogram | chromosome | genomic coordinate | RCircos |
| Feature-evidence wheel | one gene/sample/feature per equal-width sector | categorical or per-feature track value | circlize |
| Circular UMAP | cell-type sector | ordered cells within that type plus UMAP geometry inside the circle | plot1cell-style circlize |

Never convert a categorical evidence wheel into a chromosome ideogram merely
because both figures are circular. The interpretation changes completely.

## Circular UMAP

### Structural layers

1. UMAP coordinates rendered as dense colored points inside the circle.
2. A pale smooth contour around each cell-type cloud.
3. Equal-width cell-type sectors around the circle.
4. One or more narrow metadata tracks outside the sectors.
5. Cluster labels positioned inside or repelled within the cloud.

The ring is an annotation coordinate system. It is not a second UMAP axis.

### plot1cell pattern

The tested 2026-11 API pattern is:

```r
set.seed(1234)
circ_data <- plot1cell::prepare_circlize_data(seu, scale = 0.8)

se_cols <- colorRampPalette(
  RColorBrewer::brewer.pal(10, "Paired")
)(10)
cluster_cols <- se_cols[seq_along(levels(seu))]

plot1cell::plot_circlize(
  circ_data,
  do.label = TRUE,
  pt.size = 0.01,
  col.use = cluster_cols,
  bg.color = "white",
  kde2d.n = 200,
  repel = TRUE,
  label.cex = 0.6
)

plot1cell::add_track(
  circ_data,
  group = "condition",
  colors = se_cols,
  track_num = 2
)
plot1cell::add_track(
  circ_data,
  group = "dataset",
  colors = se_cols,
  track_num = 3
)
circos.clear()
```

Important corrections:

- parameter is `bg.color`, not `bg.col`;
- parameter is `kde2d.n`, not `k2d.n`;
- parameter is `track_num`, not `track.num`;
- retain `do.label = TRUE` and `repel = TRUE` when reproducing the reference;
- `repel = TRUE` uses `wordcloud::textplot()` in the tested source, so `wordcloud`
  must be available;
- `plot1cell` currently carries many optional Seurat/Bioconductor dependencies.
  Test the actual plotting functions instead of assuming a complete package install
  is lightweight.

### Density is data, not a style slider

Tested comparison:

- reference figure: dense real UMAP represented at a small final print size;
- exact reference parameters on a 2,262-cell public example: points almost
  disappeared;
- increasing opacity and marker size made the example visible but did not recreate
  the reference's cloud geometry.

Therefore:

- compare outputs at the same display size;
- record cell count and visible cluster count;
- do not infer the source cell count from density;
- do not duplicate or jitter points merely to imitate thickness;
- if fidelity requires the original point structure, ask for the Seurat object or
  UMAP-coordinate table.

For a dense source dataset, use the source's original point-size/opacity
parameters. For a smaller validation dataset, disclose any adaptive increase in
opacity or point size.

## Multi-track evidence wheel

Use this pattern for a wheel in which one gene/sample occupies one sector and each
concentric track represents a different evidence type.

Example evidence map:

1. outer bar track: count across tissues, colored by target group;
2. categorical track: approved/investigational drug evidence;
3. 3–14: binary hallmark matrix;
4. track 15: count of implicated cancer hallmarks.

Minimal circlize scaffold:

```r
circos.clear()
circos.par(
  start.degree = 90,
  gap.degree = 0.2,
  track.margin = c(0.002, 0.002),
  cell.padding = c(0, 0, 0, 0)
)
circos.initialize(factors = feature_ids, xlim = c(0, 1))

circos.track(
  factors = feature_ids,
  y = tissue_count,
  ylim = c(0, max(tissue_count)),
  track.height = 0.1,
  panel.fun = function(x, y) {
    id <- CELL_META$sector.index
    row <- match(id, feature_ids)
    circos.rect(
      0.08, 0, 0.92, tissue_count[row],
      col = group_colors[group[row]], border = NA
    )
    circos.text(
      CELL_META$xcenter,
      CELL_META$cell.ylim[2] + mm_y(2),
      id,
      facing = "clockwise",
      niceFacing = TRUE,
      adj = c(0, 0.5)
    )
  }
)

# Add one track per evidence category, keeping genes in identical order.
```

Operational requirements:

- every track must use the same feature order and sector factors;
- binary presence/absence should be explicit, not encoded by missing rectangles;
- count bars start at zero;
- legends must state what each track and color mean;
- do not use `RCircos` for this categorical feature wheel unless the positions
  truly represent genomic coordinates.

## L-axis UMAP with scRNAtoolVis

Tested argument mapping:

| Intent | Current argument |
|---|---|
| grouping column | `clusterCol` |
| point size | `pSize` |
| corner-label color | `lineTextcol` |
| corner text size | `cornerTextSize` |
| hull transparency | `cicAlpha` |
| hull extension | `cicDelta` |
| direct cluster labels | `cellLabel`, `cellLabelSize` |
| hull line color/width/type | `cicLineColor`, `cicLineSize`, `cicLineLty` |

`cicDelta` must be supplied when `addCircle = TRUE`.

## Irregular-hull UMAP with ggunchull

- current repository tested: `sajuukLyu/ggunchull`;
- current layer: `stat_unchull()`;
- prefer `linewidth` and `linetype` with modern ggplot2;
- extract Seurat embeddings explicitly and rename the first two columns to the
  expected `umap_1`, `umap_2` names;
- load `ggrepel` before using `geom_text_repel()`.

## API and source validation

Reference videos and AI summaries frequently mix versions. Before using a snippet:

1. verify the package/repository still exists;
2. inspect `packageVersion()` and `args(function_name)`;
3. test on a small real object or a clearly labelled template;
4. record which behavior is code fidelity and which is data-driven fidelity;
5. preserve original code/data provenance and disclose every simulated field.

Tested 2026-11-17 environment: R 4.3.3, Seurat 5.2.1, circlize 0.4.16,
ggunchull 1.0.1, current plot1cell source, current scRNAtoolVis source.
