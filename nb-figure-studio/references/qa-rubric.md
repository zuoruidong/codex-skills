# Scientific Figure QA Rubric

Review the rendered artifact, the underlying evidence, and the delivery package.
Use a verdict only when all required layers were actually checked.

## Severity model

### Blocker

Delivery should stop until resolved:

- invented, hidden, selectively enhanced, or mislabeled data;
- wrong direction, units, thresholds, transforms, or statistical interpretation;
- an axis or visual encoding that materially exaggerates the claimed effect;
- legend/color mapping inconsistent with the plotted groups;
- undefined uncertainty used as if it were an inferential interval;
- illegible core labels, clipped content, or overlapping text that blocks reading;
- missing source data when the requested deliverable requires traceability;
- a required alignment, text, or collision audit fails or cannot run.

### Should fix

Materially weakens reading, consistency, or reviewer confidence:

- the core comparison is not visually dominant;
- comparable panels have unexplained different scales;
- uncertainty is inconsistent across comparable panels;
- repeated legends inflate the figure;
- color is the sole encoding or fails contrast/grayscale screening;
- labels force excessive eye travel or obscure data;
- fonts, panel letters, or gutters are visibly inconsistent;
- raster detail is inadequate at final size;
- the caption cannot identify groups, statistics, or transformations.

### Polish

Improves finish without changing interpretation:

- small spacing tune;
- small type/weight refinement;
- non-semantic color adjustment;
- optional direct-labeling or whitespace optimization.

## Universal checks

### Scientific meaning

- One figure-level message is clear.
- Each panel has a distinct inferential role.
- Direction, units, groups, transformations, and thresholds are identifiable.
- Raw evidence and transformations are preserved.
- Missing values, exclusions, zero, censoring, and out-of-range values remain
  distinguishable.
- `n`, center/spread, tests, correction, and comparison are documented where used.
- The figure does not claim more than the design supports.

### Visual hierarchy

- Data and essential annotation dominate frames, grids, and decoration.
- The hero comparison is visible without reading the whole caption.
- Color follows data semantics and is redundant.
- Labels are legible and do not cover the evidence they explain.
- Legends are necessary, close to their panel, and non-obstructive.
- The composition does not force unrelated comparisons across the page.

### Consistency and geometry

- Equivalent text levels use one hierarchy.
- Group colors remain stable within the figure.
- Comparable panels share scales, limits, uncertainty, and plot-area geometry when
  the comparison requires it.
- Panel letters align and follow the paper's convention.
- Margins and gutters use space intentionally.
- Labels and lines remain clear after final scaling.
- All four corners, scale bars, colorbars, and statistical brackets are visible.

### Accessibility

- Contrast is readable at final size.
- Important color distinctions survive common color-vision deficiencies and a
  grayscale screening.
- Marker, line style, position, hatch, or direct label adds a redundant cue.
- Complex web figures have alt text/description and a data alternative when
  applicable.

### Image integrity

- Native pixel detail is adequate for final display.
- Compared images received consistent processing.
- Scale bars are calibrated.
- Crops, stitching, channel merges, pseudo-color, and reuse are documented when
  material.
- No local enhancement or background manipulation changes evidence.

### Export

- Canvas matches intended physical size.
- Fonts, line weights, and markers survive final scaling.
- Text is not clipped and is editable unless an exception is documented.
- Embedded rasters are not stretched or blurred.
- Background opacity is intentional.
- PDF/SVG/PNG/TIFF open correctly.
- The exact journal/phase instructions were checked before using “compliant.”

## Mode-specific checks

### Read

- Every discovered panel is identified and checked.
- Caption and citing text are compared with visible evidence.
- Exact numbers are reported only when printed or in source data.
- Unreadable details remain explicitly unreadable.
- Visible observation is not silently promoted to inference.

### Imitate

- The style DNA separates layout, type, palette, mark grammar, density, annotation,
  and image treatment.
- The new figure reuses structure without importing source-specific scientific
  content or protected marks.
- The data contract of the template matches the new data.
- Provenance and rights are recorded.
- Similarity does not create a false claim of exact journal compliance.

### Revise

- Invariants are listed before edits.
- The blocker list is resolved before cosmetic changes.
- The revised file is produced from the highest-fidelity available source.
- A before/after comparison confirms the intended change without unintended drift.
- All previously applicable QA checks are rerun.

### AI raster or graphical abstract

- Text is inspected for accuracy and not assumed correct.
- No numbers, mechanisms, or components were invented by the image model.
- Scientific claims are checked against the brief or manuscript.
- The output is identified as generated artwork and is not presented as measured
  evidence.
- Publication-policy and disclosure requirements are left for verification against
  the target venue.

## Automated checks

When the installed `nature-figure` source skill is available, use its scripts
according to [capability-map.md](capability-map.md):

- source validator;
- PDF text/glyph-size audit;
- multi-panel alignment audit;
- rendered text/stroke collision audit;
- SVG schematic audit.

Automated pass means only that the checked property passed. It does not prove
correct statistics, honest encoding, accessible color, or journal acceptance.

If an automated check cannot run, report `not checked`, not `pass`.

## Review output

Use this compact schema:

```markdown
Verdict: PASS | PASS WITH CAVEATS | BLOCKED

Blocker
- [location] issue → effect → required fix

Should fix
- [location] issue → effect → required fix

Polish
- [location] issue → optional refinement

Checks completed
- evidence/data:
- final-size visual:
- text/geometry:
- export/venue:

Unresolved constraints
- ...
```

For a review-only request, do not modify the figure. For a revision request, turn
the blocker and should-fix list into the implementation sequence.
