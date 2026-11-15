# Figure Studio Modes

This reference defines the operating contract for each mode. Load only the
relevant sections.

## Contents

- Make
- Read
- Audit
- Revise
- Imitate
- Full loop

## Make

Use when the user supplies data, a concept, or a brief and wants a new visual.

### Decide the deliverable

- **Data plot:** quantitative marks backed by supplied data, with reproducible
  code and source-data traceability.
- **Multi-panel figure:** a sequence of panels with different inferential roles,
  assembled under one figure-level claim.
- **Editable schematic:** components and relationships supplied by the paper or
  code, drawn as live text and shapes.
- **AI raster illustration / graphical abstract:** a visual explanation or cover
  artwork that is not a substitute for measured results.
- **Domain figure:** a known chart family with a validated implementation, such as
  volcano, forest, survival, enrichment, or image plate.

Choose the route before styling. A quantitative request should not become a
generated bitmap merely because that is easier. A conceptual request should not be
forced into plotting code when an editable vector diagram is the appropriate
artifact.

### Build the contract

Capture only what changes the figure:

```text
Claim:
Audience / medium:
Final width and height:
Figure archetype:
Panel map:
Data or image sources:
Transformations:
Uncertainty / n:
Statistics and annotations:
Required exports:
Known constraints:
```

For a single chart, this may collapse into a short brief. For a multi-panel
figure, map each panel to a distinct role: discovery, mechanism, validation,
comparison, robustness, or biological/clinical relevance. Merge panels that
repeat the same evidence under a secondary metric.

### Produce

1. Inspect the real input schema and image properties before coding.
2. Preserve raw data and keep transformed analysis outputs distinct.
3. Resolve the backend and render at final physical size.
4. Use the shared design system before adding panel-specific styling.
5. Export an editable master and a preview.
6. Run source, geometry, text, collision, and final-size visual checks that apply.
7. Deliver the contract, output paths, and unresolved assumptions.

Do not create synthetic data to fill a missing input. A labelled demonstration
may be produced only when the user asks for a template or synthetic example, and
it must never be mixed with production results.

## Read

Use when the user asks what a figure shows, whether a conclusion is visible, or
how to interpret panels.

1. Inspect the complete figure, caption, and the sentences that cite it.
2. Record panel layout, plot family, axes, units, legend, n, statistics, scale
   bars, transformations, and missing/unreadable elements.
3. Inspect each panel separately; crop only to resolve or enlarge existing
   evidence.
4. Keep source layers distinct: Visible, Caption, Body, Data, Inference.
5. State what the figure supports, what it does not establish, and alternative
   explanations.
6. End with ambiguities and conflicts.

If images cannot be visually inspected, do not claim to have done so. Limit the
report to text/data and state that the visual evidence remains unverified.

Output may be concise for one plot, but a multi-panel figure should include a
panel/page table.

## Audit

Use when the user asks whether a figure is correct, readable, consistent,
publication-ready, or suitable for a venue.

### Review layers

1. **Scientific integrity:** claim, data, exclusions, axes, transforms, uncertainty,
   n, statistics, images, and provenance.
2. **Evidentiary logic:** whether each panel supports its assigned claim and
   whether the whole figure overstates the evidence.
3. **Composition:** hierarchy, plot-area geometry, labels, legends, spacing,
   contrast, redundancy, and accessibility.
4. **Technical delivery:** dimensions, fonts, text editability, raster resolution,
   clipping, transparency, file integrity, and journal-stage requirements.

### Assign severity

- **Blocker:** scientific distortion, unreadable core evidence, missing source
  data for a claimed upload-ready figure, clipping, or a failed required audit.
- **Should fix:** ambiguous unit/statistic, weak hierarchy, inconsistent
  alignment, inaccessible encoding, unnecessary overlap, or misleading scale.
- **Polish:** refinements that do not change reading or interpretation.

Every issue needs evidence, effect, and a concrete remedy. Do not produce a generic
checklist with no diagnosis.

### If the user supplied source

Check the code or editable source for:

- data filtering and accidental simulated-data leakage;
- axis limits, baselines, log guards, aggregation, and smoothing;
- font settings and export dimensions;
- cross-backend rendering or stale previews;
- legends and annotations generated from transformed values;
- output provenance.

Fix blockers when the request includes revision; otherwise report them without
silently changing the artifact.

## Revise

Use when the user asks to improve, polish, redraw, simplify, restyle, or fix a
figure.

### Determine the revision ceiling

- **Source + data available:** full scientific and visual revision is possible.
- **Editable vector without data:** preserve encoded values and edit layout,
  typography, labels, and vector geometry only.
- **Raster only:** preserve visible evidence; use targeted edits or a control-based
  redraw without claiming to restore hidden data.
- **No original assets:** treat an image-to-image result as a visual draft requiring
  human comparison and never as exact numerical reconstruction.

### Revision sequence

1. Run or summarize the audit.
2. Declare invariants: claim, data, limits, groups, uncertainty, statistics,
   scale bars, crop, color semantics, and all text that carries scientific meaning.
3. Fix evidence and reading blockers before decoration.
4. Change layout, typography, color, and labels through the shared design system.
5. Re-render at final size.
6. Compare before/after and rerun the same audit.
7. Return an exact change log and list any untouched issues.

Prefer the smallest change that fixes the reading problem. Do not “improve” a
figure by hiding hard-to-read but valid evidence, changing significance, or
removing inconvenient groups.

## Imitate

Use when the user supplies one or more reference figures and asks to mimic,
reproduce, adapt, or match their style.

Follow [imitation-and-reuse.md](imitation-and-reuse.md). The default is a
style-system transfer with new content, not pixel-level copying.

Return:

- a compact style DNA;
- transferred versus excluded elements;
- the adapted source and figure;
- an originality/provenance note;
- remaining fidelity gaps.

## Full loop

For “从数据到投稿级图” or repeated refinement:

```text
contract
→ first render
→ evidence audit
→ visual audit
→ fix blockers
→ final-size review
→ delivery bundle
```

Stop the loop when the contract is met and remaining items are documented
constraints. Do not keep restyling after the scientific reading is already clear.
