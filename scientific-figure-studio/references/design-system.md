# Scientific Figure Design System

Use these values as coordinated starting points. The target journal's current
instructions and the actual medium override them.

## Canvas and spacing

| Element | General manuscript starting point |
|---|---:|
| Single-column width | 90 mm |
| Double-column width | 180 mm |
| Typical double-column height cap | about 170 mm |
| Safety margin | about 5 mm |
| Panel gap | 3–5 mm |
| Axis-title to tick-label gap | 2–3 mm |
| Plot area to tick-label gap | 1–2 mm |

Set the canvas to the intended final output size. Height follows content; do not
stretch a figure to fill a template. A dense journal may require 89/183 mm or a
different height, so verify the exact live guide.

If content does not fit, in order: remove repeated legends, simplify labels,
change panel proportions, split the figure, then reduce type. Never shrink text
until it becomes technically present but practically unreadable.

## Figure archetypes

Choose by evidence structure:

- **Quantitative grid:** comparable plots share geometry and scales.
- **Schematic-led composite:** one visual model anchors subordinate validation.
- **Image plate + quantification:** representative images link visibly to
  replicate-level measurement.
- **Asymmetric mixed-modality figure:** one hero panel plus supporting evidence of
  unequal weight.

Avoid equal-sized panels when one piece of evidence is clearly the hero. The
composition should match the claim’s hierarchy.

## Typography

Use one family consistently. Arial, Helvetica, or an equivalent sans-serif is a
safe manuscript starting point.

| Element | Starting size |
|---|---:|
| Panel letter | 8 pt bold |
| Plot or axis title | 7–8 pt |
| Tick, legend, direct label | 6–7 pt |
| Necessary script glyph | preferably at least 6 pt |

- Use one text hierarchy across panels.
- Preserve canonical capitalization such as `XGBoost`, `GPT-5.2`, `RF`, and
  official gene/model names.
- Place panel letters consistently, usually near the top-left.
- Check actual rendered glyph size in PDFs; math superscripts often become smaller
  than their parent text.
- Keep live, selectable text in SVG/PDF unless a glyph forces a documented
  exception.

## Color

Start with one neutral plus two accents:

| Scheme | Neutral | Accent 1 | Accent 2 |
|---|---:|---:|---:|
| Blue–orange | `#BFC7CD` | `#3478A3` | `#D8864B` |
| Teal–red | `#C4C9C9` | `#398A88` | `#CF7169` |
| Purple–gold | `#C4C3CA` | `#7772A8` | `#BF934B` |

Choose by data semantics:

- unordered categories: qualitative palette;
- ordered magnitude: sequential scale;
- departure around a meaningful center: diverging scale fixed at that center;
- cyclic data: cyclic palette.

Dense points often start at 60%–80% opacity; uncertainty bands at 15%–25%. Check
the rendered result rather than treating those values as rules.

Do not use red/green as the only distinction. Do not reuse a sequential light–dark
scale as arbitrary categories. A neutral baseline should not appear more salient
than the primary evidence.

## Lines and marks

| Element | Starting size |
|---|---:|
| Primary curve | 1 pt |
| Axis / secondary curve | 0.75 pt |
| Error bar | 0.5–0.75 pt |
| Threshold / guide | 0.5 pt |
| Ordinary marker diameter | 2–3 pt |
| Highlight marker | 1.3–1.5 × ordinary |
| Leader line | 0.4–0.5 pt |

Use position first. Add color, shape, line style, hatch, direct labels, or panel
separation as redundant cues. For dense scatter, reduce size, increase
transparency, show a distribution summary, and label only meaningful
observations.

## Labels, legends, and axes

- Directly label stable or important categories; reserve a legend for what cannot
  be read in place.
- Do not cover data with labels or legend boxes.
- Keep leader lines short, sparse, and non-crossing.
- Put variable and unit together, for example `Time (months)`.
- Bars that encode magnitude normally start at zero. Nonzero limits may be valid
  for points and lines when the range is honest and visible.
- Prefer aligned panels over dual axes.
- Name the uncertainty: SD, SE, 95% CI, percentile interval, posterior interval,
  and so on. State the replication unit.
- Keep documented transformations and log handling visible in the caption or
  figure.

## Multi-panel consistency

Unify:

- font family and equivalent type levels;
- group colors;
- line and marker hierarchy;
- backgrounds and axis treatment;
- panel letters;
- comparable plot-area dimensions;
- scale limits where comparison requires them;
- legend placement or direct-label conventions.

Measure comparable plot-area rectangles after the final layout pass. A grid that
looks aligned can still have unequal tick-label margins or panel widths.

## Images and schematics

- Preserve original microscopy/pathology images.
- Apply comparable whole-image processing to images being compared.
- Do not locally enhance, erase background, clone, or crop selectively to change
  evidence.
- Verify scale-bar calibration and final legibility.
- Use editable SVG for hand-built schematics; keep text as text and avoid gradients,
  shadows, filters, and 3D.
- In schematics, one accent marks the paper's novel component; flow direction and
  arrowheads should carry meaning without reliance on color.

## Export bundle

Keep:

- source code or editable artwork;
- vector master: PDF or SVG for figures that are not inherently raster;
- preview: PNG for collaborators;
- source data and a short provenance note when required;
- final submission format specified by the venue.

For a 180 mm raster:

- 300 dpi target width ≈ 2126 px;
- 600 dpi target width ≈ 4252 px.

For a 90 mm raster:

- 300 dpi target width ≈ 1063 px;
- 600 dpi target width ≈ 2126 px.

Changing DPI metadata does not create detail in a low-pixel source. Open the final
export and check dimensions, font substitution, line visibility, image sharpness,
aspect ratio, opacity, and all four corners.
