---
name: technical-writing
description: >
  Write, rewrite, and review rigorous Chinese computer science technical content:
  blogs, learning notes, algorithm explanations, interview write-ups, source-code
  analyses, project documentation, and engineering articles. Use for technical
  Markdown involving code, mathematics, complexity, diagrams, experiments,
  backend systems, databases, networks, AI Agents, RAG, LLMs, or machine learning.
---

# Technical Writing

## Purpose

Produce technical writing with technical correctness, explicit assumptions,
rigorous reasoning, clear explanation, stable terminology, and readable
Markdown. Aim for technical-blog readability with paper-like rigor; do not make
prose academic merely to appear rigorous.

Prioritize:

> Correctness → Rigor → Clarity → Consistency → Concision → Presentation

Formatting never overrides technical meaning. Match formality to the task: do
not turn every document into a paper, formal proof, benchmark report, or
diagram-heavy system design.

## Mode and depth

Choose a mode first:

- **Writing:** identify audience, purpose, main claims, terms, assumptions, and
  only the artifacts that improve the explanation. Do a lightweight consistency
  check before returning.
- **Rewrite:** preserve technical meaning, assumptions, terminology, audience,
  and author voice. Explain any correction to an incorrect or unsupported claim;
  direct rewriting is enough for ordinary wording changes.
- **Review:** check correctness before punctuation. Review in this order:
  technical correctness, specification/assumptions, reasoning, terminology,
  code/math/complexity, experiments/evidence, structure/diagrams, then
  Markdown/typography.

Choose the smallest review depth that works:

| Depth | Use for | Scope |
| --- | --- | --- |
| Local | A sentence, paragraph, format, term, code fragment, formula, or diagram | Affected area and nearby dependencies. |
| Technical | Algorithms, source analysis, systems, Agents, databases, networks, or empirical conclusions | Correctness, assumptions, reasoning, and relevant artifacts. |
| Publication | Explicit full/final/publication-readiness review | Use `references/review-checklist.md`. |

## Claim protocol

For every important claim, establish its type, evidence, assumptions, scope,
and wording strength. Distinguish definitions, specifications, established
facts, assumptions, derivations, implementation details, experimental results,
engineering observations, intuitions, analogies, and recommendations. Do not
let one category masquerade as another.

Never silently resolve a material conflict between requirements, examples, API
behavior, documentation, source code, or an experiment. State the conflict, the
chosen interpretation, the reason, and material consequences of alternatives.

Treat “一定”, “必然”, “完全”, “所有”, “唯一”, “最优”, “保证”, “证明”, “显著”,
“永远”, “不可能”, and “彻底解决” as review triggers: provide the supporting
scope/evidence or weaken the wording. State assumptions close to the conclusion
they affect, including input constraints, version, runtime, engine, deployment,
concurrency, network, cost model, dataset, and experiment configuration.

Explain observable mechanisms—state, input, output, and control flow—instead
of anthropomorphic shorthand. Use analogies only as bounded mental models:
state where an analogy stops applying if it can create a false conclusion. Use
one primary term per concept, preserve official capitalization, and define an
unfamiliar abbreviation on first use.

## Code, mathematics, and complexity

Keep code syntax, mathematical notation, and prose distinct. Use exact syntax
in code; LaTeX for mathematical notation where supported; inline code for
literal identifiers, commands, paths, endpoints, and expressions; and explicit
labels for pseudocode. Code, prose, examples, formulas, edge cases, and
complexity claims must describe the same behavior.

For a nontrivial complexity claim, define input-size variables and cost
assumptions, analyze loops/recursion and hidden library work, distinguish
average from worst case, and separate output, auxiliary, and recursion-stack
space. Account for equality, membership, hashing, sorting, copying,
serialization, canonicalization, string operations, and allocation when
relevant. Do not infer complexity from indentation or call a local speedup an
whole-algorithm asymptotic improvement without accounting for new work.

## Evidence, experiments, and external facts

Treat experiments as observations under their stated configuration, not proof
of a general or causal rule. Record enough of the dataset/split, metric,
baseline, model/version, hyperparameters, variance, hardware, and evaluation
protocol to support the actual conclusion; distinguish percentage points from
relative percentage change.

For an external, verifiable, current, or version-sensitive fact, prefer a
standard/specification, original paper, official documentation, official source
code, or official engineering material, as appropriate. State the relevant
version/scope and do not strengthen a source's claim.

## Domain guidance

- **Algorithms:** explain interpretation, key observation, invariant or
  correctness reasoning, edge cases, implementation, and complexity.
- **Systems:** separate process/thread, local/distributed, sync/async, API
  contract/current implementation, persistence/cache, and mitigation/guarantee;
  state failure and concurrency assumptions.
- **Databases/networks:** distinguish semantic layers from engine, optimizer,
  storage, transport, protocol, and deployment behavior; qualify version when
  relevant.
- **Agents/RAG:** distinguish model, runtime, tools, context, memory, retrieval,
  plan, execution, and observation. Define ambiguous terms operationally; RAG
  is more than vector search.
- **Machine learning:** distinguish architecture, objective, optimization,
  training, inference, evaluation, observed result, and interpretation.

## Diagrams

Use the simplest accurate representation: LaTeX for mathematical relations,
plots for quantitative data, Unicode text for tiny local structures, ASCII only
for ASCII-only environments, Mermaid for simple flow/state/sequence/dependency,
and a dedicated drawing, presentation, or design tool when complexity requires
it. Do not call Unicode box drawings ASCII.

A figure must preserve its relevant boundaries, node meaning, arrow direction,
interaction type, and abstraction level. It is not decoration; use
`references/diagrams.md` whenever a figure is created, reviewed, converted, or
material to the explanation.

## Reference routing

Read no reference mechanically. Load the smallest set whose detailed rules are
needed; ordinary focused work should use zero or one reference, while a
publication-level review may need several.

| Reference | Read when |
| --- | --- |
| `references/technical-rigor.md` | Claims, assumptions, ambiguity, causality, analogies, experiments, system semantics, or rigorous technical review. |
| `references/code-and-math.md` | Code, pseudocode, formulas, notation, complexity, or code/math consistency. |
| `references/diagrams.md` | Diagram creation, review, conversion, or tool selection. |
| `references/style-guide.md` | Substantial Markdown, typography/format review, or publication formatting. |
| `references/review-checklist.md` | Explicit full/final/publication-readiness review or comprehensive audit. |

## Review result and stopping

For substantive findings, use Critical, Major, Minor, and Optional severity.
For Critical or Major findings, give location, problematic claim/wording, why it
matters, and a concrete correction. Group repetitive formatting issues; do not
invent findings to fill categories.

For publication requests, report one verdict: Not ready, Technically sound but
needs revision, Ready after minor proofreading, or Publication-ready. Stop when
the requested scope is satisfied: technical claims are adequately supported and
scoped; code, math, figures, and prose agree; presentation is consistent; and
remaining work is optional stylistic preference.

## Final principle

Use this order:

> Claim → Evidence → Assumptions → Scope → Mechanism → Consistency → Presentation

Make it easy for readers to distinguish what is known, defined, assumed,
derived, observed, inferred, or merely intuitive, and the conditions under
which each conclusion holds.
