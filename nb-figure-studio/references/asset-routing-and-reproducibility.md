# Asset Routing and Reproducibility

Use this before adapting a plotting script, template, figure recipe, or reference
figure. It turns “borrowed a style” into a traceable implementation.

## 1. Figure contract and evidence chain

For each panel record:

```text
Panel:
Scientific question:
Unique evidence contributed:
Required visual comparison:
Data source:
Transformation:
Uncertainty / n:
Statistics:
Figure family:
```

Drop a panel when it repeats the same evidence without a distinct inferential
role. More panels are not inherently more rigorous.

## 2. Semantic-match gate

Compare what the source really encodes with what the new figure must encode before
mapping columns.

Record:

| Source semantic | New-data semantic | Compatible? | Action |
|---|---|---|---|
| chromosome interval | gene-level categorical evidence | no | build a feature wheel, not a chromosome ideogram |
| UMAP coordinates | UMAP coordinates | yes | style/layout adaptation allowed |
| paired X/Y observations | wide multivariate table | depends | require explicit column mapping |

Reject column mapping when the chart family or data dimensions differ. Column
renaming cannot turn a genomic ideogram into a categorical evidence matrix.

## 3. Adaptation levels

Use one of these labels:

- **Native recipe:** executes a validated implementation with the user's data.
- **Data adapt:** same figure family and semantic contract; only input mapping,
  names, scales, and guards change.
- **Parameter inherit:** borrow typography, line, marker, and spacing rules but
  draw a different chart family.
- **New build:** no sufficiently compatible recipe exists.

Every panel in the final report should state its adaptation level.

## 4. Protect against template leakage

Before execution, inspect the adapted source for:

- built-in random or simulated data;
- rows silently filtered or truncated;
- demo group names left in labels;
- hard-coded significance thresholds or factor levels;
- demo summary annotations/statistics;
- output paths that overwrite source data;
- seed changes that alter the user's analysis rather than layout only.

If a script embeds simulated data, replace the entire data entry section, not just
a file path. A figure is not traceable merely because the text “replace with real
data” appears in a comment.

## 5. Environment and output preflight

Before rendering:

1. Detect Python and R.
2. Check required packages and versions.
3. Identify whether each panel can output true vector content.
4. Decide whether a mixed Python/R figure is necessary.
5. State any fallback before using it.

Do not silently replace a requested backend or claim a vector master when a panel
was loaded as a flattened PNG.

## 6. Executable QA, kept subordinate to scientific review

Useful automated checks:

- figure dimensions and aspect ratio;
- font family and minimum rendered size;
- target 300 dpi or greater for raster components;
- PDF/SVG font embedding;
- existence of vector master and raster preview;
- clipping and text/stroke collision;
- multi-panel alignment;
- unresolved placeholder text.

Automated checks are screening tools. Do not let a zero-failure report override a
visible scientific flaw or a legitimate but visually “awkward” result.

Use warnings rather than fabricated gates for:

- very few significant features;
- weak correlation;
- low between-group separation;
- small or imbalanced groups;
- absent apparent structure.

These can be real scientific results. Explain the readability risk; do not refuse
to render solely because the plot is not visually impressive.

## 7. Statistics and reproducibility report

For every quantitative panel report:

- `n` and the unit of replication;
- inclusion/exclusion rules;
- aggregation and center statistic;
- spread/interval and its definition;
- statistical test and multiplicity correction;
- transformations and handling of missing/zero values;
- random seeds where stochastic methods affect the result;
- source file/columns and output file;
- for models: train/validation/test split, folds/seeds, metric, and baseline.

The report should be generated from the actual inputs or code, not reconstructed
from the final image.

## 8. Reviewer simulation

When the user asks whether a figure will survive review, review through:

1. scientific clarity: is the claim visible and correctly supported;
2. evidence logic: does every panel contribute something unique;
3. visual hierarchy: does the intended comparison dominate;
4. print/accessibility: are type, color, scale, and redundancy adequate;
5. completeness: are `n`, statistics, labels, source, and export documented.

Return `must-fix` and `suggestion` items with concrete remedies. Do not present a
generic checklist as a review of the specific figure.

## 9. Final delivery record

Keep:

- figure contract and panel evidence map;
- variant selection, when applicable;
- adaptation level and source recipe;
- editable source;
- vector master and raster preview;
- statistical/reproducibility report;
- QA findings and unresolved risks;
- target-journal rules checked, with date/phase when known.

