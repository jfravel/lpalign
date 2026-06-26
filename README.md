# lpalign

`lpalign` is a small LaTeX package for formatting mathematical programs and for naming or referencing related displayed objects.

It currently provides:

- `lpalign` and `lpalign*` for optimization problems aligned on constraint relations
- `namedsubeqs` plus `\lpsubref` and `\lpsubeqref`, with `\sublabel` retained for compatibility
- `\paratitle` and `\namedpara` for named paragraphs
- quick horizontal and vertical spacing helpers
- display-style sum/product/union/intersection helpers with zero-width lower indices

## Installation

Place [`lpalign.sty`](/repos/lpalign/lpalign.sty) alongside your main `.tex` file and load it with:

```tex
\usepackage{lpalign}
```

The package requires `amsmath` and `expl3`. Loading `hyperref` is optional but recommended if you want clickable references.

## Documentation

The user documentation lives in [`lpalign-Documentaion.tex`](/repos/lpalign/lpalign-Documentaion.tex).

From the repository root, a simple local build is:

```bash
pdflatex -interaction=nonstopmode --aux-directory=build lpalign-Documentaion.tex
pdflatex -interaction=nonstopmode --aux-directory=build lpalign-Documentaion.tex
```

Run `pdflatex` twice if you want references and the table of contents fully resolved.

## Status

`v1.3` was published on June 26, 2026. The main visible changes since `v1.2` are the new `\namedpara` command, namespaced sub-equation references via `\lpsubref` and `\lpsubeqref`, and more robust parent-label handling inside `namedsubeqs` and traditional `subequations`.
