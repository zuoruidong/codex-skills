---
name: nb-figure-studio
description: >-
  Unified scientific-figure workflow for creating, reading, auditing, revising,
  redesigning, and imitating data plots, multi-panel figures, vector schematics,
  graphical abstracts, and publication artwork. Use for 科研绘图、出图、审图、
  翻修、仿图、论文配图、figure redesign, reference-style adaptation, or final-size
  export review. Do not use for dashboards, video, or purely statistical analysis
  that does not need a figure.
metadata:
  version: "1.1"
---

# NB-figure-studio

Turn a scientific message into an honest, legible, reproducible figure, then
review it as both visual evidence and a deliverable. Keep creation, reading,
critique, revision, and reference-style adaptation in one coherent workflow.

## Start with the mode

Classify the request before choosing tools:

| User intent | Mode | Default deliverable |
|---|---|---|
| New plot, plate, multi-panel figure, schematic, or graphical abstract | **Make** | Editable source + vector + preview |
| Explain what an existing figure shows | **Read** | Evidence-led panel interpretation |
| Find problems in an existing figure | **Audit** | Severity-ranked review |
| Improve or redraw an existing figure | **Revise** | Revised figure + change log |
| Match the look or composition of reference figures | **Imitate** | Style transfer brief + adapted figure |
| “Make it publication-ready” | **Full loop** | Make → audit → revise → deliver |

For a combined request, use the smallest sequence that reaches the outcome. A
final reviewer typically runs `Audit + Revise + Audit`.

Read [references/modes.md](references/modes.md) for each mode's decision rules,
required inputs, and output contract. Read only the mode sections in use.

## Protect the scientific evidence

These constraints apply in every mode:

- Preserve source data, raw images, exclusions, transformations, uncertainty,
  statistical annotations, and image provenance.
- Do not invent, hide, selectively enhance, or “clean up” evidence to improve
  appearance.
- Do not infer a statistical test or exact value from visual appearance. Separate
  **Visible**, **Caption**, **Body**, **Data**, and **Inference** when reading.
- When a figure image is the only input, change visual design without pretending
  to have re-analyzed the underlying values.
- A polished figure is not automatically accessible, reproducible, or compliant
  with the target journal. Check the current official instructions when the exact
  venue and submission phase are known.

## Establish the figure contract

Before generation or structural revision, record:

1. one-sentence scientific claim and the comparison a reader must understand;
2. medium, final physical size, viewing distance, and target venue;
3. data/image provenance, variables, units, transformations, and uncertainty;
4. figure archetype and the inferential role of each panel;
5. editable source format, export bundle, and acceptance checks.

Use a compact contract for a single plot and a panel map for a composite figure.
Do not ask for information that can be inferred from supplied files. Ask only
when the missing choice changes the scientific output or the drawing backend.

## Choose the production route

- **Quantitative Python plot:** use the existing `nature-figure` Python route and
  `scientific-visualization` checks when available.
- **Quantitative R plot:** use the existing `nature-figure` R route, typically
  ggplot2/ComplexHeatmap with patchwork layout.
- **Editable schematic:** build SVG with live text; use the vector-schematic
  workflow rather than a raster generator.
- **AI bitmap, illustration, or graphical abstract:** use `imagegen`; treat the
  result as a draft visual, not quantitative evidence.
- **Domain plot:** use a validated domain script when the data contract matches.
  For the chart families learned in this toolkit, use the internal recipe index
  below rather than assuming a separately installed domain skill exists.
- **Reference-derived R figure:** read
  [references/reference-figure-recipes.md](references/reference-figure-recipes.md)
  before recreating volcano plots, circular UMAPs, L-axis UMAPs, irregular hull
  UMAPs, multi-track evidence wheels, or code shown in video/reference screenshots.

Read [references/capability-map.md](references/capability-map.md) for the current
skill/script routing table and fallback behavior.

For plotting code, resolve Python or R from the request, input workflow, this
task, or the saved default. If still unresolved, ask once: **Python or R? I will
remember this as your default.** Do not cross-render the final figure or its
previews in the other language.

## Apply one visual system

Start at final physical size. Make data and direct labels dominate, use a
restrained palette with redundant encodings, and unify typography, line weights,
marker sizes, legend behavior, and panel geometry.

Read [references/design-system.md](references/design-system.md) before styling or
redesigning a figure. Treat its dimensions as provisional defaults, not claims of
journal compliance.

## Review what is actually rendered

Inspect the exported file at final size, not only the source code or a large design
canvas. Review the whole figure, then each panel, then the panel relationships.
Use automated geometry checks when available, but do not treat them as proof that
the science, hierarchy, or accessibility is correct.

Read [references/qa-rubric.md](references/qa-rubric.md) for the severity model,
mode-specific checks, and pass conditions.

## Imitate the system, not the evidence

Reference figures can supply composition, typography, palette logic, panel
rhythm, mark grammar, and annotation conventions. They do not supply the user's
scientific values, unpublished claims, microscopy evidence, logos, or permission
to reproduce protected artwork.

Separate:

- visual DNA that can be transferred;
- plot-family and data-contract compatibility;
- source-specific content that must be replaced;
- provenance and rights constraints.

Read [references/imitation-and-reuse.md](references/imitation-and-reuse.md) before
any 仿图、reference-style redraw, template reuse, or image-to-image style transfer.

For structural ambiguity in Circos-style figures or density-driven UMAP
appearance, also read
[references/reference-figure-recipes.md](references/reference-figure-recipes.md).

## Maintain the skill

This skill is a living personal toolkit. When the user supplies a plotting
technique, strong reference, correction, or review lesson and asks to learn it:

1. Extract the generalizable principle, when it applies, and when it would be
   misleading. Separate a durable rule from a one-off aesthetic preference.
2. Check it against existing guidance. Merge or replace only after resolving
   conflicts; preserve stricter scientific-integrity and accessibility rules.
3. Put it in the right home: design values in `references/design-system.md`,
   review tests in `references/qa-rubric.md`, mode procedures in
   `references/modes.md` or `references/imitation-and-reuse.md`, and tool routing
   in `references/capability-map.md`.
4. Validate the skill. For a substantial workflow change, test it on a realistic
   figure request without creating misleading synthetic production data.
5. Update `metadata.version`. The current contract starts at `1.0`. Use a minor
   bump such as `1.1` for a new reusable technique or capability, a patch bump
   such as `1.0.1` for a correction, and `2.0` only for an incompatible
   restructuring.
6. Sync the workspace package, installed Codex skill, and public repository:
   <https://github.com/zuoruidong/codex-skills>. Commit, push, and verify that the
   remote `nb-figure-studio/` tree contains the change.
7. Report the new version, what was learned, and the GitHub commit. Never upload
   private source data, credentials, personal paths, or protected reference assets.

Do this proactively when the user explicitly asks to learn and save a technique.
For ordinary figure production, update the skill only when the user asks to
persist a reusable lesson.

## Delivery standard

Return the files appropriate to the medium:

- editable source or code;
- vector master when the figure is not inherently raster;
- final-size PNG/PDF preview;
- clean source data or a pointer to it;
- concise QA report with unresolved issues;
- before/after change log for revisions;
- style-transfer map and provenance note for imitation.

For a final figure, do not say “publication-ready” if text was clipped, labels
overlap, uncertainty is undefined, source data are missing, the target journal was
not checked, or automated checks could not run. State the exact remaining risk.
