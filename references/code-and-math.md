# Code and Math Style Guide

## Purpose

Keep natural-language prose, mathematical notation, and programming syntax
semantically and visually distinct. This guide covers code examples,
pseudocode, formulas, complexity, numeric claims, and their review.

## Choose the notation by meaning

| Meaning | Use |
| --- | --- |
| Prose flow | `A → B → C` |
| Mathematical mapping / implication | `$f : X \to Y$`, `$A \Rightarrow B$` |
| Program syntax | `->`, `<=`, `!=`, `==` inside code |
| Literal program entity | inline code, such as `merge_json()` or `config.yaml` |

Never replace program syntax with visually similar Unicode characters. Use
LaTeX for mathematical variables, operators, sets, functions, fractions,
subscripts, sums, probability, objectives, and relations when Markdown supports
it. Define variables, domains, indexing conventions, units, and assumptions
before relying on them; do not overload a symbol for unrelated concepts.

## Code and pseudocode

- Use inline code for literal variables, classes, methods, literals,
  expressions, files, paths, commands, environment variables, and routes—not
  for ordinary prose concepts.
- Use fenced blocks for multiline examples and label the actual language.
  Distinguish JSON, JavaScript object literals, Python dictionaries, YAML,
  shell output, SQL, logs, diffs, and pseudocode.
- Runnable code must have valid syntax, required imports/context where needed,
  and behavior consistent with the surrounding explanation. A small conceptual
  fragment may omit boilerplate only when labeled as a fragment.
- Pseudocode may omit language detail, but must be explicitly labeled and must
  state its relevant control flow and data transformations.
- Preserve code identifiers, comments, placeholders, redactions, paths, error
  messages, and truncation faithfully. Comments explain intent, invariants,
  assumptions, or non-obvious trade-offs—not syntax already visible.
- Verify that prose, variables, branches, return values, examples, inputs and
  outputs, edge cases, and complexity claims all describe the shown code.

## Formula and numerical reasoning

For a formula, define each symbol and its shape/type; state whether bounds are
inclusive, the base of any logarithm, and the units/precision of measured
quantities. Keep assignment, equality, definition, approximation, and logical
implication distinct. Map important formula terms to the code that computes
them.

For vectors, matrices, tensors, probabilities, losses, recurrences, dynamic
programming states, invariants, floating-point comparisons, numerical stability,
overflow, and ranges, state the convention or boundary condition that changes
the result. A formula-derived number must show its inputs and rounding; a
code-derived number must identify the relevant implementation and configuration.

Do not call an engineering explanation a mathematical proof. Examples and tests
are evidence, not exhaustive verification, unless their coverage justifies that
claim.

## Complexity protocol

For every nontrivial complexity statement:

1. Define input-size variables and the primitive-operation cost model.
2. Analyze loops, branching, recursion call count and recursion depth
   separately, and output size.
3. Include hidden work in built-ins and libraries: equality, hashing, copying,
   string operations, serialization, canonicalization, sorting, allocation, and
   I/O where relevant.
4. Separate average and worst case; name implementation, runtime, or container
   assumptions behind average `O(1)` behavior.
5. Separate output space, auxiliary space, and recursion-stack space.
6. Distinguish asymptotic cost from measured wall-clock performance.

Do not infer complexity from indentation alone. In particular, membership in a
list includes scans and potentially non-constant equality; hashing composite
objects or constructing a canonical hashable representation can add traversal,
sorting, and allocation. Claim an optimization only for the operation whose full
replacement cost has been accounted for.

## Review checklist

- Is each code fence syntactically and semantically labeled correctly?
- Are code, prose, formulas, examples, and tests mutually consistent?
- Are every material variable, unit, dimension, domain, bound, and assumption
  defined near its use?
- Are implementation/runtime-sensitive costs and numeric behavior scoped?
- Does the stated complexity include hidden costs and distinguish cases/spaces?
- Can a reader tell whether a fragment is runnable code, pseudocode, log,
  command, data, or a simplified illustration?
