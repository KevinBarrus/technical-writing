# Technical Rigor Guide

## Core test

For each important statement, let a reader identify: what is claimed, whether
it is a definition/fact/specification/assumption/derivation/observation/
analogy/opinion, what supports it, its scope, and what would change the
conclusion. Optimize for actual rigor, not academic-sounding language.

## Claims, evidence, and scope

- A **definition** states local or established meaning; label project-local
  definitions. A **specification** states required behavior; current code may
  violate it. An **established fact** needs an authoritative source, standard,
  source code, theorem, or reproducible implementation evidence.
- Do not present one implementation as the definition of an abstraction, or
  infer a universal semantic guarantee from current implementation behavior.
- An **assumption** is a condition accepted for analysis. State material
  assumptions near the conclusion; do not silently resolve a conflict between a
  prompt, sample, documentation, paper, API, or implementation.
- A **derivation** follows stated premises. Replace “显然”“易知” and similar
  rhetoric with the missing logical step when it matters.
- An **experimental result** or **engineering observation** is limited to its
  configuration, environment, input, metric, and time. It is not automatically
  a general rule, a proof, or a causal conclusion.
- An **analogy** or **intuition** is a teaching aid. Mark it as approximate and
  state the boundary when it could produce a wrong mental model.

Use the weakest accurate wording. Treat universal, absolute, or evaluative
words—“一定”“必然”“所有”“任何”“唯一”“最优”“保证”“证明”“显著”“完全”“从不”
—as prompts to provide a theorem/specification/evidence and scope, or weaken
the language. Name relevant language and version, runtime, framework, OS,
database, deployment, hardware, dataset, model, benchmark, input distribution,
concurrency model, network condition, and experiment configuration.

## Reasoning discipline

Separate correlation from causation, necessary from sufficient conditions,
local from global optimality, and mitigation from resolution. Explain mechanism
before recommendation; identify trade-offs, failure modes, edge cases, negative
claims, and counterexamples that materially constrain the result. Keep a stable
term for each concept, avoid ambiguous pronouns, and give each sentence one
main claim when possible.

Examples and tests demonstrate behavior; they do not prove universal
correctness without coverage or a separate proof. For algorithms, state the
invariant or other correctness argument. For complexity, use the cost-model and
hidden-cost protocol in `code-and-math.md`.

## Domain-specific boundaries

| Domain | Distinctions that must remain visible |
| --- | --- |
| Language/runtime | Language semantics, documented API contract, current implementation, and version-specific behavior. |
| Backend/distributed systems | Process, thread, transaction, storage, cache, queue, consistency, timeout, retry, failure, and deployment boundaries. |
| Database | Logical query intent, engine/version, index and execution plan, isolation/locking, data distribution, and measured behavior. |
| Networks | Application/protocol semantics, transport behavior, ordering, reliability, timeout, retry, congestion, and topology. |
| Agents/LLMs | Operational definitions of Agent, context, memory, plan, tool, observation, and reasoning; model output is not hidden human-like deliberation. |
| RAG | Ingestion/indexing and online retrieval/generation paths; retrieval quality, context construction, grounding, and evaluation are separate concerns. |
| Deep learning | Architecture, objective, optimizer, training procedure, evaluation protocol, result, and interpretation. |

For security and reliability claims, specify the threat/failure model and the
guarantee boundary. Never call a measure “safe”, “reliable”, or “solved” without
the conditions and residual risk.

## Evidence and reproducibility

Prefer primary sources: standards, official documentation, source code,
original papers, datasets, and reproducible experiments. State source conflicts
instead of silently choosing a convenient one. For empirical claims, retain the
data split, baseline, metric, configuration, random seed where applicable, and
enough version information to reproduce or qualify the observation.

## Review prompts

- Does every central claim have the right category, evidence, strength, and
  scope?
- Is an assumption, ambiguity, version dependency, or implementation detail
  carrying an unstated conclusion?
- Does the mechanism support the recommendation and exclude material failure
  modes or counterexamples?
- Are a benchmark, test, observation, analogy, or implementation being
  overstated as proof, causation, definition, or universal behavior?
- Can a reader reproduce the material result or locate its authoritative source?
