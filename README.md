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

The user documentation lives in [`lpalign-Documentaion.tex`](/repos/lpalign/lpalign-Documentaion.tex).

From the repository root, a simple local build is:

```bash
pdflatex -interaction=nonstopmode --aux-directory=build lpalign-Documentaion.tex
pdflatex -interaction=nonstopmode --aux-directory=build lpalign-Documentaion.tex
```

Run `pdflatex` twice if you want references and the table of contents fully resolved.

## Regression Tests

Small manual regression files live in [`tests/`](/repos/lpalign/tests):

- `HookError.tex` checks package loading with `hyperref`
- `test-subequations.tex` checks standard `subequations`
- `test-namedsubeqs.tex` checks `namedsubeqs`
- `test-mixed.tex` checks mixed usage with `lpalign`

Compile them from the repository root, and compile each file twice. For example:

```bash
pdflatex -interaction=nonstopmode tests/HookError.tex
pdflatex -interaction=nonstopmode tests/HookError.tex
```

## Status

This repository is still in a light pre-packaging state. The current pass focuses on small consistency fixes and documentation cleanup rather than structural redesign.
