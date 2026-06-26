# lpalign

`lpalign` is a small LaTeX package for formatting mathematical programs and for naming or referencing related displayed objects.

This branch, `codex/lpalign-redesign`, is a design-and-experiment branch for the next `lpalign` layout revision. The goal here is to rethink the mathematical-programming environments before updating the full package documentation.

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

## Current Focus

The current redesign target is the `lpalign` / `lpalign*` environment pair.

The present `v1.3` implementation still has one structural annoyance inherited from the original `alignat` approach: the left-hand `sense` and `s.t.` labels are part of the alignment grid, so users must reserve their space indirectly with extra alignment structure. In practice this shows up most visibly as the trailing `&&` at the end of each constraint row.

The redesign goal is to keep the source as close as possible to ordinary `alignat` syntax while removing that fake left column.

## Proposed Direction

The current design target is:

```tex
\begin{lpalign}[<keys>]{<sense>}{<objective>}
  <raw aligned constraint body>
\end{lpalign}
```

with the starred form

```tex
\begin{lpalign*}[<keys>]{<sense>}{<objective>}
  ...
\end{lpalign*}
```

### Main ideas

- Keep `sense` and `objective` as mandatory arguments.
- Keep the constraint body close to raw `alignat` / `align` source.
- Remove the current fake left alignment column for `sense` and `s.t.`.
- Reserve a real left gutter whose width is measured from the `sense` and `s.t.` boxes.
- Place the left labels inside that gutter instead of forcing them into the alignment structure.
- Remove the structural `\\&&` placeholder at the end of ordinary constraint rows.
- Keep the qualifier column working during the first pass, even if that still means using `&& \forall ...` for now.

### Draft option keys

The current planned keys are:

- `vars`
- `st`
- `sense-pos = c|t|b`
- `st-pos = c|t|b`
- `sense-shift = <length>`
- `st-shift = <length>`
- `qualifier-sep = <length>`
- possibly `gutter-sep = <length>`

The current default direction is:

- `sense-pos = c`
- `st-pos = t`
- `sense-shift = 0pt`
- `st-shift = 0pt`
- `st = s.t.`

`sense` and `objective` stay mandatory because they are central to the visual structure and read naturally in the same order as a printed mathematical program.

### Example target syntax

```tex
\begin{lpalign}[vars={x \in \mathbb{R}_+^n}]{max}{c^\top x}
  Ax &= b & \forall i \in I \\
  x  &\ge 0
\end{lpalign}
```

The intended improvement over the current implementation is that the constraint body remains familiar to anyone who already reads `align` / `alignat`, but the old end-of-line `\\&&` boilerplate disappears on ordinary rows.

## Experiment Notes

For this phase, the README is the design note. The full user documentation in [`lpalign-Documentaion.tex`](/repos/lpalign/lpalign-Documentaion.tex) is intentionally not being updated in parallel, so that experiments can stay lightweight and can be tested locally without depending on the documentation toolchain.

When running quick TeX experiments from the repository root, the basic pattern is:

```bash
pdflatex -interaction=nonstopmode <scratch-file>.tex
pdflatex -interaction=nonstopmode <scratch-file>.tex
```

## Status

`v1.3` was published on June 26, 2026. The main visible changes since `v1.2` are the new `\namedpara` command, namespaced sub-equation references via `\lpsubref` and `\lpsubeqref`, and more robust parent-label handling inside `namedsubeqs` and traditional `subequations`.

This branch is not a release branch. It is a working branch for the next `lpalign` design cycle.

## Roadmap

Items intentionally deferred until after the first redesign pass:

- custom variable-line styling beneath the `sense` marker
- explicit gutter-width override keys
- more expressive vertical-position syntax beyond `t/c/b` plus additive shifts
- richer subject-to formatting beyond a single `st` label
- reducing the qualifier column from `&& <qualifier>` to a single `& <qualifier>` without losing alignment
- deciding whether the backend should remain `alignat` or switch to a different display engine if the gutter approach proves too fragile
- broader documentation updates in [`lpalign-Documentaion.tex`](/repos/lpalign/lpalign-Documentaion.tex) once the design stabilizes
