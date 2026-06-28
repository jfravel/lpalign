# lpalign

`lpalign` is a small LaTeX package for formatting mathematical programs and for naming or referencing related displayed objects.

Current release:
- `v1.4 final`
- published June 28, 2026

The package currently provides:
- `lpalign` and `lpalign*` for optimization problems aligned on constraint relations
- `namedsubeqs` plus `\lpsubref` and `\lpsubeqref`
- `\paratitle` and `\namedpara` for named paragraphs
- quick horizontal and vertical spacing helpers
- display-style operator helpers that preserve ordinary `_`/`^` syntax while applying `\smashoperator`

## Installation

Place [`lpalign.sty`](/repos/lpalign/lpalign.sty) alongside your main `.tex` file and load it with:

```tex
\usepackage{lpalign}
```

The package loads:
- `amsmath`
- `expl3`
- `l3keys2e`
- `mathtools`
- `stackengine`

Loading `hyperref` is optional but recommended if you want clickable references.

## `lpalign`

The main environment is:

```tex
\begin{lpalign}[<keys>]{<sense>}{<objective>}
  <constraint rows>
\end{lpalign}
```

The starred form suppresses automatic tags unless you add them explicitly:

```tex
\begin{lpalign*}[<keys>]{<sense>}{<objective>}
  ...
\end{lpalign*}
```

Supported keys include:
- `vars`
- `vars-style`
- `st`
- `objective-sep`
- `qualifier-sep`
- `gutter-sep`
- `sense-shift`
- `st-shift`

Example:

```tex
\begin{lpalign}[vars=\mathbf{x}\in\mathbb{R}_+^n]{Maximize}{\mathbf{c}^\top\mathbf{x}}
  A\mathbf{x} &\le \mathbf{b} \\
   \mathbf{x} &\ge \mathbf{0}
\end{lpalign}
```

Qualified constraints still use `&&`:

```tex
\begin{lpalign}{Maximize}{\sum_{j=1}^m c_j x_j}
  \mathbf{a}_i^\top \mathbf{x} &\le b_i && \forall i \in [n] \\
  x_i                          &\ge 0   && \forall i \in [n]
\end{lpalign}
```

Package-load defaults are available for the three main spacing keys:

```tex
\usepackage[
  lp_objective-sep=1em,
  lp_qualifier-sep=3em,
  lp_gutter-sep=1em
]{lpalign}
```

## Named Paragraphs

`namedpara` displays a paragraph marker and, when labeled, uses the supplied abbreviation as the reference text.

```tex
\namedpara{Named Paragraph}[abv=NPg]\label{npara}
Paragraph \ref{npara} is a named paragraph.
```

Supported keys include:
- `abv`
- `indent`
- `before`
- `after`
- `flush`

The package-load default indent can be changed with:

```tex
\usepackage[namedpara_indent=3em]{lpalign}
```

The legacy `\paratitle` command remains available unchanged.

## Named Sub-equations

`namedsubeqs` gives a shared main tag to a group of equations while letting each line carry its own sub-index.

```tex
\begin{namedsubeqs}{EQ}
\begin{align}
  A\mathbf{x} &= \mathbf{b} \label{eq:1} \\
  C\mathbf{y} &= \mathbf{d} \label{eq:2}
\end{align}
\end{namedsubeqs}
```

Use:
- `\ref` / `\eqref` for the full tag
- `\lpsubref` / `\lpsubeqref` for the sub-index only

Example:

```tex
Equation \ref{eq:1} has sub-reference \lpsubref{eq:1}.
```

## Documentation

The full package documentation is in [`lpalign-Documentaion.tex`](/repos/lpalign/lpalign-Documentaion.tex).

Build it from the repository root with:

```bash
pdflatex -interaction=nonstopmode lpalign-Documentaion.tex
pdflatex -interaction=nonstopmode lpalign-Documentaion.tex
```
