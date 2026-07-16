# lpalign

`lpalign` is a small LaTeX package for formatting mathematical programs and for naming or referencing related displayed objects.

Current release:
- `v1.6`
- published July 16, 2026

The package currently provides:
- `lpalign` and `lpalign*` environments for writing mathematical programs with an `IEEEeqnarray` backend,
- `lpregion` and `lpregion*` environments for aligned or centered constraint regions without an objective row,
- `\namedpara` for named paragraphs with referencable abbreviations,
- `namedsubeqs` plus `\lpsubref` and `\lpsubeqref` for referencing subequations in a named environment,
- quick horizontal and vertical spacing helpers and
- display-style operator helpers which mimic `\smashoperator` from `mathtools` while prexerving ordinary `_`/`^` syntax.

## Installation

Place [`lpalign.sty`](/repos/lpalign/lpalign.sty) alongside your main `.tex` file and load it with:

```tex
\usepackage{lpalign}
```

The package loads:
- `IEEEtrantools`
- `expl3`
- `l3keys2e`

If available, it also loads:
- `mathtools`
- `stackengine`

Built-in fallbacks are provided for the small pieces currently needed from `mathtools` and `stackengine`.

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
- `flush`
- `objective-sep`
- `row-sep`
- `qualifier-sep`
- `gutter-sep`
- `sense-shift`
- `st-shift`

Package-load defaults are available for:
- `objective-sep`
- `row-sep`
- `qualifier-sep`
- `gutter-sep`
- `vars-style`
- `st`
- `flush`

Example:

```tex
\begin{lpalign}[vars=\mathbf{x}\in\mathbb{R}_+^n]{Maximize}{\mathbf{c}^\top\mathbf{x}}
  A\mathbf{x} &\le \mathbf{b} \\
   \mathbf{x} &\ge \mathbf{0}
\end{lpalign}
```

Qualified constraints use a second `&`-separated column:

```tex
\begin{lpalign}{Maximize}{\sum_{j=1}^m c_j x_j}
  \mathbf{a}_i^\top \mathbf{x} &\le b_i & \forall i \in [n] \\
  x_i                          &\ge 0   & \forall i \in [n]
\end{lpalign}
```

## `lpregion`

The constraints-only companion environment is:

```tex
\begin{lpregion}[<keys>]
  <constraint rows>
\end{lpregion}
```

The starred form suppresses automatic tags unless you add them explicitly.

Supported keys include:
- `flush`
- `row-sep`
- `qualifier-sep`

Package-load defaults are available for:
- `region-flush`

Example:

```tex
\begin{lpregion}[flush=c, qualifier-sep=3em]
  \mathbf{a}_i^\top \mathbf{x} \le b_i & \forall i \in [n] \\
  x_i \ge 0                            & \forall i \in [n]
\end{lpregion}
```

## Named Paragraphs

`namedpara` displays a paragraph marker and, when labeled, uses the supplied abbreviation as the reference text.

```tex
\namedpara{Named Paragraph}[NPg]\label{npara}
Paragraph \ref{npara} is a named paragraph.
```

Supported keys include:
- `abv`
- `indent`
- `before`
- `after`
- `flush`

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

Package-load defaults are available for:
- `namedsubeqs-style`
- `namedsubeqs-punct`

## Package-Load Options

The package supports the following load-time defaults:

- `objective-sep`
- `row-sep`
- `qualifier-sep`
- `gutter-sep`
- `vars-style`
- `st`
- `flush`
- `region-flush`
- `namedpara-indent`
- `namedpara-before`
- `namedpara-after`
- `namedpara-flush`
- `namedsubeqs-style`
- `namedsubeqs-punct`
- `evaluator-spacing`

For package-load style defaults, use the style names rather than raw control sequences:
- `vars-style`: `scriptstyle`, `scriptscriptstyle`, `textstyle`, `displaystyle`
- `namedsubeqs-style`: `alph`, `Alph`, `arabic`, `roman`, `Roman`

For `st`, bare spaces in `\usepackage[...]` are stripped by LaTeX before the package sees the option value. Use either:
- `st={subject to}`
- `st=subject~to`

## Documentation

The full package documentation is in [`lpalign-Documentaion.pdf`](/repos/lpalign/lpalign-Documentaion.pdf).

## Contributions
This package was, from versions 1.2-1.5, developed with assistance of OpenAI Codex.
