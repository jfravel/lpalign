# lpalign

`lpalign` is a small LaTeX package for formatting mathematical programs and for naming or referencing related displayed objects.

It currently provides:

- `lpalign` and `lpalign*` for optimization problems aligned on constraint relations
- `namedsubeqs` plus `\sublabel`, `\subref`, and `\subeqref`
- `\paratitle` for named paragraphs
- quick horizontal and vertical spacing helpers
- display-style sum/product/union/intersection helpers with zero-width lower indices

## Installation

Place [`lpalign.sty`](/repos/lpalign/lpalign.sty) alongside your main `.tex` file and load it with:

```tex
\usepackage{lpalign}
```

The package requires `amsmath` and `expl3`. Loading `hyperref` is optional but recommended if you want clickable references.

## Documentation

The user documentation lives in [`Documentation/lpalign-Documentaion.tex`](/repos/lpalign/Documentation/lpalign-Documentaion.tex).

From `Documentation/`, `latexmk` will pick up the bundled search path config automatically:

```bash
cd /repos/lpalign/Documentation
latexmk -pdf lpalign-Documentaion.tex
```

If you prefer to run `pdflatex` directly, use:

```bash
cd /repos/lpalign/Documentation
TEXINPUTS=..: pdflatex -interaction=nonstopmode -output-directory build lpalign-Documentaion.tex
```

Run `pdflatex` twice if you want references and the table of contents fully resolved.

## Status

This repository is still in a light pre-packaging state. The current pass focuses on small consistency fixes and documentation cleanup rather than structural redesign.
