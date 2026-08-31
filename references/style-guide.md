# Technical Writing Style Guide

## Priority

For Chinese technical Markdown, preserve semantic correctness first, then
readability, consistency, and typography. Apply one valid convention
consistently; adapt presentation to a platform only after preserving meaning.
Use `code-and-math.md` for programming syntax, formulas, and complexity.

## Prose, punctuation, and spacing

- The sentence language determines sentence punctuation: Chinese prose uses
  full-width `，。；：！？（）“”……——`; English prose uses half-width punctuation.
  A Chinese sentence ending in `Agent` or `merge_json()` still ends in `。`.
- Put one half-width space between Chinese and English words or Arabic numbers:
  `使用 Python 实现`、`进行了 10 次实验`. Do not insert spaces inside code,
  established tokens (`GPT-5`, `92.3%`, `IPv4`), paths, versions, or syntax.
- Use `、` for Chinese enumeration; use English commas and conjunctions in
  English prose. Do not use `/` or `\` as a generic enumeration marker.
- Keep pronoun referents clear. Prefer one main claim per sentence; split a
  sentence when scope, causality, or conditions become hard to inspect.

## Markdown structure

- Use continuous heading hierarchy; do not skip levels or add sentence-ending
  punctuation to headings. Number headings only when their order is meaningful.
- Separate adjacent block-level elements with one blank line. Do not create
  visual hierarchy through stacks of blank lines.
- Use lists for parallel items, keep list grammar parallel, and use ordered
  lists only where order matters. Avoid tabs for alignment.
- Tables should compare compact, homogeneous fields; move long explanations or
  code outside the table. Refer to figures and tables by an explicit name or
  number rather than “如下图”.
- Prefer descriptive link text. Ensure images have useful alt text where the
  publishing format supports it.

## Technical tokens and symbols

- Backtick literal identifiers, APIs, commands, paths, filenames, endpoints,
  environment variables, and expressions; do not backtick ordinary concepts for
  emphasis. Keep Chinese prose adjacent to inline code naturally readable:
  `调用 forward() 方法。`
- Use bold only for meaningful emphasis; do not combine bold, code, headings,
  and punctuation as decoration.
- In prose use `→` for flow; reserve `->`, `<=`, `==`, and similar ASCII forms
  for code. Use LaTeX operators in mathematical expressions.
- Use `-` for compound terms and command options, `–` for numeric ranges when
  appropriate, and `——` for a Chinese prose dash. State units and numerical
  precision consistently; distinguish `%` change from percentage points.

## Code blocks, figures, and naming

- Use fenced blocks with an accurate language identifier. A Python assignment
  is not JSON; label pseudocode as `text` or explicitly call it pseudocode.
- Keep titles, product names, abbreviations, capitalization, and terminology
  consistent. Define unfamiliar abbreviations on first use; do not repeatedly
  redefine established ones.
- Captions should state what a figure, table, or code sample shows and the
  scope of the data when relevant. Do not use decorative diagrams or screenshots
  as evidence.

## Final pass

Check sentence punctuation, Chinese-English/number spacing, inline-code scope,
heading hierarchy, block spacing, list consistency, code-fence labels, units,
links, figure references, terminology, and accidental symbol substitution. Fix
only presentation issues here; return to the relevant technical guide if a
formatting inconsistency reveals a semantic error.
