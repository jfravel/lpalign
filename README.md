# lpalign

`lpalign` is a small LaTeX package for formatting mathematical programs and for naming or referencing related displayed objects.

Current release:
- `v1.5`
- published July 6, 2026

The package currently provides:
- `lpalign` and `lpalign*` environments for writing mathematical programs within `alignat`,
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

Package-load defaults are available for:
- `lp_objective_sep`
- `lp_qualifier_sep`
- `lp_gutter_sep`
- `lp_vars_style`
- `lp_st`

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

Package-load defaults are available for:
- `namedsubeqs_style`
- `namedsubeqs_punct`

## Package-Load Options

The package supports the following load-time defaults:

- `lp_objective_sep`
- `lp_qualifier_sep`
- `lp_gutter_sep`
- `lp_vars_style`
- `lp_st`
- `namedpara_indent`
- `namedparabefore`
- `namedparaafter`
- `namedparaflush`
- `namedsubeqs_style`
- `namedsubeqs_punct`
- `evaluator_spacing`

Example:

```tex
\usepackage[
  lp_objective_sep=0em,
  lp_qualifier_sep=2em,
  lp_gutter_sep=0.75em,
  lp_vars_style=scriptstyle,
  lp_st=subject\ to,
  namedpara_indent=2em,
  namedsubeqs_style=roman,
  namedsubeqs_punct=:,
  evaluator_spacing=0.35em
]{lpalign}
```

For package-load style defaults, use the style names rather than raw control sequences:
- `lp_vars_style`: `scriptstyle`, `scriptscriptstyle`, `textstyle`, `displaystyle`
- `namedsubeqs_style`: `alph`, `Alph`, `arabic`, `roman`, `Roman`

## Documentation

The full package documentation is in [`lpalign-Documentaion.pdf`](/repos/lpalign/lpalign-Documentaion.pdf).


## Contributions
This package was, from versions 1.2-1.5, developed with assistance of OpenAI Codex.
