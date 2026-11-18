# Figure Variant Gallery

Use this when a user asks for a new data figure without fixing the visual
direction. The goal is to make style a visible choice instead of silently
deciding for the user.

## When to produce variants

Produce 2–4 variants when:

- the request is “make a UMAP / volcano / PCA / heatmap” without a named style;
- the user asks to “show me options”, “看几个画风”, or “先做几个方案”;
- several layouts are scientifically equivalent but serve different reading
  needs;
- the user wants to imitate a reference but has not chosen how strongly to
  transfer its composition.

Skip the gallery when:

- the user specifies the exact layout, style, or template;
- the task is a small cosmetic fix;
- the medium or time constraint makes multiple renders impractical;
- extra variants would require changing the data, statistical meaning, or claim.

When skipping, state why and proceed with the explicitly requested direction.

## Invariants

Every variant must use the same:

- input dataset, exclusions, and transformations;
- statistical thresholds, tests, uncertainty, and `n`;
- group order and color semantics for the same group;
- axis variables, units, and meaningful limits;
- label set that carries scientific meaning;
- final physical size or a directly comparable preview size;
- panel count unless the user explicitly asks to compare compositions.

Variants may differ only in visual organization and encoding that preserve the
same evidence, for example:

- axis treatment;
- label placement and legend strategy;
- density contour or hull treatment;
- circular versus rectangular layout;
- annotation hierarchy;
- whitespace and panel rhythm;
- palette, as long as group semantics stay stable.

Do not treat removing evidence, changing thresholds, duplicating points, or
changing cluster labels as “another style”.

## Default variant counts

- General quantitative figure: 3 variants.
- Expensive or very dense figure: 2 variants initially.
- UMAP/PCA/t-SNE: 3 variants by default; add a fourth circular/metadata-track
  option when the circular form is relevant.
- Multi-panel manuscript figure: 2 complete compositions; do not create a new
  analysis for each.

## UMAP gallery

For the same embeddings, groups, and label set, useful variants are:

| ID | Direction | Best for | Tradeoff |
|---|---|---|---|
| V1 | Minimal UMAP with direct cluster labels | Fast reading, manuscript main panel | Less room for sample metadata |
| V2 | L-axis UMAP with grey dashed hulls | Clean talk/paper visual, emphasizes cluster boundaries | Axis values are less prominent |
| V3 | Colored irregular-hull UMAP | Group boundaries and identity are important | More visual ink; hull can imply a sharper boundary than the data support |
| V4 | Circular UMAP with metadata tracks | Dense atlas overview and sample/dataset annotation | Needs high point density; labels and fine axes become harder to read |

Render V4 only when the dataset has enough points and metadata to justify the
outer tracks. A sparse dataset should not be made to look dense by duplicating or
jittering points.

## Volcano gallery

Keep identical thresholds and genes across variants:

| ID | Direction | Best for |
|---|---|---|
| V1 | Minimal neutral/blue/orange volcano | Main manuscript panel |
| V2 | Direct-label emphasis | Story around selected genes |
| V3 | Density-aware display for very large tables | Preserving structure without a saturated point cloud |

If Y values are capped, use the same cap and triangle convention in every variant.

## Other figure families

Use these generic style axes:

| Figure | Variant axis |
|---|---|
| PCA / t-SNE | minimal score plot; annotated ellipse plot; density/hull plot |
| Heatmap | minimal clustered; annotation-rich; split/comparative layout |
| Bar / box / violin | compact main-panel; individual-point overlay; reference-style annotation |
| Line / trend | minimal direct-series labels; uncertainty-forward; small-multiples |
| ROC / PR | compact performance panel; annotated thresholds/operating point; faceted comparisons |
| Enrichment | dotplot; bar/size-encoding; network/tree redundancy view |
| Circos evidence wheel | outer-count emphasis; evidence-matrix emphasis; grouped-comparison emphasis |

Rename these variants to match the actual scientific role rather than using
generic labels such as “pretty” or “advanced”.

## Variant production protocol

1. Parse and validate the input once.
2. Create an invariant data object used by every variant.
3. Set one deterministic seed for each stochastic layout.
4. Render each variant at the same preview size.
5. Record source paths and exact changed design variables.
6. Build a contact sheet with IDs `V1`, `V2`, etc.
7. Present a short comparison table:

```markdown
| Variant | Visual premise | Strengths | Tradeoffs | Recommended use |
|---|---|---|---|---|
| V1 | ... | ... | ... | ... |
| V2 | ... | ... | ... | ... |
| V3 | ... | ... | ... | ... |
```

8. Recommend one variant, but do not produce the final submission export until
   the user chooses or explicitly delegates the choice.

## Variant manifest

Keep a lightweight manifest next to the previews:

```text
variant_id:
figure_family:
data_source:
transformation:
statistical_invariants:
visual_premise:
changed_design_variables:
preview_path:
editable_source_path:
vector_master_path:
known_tradeoff:
asset_or_reference:
adaptation_level:
```

## Selection handling

When the user selects a variant:

1. Re-read the selected variant's source and data mapping.
2. Produce the final physical-size vector master and raster preview.
3. Re-run the full evidence and export QA.
4. Keep the variant gallery and manifest as provenance, not as submission files.
5. If the user asks to combine variants, list exactly which visual elements move
   from which variant and re-check collisions and consistency.

Do not assume the prettiest preview is the best manuscript figure. The recommended
variant should match the scientific reading task and the target medium.

