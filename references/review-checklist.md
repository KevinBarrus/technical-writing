# Technical Writing Review Checklist

## Purpose

Use this file for full, publication-readiness, or explicitly scoped reviews.
Review in descending order of consequence; do not spend formatting effort before
checking whether the document's conclusion and mechanism are correct.

## Select the review scope

| Request | Required work |
| --- | --- |
| Full / publication-ready | Run every applicable category below. |
| Technical correctness | Focus on claims, specifications, reasoning, complexity, code, experiments, and system semantics. |
| Style only | Check Markdown, typography, structure, and wording; report a visible technical error but do not reopen settled analysis. |
| Focused request | Check the named concern first; expand only for a severe related issue. |

Use the detailed rule source rather than duplicating it here:

- claim, scope, evidence, systems, algorithms, AI/ML: `technical-rigor.md`;
- code, pseudocode, formulas, and complexity: `code-and-math.md`;
- diagrams and figures: `diagrams.md`;
- Markdown and Chinese typography: `style-guide.md`.

## Severity

| Severity | Meaning | Publication action |
| --- | --- | --- |
| Critical | Invalidates a central implementation, explanation, experiment, security property, or conclusion. | Must fix. |
| Major | Materially weakens correctness, rigor, reproducibility, or the reader's mental model. | Normally fix. |
| Minor | Local clarity, consistency, notation, Markdown, or typography issue. | Fix during proofreading. |
| Optional | Valid alternative or preference. | Never block approval. |

Classify by consequence, not by how many words a fix requires. A wrong
algorithm, formula, protocol direction, destructive command, or leaked test
data is Critical. A missing assumption, overstated claim, incorrect complexity
model, misleading analogy, missing baseline, or code/prose disagreement is
normally Major.

## Review order

1. **Main conclusion and specification.** Identify what the article asks the
   reader to believe or implement. Verify it against the stated requirements,
   source, data, or implementation. Record ambiguities and the adopted
   interpretation.
2. **Claims and reasoning.** Check definitions, assumptions, scope, evidence,
   causal language, necessary/sufficient conditions, counterexamples,
   trade-offs, failure modes, and version sensitivity.
3. **Technical artifacts.** Check algorithm correctness and invariants;
   complexity cost model; code, pseudocode, formulas, examples, logs, commands,
   experiments, benchmarks, and sources.
4. **Structure and visuals.** Ensure headings support the argument, diagrams
   match the described boundaries and flow, and examples are placed near the
   claims they explain.
5. **Presentation.** Check terminology, Markdown, Chinese/English spacing and
   punctuation, symbols, units, links, captions, and accessibility.

## Cross-artifact checks

For every material conclusion, verify the prose against all artifacts that
support it:

- specification versus current implementation;
- code versus pseudocode, examples, and claimed edge cases;
- formula versus variable definitions, units, and calculated values;
- complexity conclusion versus operations and cost assumptions;
- experiment or benchmark conclusion versus configuration, baseline, metric,
  data split, and raw result;
- diagram versus system boundary, arrow direction, interaction type, and text;
- external claim versus source strength and applicable version.

When reviewing a revision, also check for regressions introduced by the edit:
changed code, terminology, numbers, diagrams, or wording must remain consistent
with dependent claims and artifacts.

## Reporting

For each Critical or Major finding provide:

```text
Severity: Major
Location: section, figure, code block, or quoted claim
Problem: what is wrong or missing
Why: how it affects correctness, scope, implementation, or reader understanding
Correction: a concrete replacement, test, source, or next action
```

Group repeated Minor issues by rule and locations. Keep distinct Major issues
separate. Preserve the author's intent, distinguish a diagnosis from a rewrite,
and never manufacture findings to make a review look exhaustive.

## Publication decision

Use one verdict:

- **Not ready:** a Critical issue remains.
- **Technically sound but needs revision:** one or more Major issues remain.
- **Ready after minor proofreading:** only Minor issues remain.
- **Publication-ready:** no known material issue or unmet source/
  reproducibility requirement remains.

Stop when the selected scope has been checked and further changes would be
stylistic alternatives rather than meaningful improvements. A document need not
be rewritten indefinitely to be publication-ready.
