# Style Imitation and Asset Reuse

Use this reference for 仿图, “像这张图”, reference-style redraw, template reuse, and
image-to-image adaptation of scientific figures.

## Principle

Imitate the reusable visual system, not the source claim. A reference provides
evidence about design decisions; it does not provide the new figure's data,
statistics, component relationships, or publication rights.

State the adaptation level before implementation:

| Level | What transfers | When to use |
|---|---|---|
| **Style transfer** | Palette, typography, line/marker system, spacing, annotation tone | Same scientific meaning, different plot family or data |
| **Composition transfer** | Panel count, hierarchy, hero/subordinate rhythm, shared-legend logic | New data with a similar argument structure |
| **Structural recreation** | Plot families, panel roles, axes, grouping, and encodings | Data contract and claim structure genuinely match |
| **Exact redraw** | The full visual organization | User owns or may adapt the source and supplies the necessary data/assets |

Pixel-level copying is not the default. If exact redraw is requested, inspect
licensing and attribution, and do not reproduce third-party logos, photographs,
micrographs, or text without permission.

## Build a style DNA

Inspect the reference at full figure and panel scale. Record only observable
features:

```text
Canvas and aspect:
Panel count and hierarchy:
Plot families:
Whitespace and gutters:
Typography and hierarchy:
Palette and semantic color use:
Line weights and marker grammar:
Legend strategy:
Direct-label and annotation style:
Image/plate treatment:
Background and frame treatment:
Visual rhythm:
Apparent venue/style family:
```

Use relative descriptions when exact values cannot be measured. For example:
“three times more whitespace between evidence blocks than within a panel” is
safer than inventing a millimetre value.

## Separate transferable and non-transferable content

Transferable by default:

- final-size proportion and panel rhythm;
- typography hierarchy;
- neutral-plus-accent palette logic;
- line/marker hierarchy;
- direct-label and legend strategy;
- amount of decorative ink;
- treatment of uncertainty and annotations.

Not transferable without explicit source/rights:

- reported values, sample sizes, significance marks, or conclusions;
- microscopy, blots, photographs, clinical images, or maps;
- unique illustrations, logos, icons, institutional marks, and watermarks;
- exact long text, captions, or original source layout files;
- mechanisms, components, or arrows not supported by the user's material.

## Check compatibility

Before reusing a template or composition:

1. Compare the source plot family with the requested plot family.
2. Map every field: template role → user field → units → allowed values.
3. Compare grouping, replicate unit, uncertainty, transformations, and missing-data
   behavior.
4. Reject structural reuse when the scientific logic differs.
5. Use style-only inheritance when only the visual language is reusable.
6. Build anew when the source would require changing the statistical logic or
   inventing structure.

Do not force a different chart family into the reference's shape merely to match
the picture.

### Resolve structural ambiguity before copying

A familiar plot name can hide incompatible data contracts. In particular:

- A genomic Circos ideogram uses chromosomes as sectors and genomic coordinates
  as positions.
- A feature-evidence wheel can use one gene or sample per equal-width sector;
  radial tracks then represent categorical evidence rather than genomic location.

These figures may look related and even use the same package family, but their
sector semantics, ordering, and interpretation are different. Identify the unit
represented by each sector before choosing `RCircos`, `circlize`, or another
renderer. Do not convert a categorical multi-track wheel into a chromosome plot
merely because both are circular.

### Treat density as evidence-bearing

Dense UMAP, t-SNE, and scatter clouds depend on the number and distribution of
observations. Point size and opacity can improve legibility, but raising them
cannot reconstruct a reference's density from a much smaller demo dataset.

For reference-style UMAP work:

1. compare the reference and candidate at the same display size;
2. record cell count, visible cluster count, cluster area, and apparent density;
3. preserve the supplied point coordinates and grouping;
4. state when a public demo or simulated point cloud is standing in for the
   original data;
5. judge code fidelity separately from data-driven fidelity.

## Workflow

1. Classify each reference image: style reference, structural reference, or source
   asset to edit.
2. Write the style DNA and adaptation level.
3. State which elements will transfer and which will be replaced.
4. Build the new figure from the user's data/brief using the shared design system.
5. Compare side by side at the same display size.
6. Adjust the design system, not the evidence.
7. Audit the new figure independently; do not inherit trust from the reference.
8. Return the mapping and note whether similarity is aesthetic, structural, or a
   licensed reconstruction.

## Image-to-image adaptation

Use `imagegen` when the desired artifact is raster and the user explicitly wants
an illustration or image edit.

Prompt structure:

```text
Use case: scientific-educational | infographic-diagram | style-transfer
Input images: Image 1 = style/composition reference; Image 2 = edit target
Scientific message: <exact supported message>
Transfer: <palette, hierarchy, spacing, mark style>
Replace: <all source-specific content>
Preserve: <target geometry, data evidence, text invariants>
Constraints: no invented data, statistics, components, labels, or mechanisms;
no logos, watermarks, or copied source text
Output: <medium and use>
```

For edits, repeat the invariants every iteration. For figure data, raster generation
is not a reliable renderer of exact axes, numbers, or statistical annotations; use
code for quantitative plots.

## Fidelity review

Check:

- same visual rhythm at final size;
- consistent typography and line hierarchy;
- palette semantics transferred rather than copied blindly;
- no source-specific evidence survived accidentally;
- no unsupported component or arrow was introduced;
- labels and numbers were regenerated from the user's material;
- the new figure remains legible and honest when the reference is hidden.

Return the style DNA, transfer/exclusion map, touched files, and any fidelity gaps.
