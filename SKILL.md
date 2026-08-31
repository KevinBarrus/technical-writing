---
name: technical-writing
description: >
  Write and review rigorous Chinese computer science technical content, including
  technical blogs, learning notes, algorithm explanations, interview write-ups,
  source-code analyses, project documentation, and engineering articles. Use this
  skill when creating, rewriting, reviewing, or polishing technical Markdown,
  especially content involving code, mathematics, complexity analysis, diagrams,
  experiments, systems, AI Agents, RAG, LLMs, deep learning, backend engineering,
  databases, operating systems, or computer networks.
---

# Technical Writing

## Purpose

Produce technical writing that is correct, rigorous, clear, consistent, and readable without unnecessarily turning engineering articles into academic papers.

The target style is:

> Technical-blog readability with paper-like rigor.

Optimize in this order:

1. Technical correctness
2. Rigor
3. Clarity
4. Consistency
5. Concision
6. Reproducibility where applicable
7. Visual quality

Do not optimize for the appearance of rigor. Optimize for actual rigor.

Preserve useful intuition, examples, teaching-oriented explanations, and the author's voice unless they reduce technical accuracy.

---

## Operating Modes

Determine the task mode before working.

### Writing Mode

Use when creating new technical content.

Before writing:

1. Identify the target audience.
2. Identify the technical scope.
3. Identify assumptions and prerequisites.
4. Determine whether code, mathematics, diagrams, experiments, or citations are needed.
5. Load the relevant reference files described in [Reference Routing](#reference-routing).

While writing:

- Prefer mechanism over vague description.
- Explain important design choices and reasoning.
- State assumptions near the conclusions that depend on them.
- Keep terminology and notation consistent.
- Use examples to improve understanding without presenting examples as proof.

### Review Mode

Use when reviewing existing technical content.

Review in this order:

1. Technical correctness
2. Specification and assumptions
3. Logical rigor
4. Terminology
5. Complexity and mathematical reasoning
6. Code and pseudocode
7. Structure
8. Diagrams and figures
9. Markdown and typography
10. Language style
11. References and reproducibility

Do not begin by polishing punctuation while substantive technical problems remain.

Use the severity system defined in `references/review-checklist.md`.

### Rewrite Mode

Use when the user asks to rewrite or polish existing content.

Preserve the original technical meaning unless:

- it is incorrect;
- it is internally inconsistent;
- it relies on an unstated assumption;
- it overstates the available evidence;
- the user explicitly asks for conceptual changes.

Do not silently change technical claims merely to make prose sound better.

If a technically meaningful change is necessary, make the change explicit.

---

## Core Rules

### 1. Correctness Before Style

NEVER sacrifice technical correctness for:

- shorter prose;
- cleaner diagrams;
- stronger rhetoric;
- prettier notation;
- more academic wording.

A technically incorrect statement is more important than dozens of formatting inconsistencies.

---

### 2. Distinguish Claim Types

When relevant, distinguish among:

- definition;
- established fact;
- assumption;
- derivation;
- experimental result;
- engineering observation;
- intuition;
- analogy;
- opinion.

Do not present one category as another.

In particular:

- an experiment does not automatically prove a general rule;
- an analogy is not a definition;
- an implementation is not necessarily the definition of a concept;
- correlation is not automatically causation;
- a local observation is not automatically a universal property.

Read `references/technical-rigor.md` when these distinctions materially affect the document.

---

### 3. State Assumptions

NEVER silently resolve meaningful ambiguity.

If a specification, sample, implementation, paper, documentation, or experiment is ambiguous or internally inconsistent:

1. identify the ambiguity;
2. state the interpretation being used;
3. state the reason for choosing it;
4. explain the consequence when another interpretation would materially change the result.

Keep assumptions close to the conclusions that depend on them.

---

### 4. Control Claim Strength

Use the weakest wording that accurately represents the available evidence.

Distinguish strengths such as:

> 可能 < 通常 < 会 < 必然

Treat words such as the following as high-risk rather than automatically forbidden:

- 一定
- 必然
- 显然
- 完全
- 永远
- 所有
- 任何
- 唯一
- 最优
- 保证
- 证明
- 显著
- 本质上
- 彻底解决

Use strong language when it is justified. Otherwise add the missing scope, assumptions, or evidence.

---

### 5. Prefer Mechanism Over Anthropomorphism

For systems, Agents, models, runtimes, databases, operating systems, and similar technical subjects, explain observable mechanisms instead of replacing them with human-like descriptions.

Prefer:

> Tool 返回失败 Observation 后，Replanner 根据当前执行状态和历史 Observation 生成新的 Plan。

over:

> Agent 发现自己做错了，于是重新思考。

Intuitive anthropomorphic descriptions may be used as secondary explanations when clearly identified as intuition.

---

### 6. Keep Analogies Bounded

Analogies are useful for teaching but MUST NOT be presented as exact equivalence unless they actually are equivalent.

Prefer:

> 可以使用 C++ 指针建立一个近似的心智模型。

over:

> Python 变量就是 C++ 指针。

When an analogy could cause a wrong mental model, state where the analogy stops applying.

---

### 7. Keep Terminology Stable

Use one term for one concept unless there is a reason to introduce an alternative term.

Keep capitalization and official names consistent.

Examples:

- Python
- PyTorch
- JavaScript
- MySQL
- GitHub
- LaTeX
- Agent
- RAG
- MCP

Define important abbreviations at first occurrence when the audience may not already know them.

Do not repeatedly redefine established terms.

---

## Complexity Analysis Protocol

When a document contains algorithmic complexity claims, do not infer complexity mechanically from visible loop nesting.

Perform the following analysis:

1. Define input-size variables.
2. Identify the operations performed.
3. State the assumed cost of relevant primitive operations.
4. Analyze loops and recursion.
5. Inspect hidden costs inside container operations and library calls.
6. Inspect comparison, hashing, sorting, copying, serialization, and canonicalization costs where relevant.
7. Distinguish average-case and worst-case behavior.
8. Analyze result space and auxiliary space separately when useful.
9. Include recursion-stack depth where relevant.
10. State assumptions near the resulting complexity claim.

Example:

For:

```python
if x not in res:
    ...
```

do not automatically conclude that the membership test is simply `O(k)` in every meaningful cost model.

If `res` is a Python `list`, locating a matching element requires a linear scan, but equality comparison between individual elements may itself have non-constant cost.

For nested `list` or `dict` values, equality comparison may recursively inspect nested contents.

A rigorous analysis may therefore state:

> 若暂时将单个元素的相等性比较视为 $O(1)$，长度为 $k$ 的列表使用线性成员查询进行稳定去重时，最坏时间复杂度为 $O(k^2)$。对于嵌套 `list` 或 `dict` 元素，相等性比较本身还可能产生额外开销。

Read `references/technical-rigor.md` and `references/code-and-math.md` for detailed rules.

---

## Optimization Claims

Do not describe a local optimization as an asymptotic improvement of the entire algorithm without analyzing the new work introduced.

For example, replacing linear duplicate detection with a hash set may require:

- checking whether elements are hashable;
- computing hashes;
- constructing canonical representations;
- recursively traversing nested values;
- sorting dictionary entries;
- allocating additional memory.

State precisely which operation becomes cheaper.

Do not mechanically write:

> 使用 `set` 后，算法从 $O(n^2)$ 优化到 $O(n)$。

unless the complete cost model supports that conclusion.

---

## Code and Mathematics

Keep natural-language typography, mathematics, and programming syntax separate.

Examples:

| Context | Preferred notation |
| --- | --- |
| Natural-language flow | `A → B → C` |
| Mathematical mapping | `$f : X \to Y$` |
| Logical implication | `$\Rightarrow$` |
| Programming syntax | `->`, `<=`, `!=`, `==` |

Use inline code for concrete program entities such as:

- `json1`
- `merge_json()`
- `copy.deepcopy()`
- `True`
- `None`
- `config.yaml`
- `src/agent/`

Do not use inline code merely to emphasize ordinary concepts such as Agent, RAG, Memory, Context, 深拷贝, or对象引用.

Use LaTeX for mathematical variables and expressions where Markdown rendering supports it.

Read `references/code-and-math.md` whenever the document contains substantial code, formulas, notation, or complexity analysis.

---

## Markdown and Typography

For Chinese technical Markdown:

- follow Chinese punctuation conventions for Chinese sentences;
- keep Chinese-English spacing consistent;
- keep Chinese-number spacing consistent;
- use correct Markdown heading and list syntax;
- use exactly one blank line between adjacent block-level elements;
- use code fences with accurate language identifiers;
- keep heading hierarchy continuous;
- do not use extra blank lines to simulate visual hierarchy.

The language of the sentence determines sentence punctuation, not the language of its final token.

Correct:

> 本文使用 Python 实现了一个 Agent。

Incorrect:

> 本文使用 Python 实现了一个 Agent.

Read `references/style-guide.md` for the complete formatting rules.

---

## Diagrams and Figures

Choose the simplest diagram representation that clearly communicates the required information.

Default escalation path:

> Unicode text diagram → Mermaid → draw.io → Figma

Use:

- LaTeX for mathematical relationships;
- plotting tools for data visualization;
- Unicode text diagrams for small object, pointer, memory, or relationship diagrams;
- ASCII only when ASCII-only compatibility is required;
- Mermaid for flows, states, sequences, pipelines, and simple dependency diagrams;
- draw.io for formal or complex architecture diagrams;
- PowerPoint for presentation-oriented diagrams and progressive reveal;
- Figma when visual design itself is important.

Do not use a higher-complexity diagramming tool merely to make a document appear more professional.

Do not call diagrams containing characters such as `┌`, `─`, `│`, or `→` ASCII diagrams. They are Unicode text diagrams.

Read `references/diagrams.md` whenever diagrams are created, selected, converted, or reviewed.

---

## Experiments and Empirical Results

When reproducibility matters, consider recording:

- model;
- dataset;
- data split;
- hardware;
- framework and version;
- batch size;
- learning rate;
- optimizer;
- epochs or steps;
- random seed;
- evaluation metric;
- baseline;
- evaluation protocol.

Do not infer causality from an uncontrolled observation.

Prefer measured values over vague adjectives such as:

- 很快
- 很强
- 很大
- 很好
- 显著提升

unless those terms are explicitly defined or justified.

Distinguish percentage-point change from relative percentage change.

---

## Domain-Specific Guidance

### Algorithms

Prefer the structure:

1. Problem
2. Constraints and assumptions
3. Brute-force approach
4. Key observation
5. Optimized approach
6. Invariant or correctness reasoning
7. Implementation
8. Complexity
9. Edge cases
10. Tests
11. Further optimization where useful

Explain why an algorithmic technique applies instead of presenting only the final implementation.

### Backend and Systems

Distinguish among:

- language semantics;
- runtime behavior;
- operating-system behavior;
- network behavior;
- framework behavior;
- implementation-specific behavior.

State relevant environmental assumptions when they affect conclusions.

### AI Agents and LLM Systems

Prefer operational definitions for terms such as:

- Agent
- Memory
- Context
- Planning
- Reflection
- Reasoning
- Tool
- Observation

Do not let anthropomorphic terminology replace system mechanisms.

### Deep Learning and Experimental ML

Separate:

- architecture;
- objective;
- optimization;
- training procedure;
- evaluation;
- observed results;
- interpretation.

Do not infer general causal conclusions from a single uncontrolled experiment.

---

## Reference Routing

Do not load every reference file mechanically.

Load only the files relevant to the current task.

### `references/style-guide.md`

Read when:

- writing or reviewing Markdown;
- checking punctuation or spacing;
- checking headings, lists, block spacing, units, symbols, or inline-code formatting;
- performing final publication proofreading.

### `references/technical-rigor.md`

Read when:

- reviewing technical claims;
- checking assumptions;
- analyzing causality;
- reviewing complexity;
- evaluating analogies;
- reviewing experiments;
- handling specification ambiguity;
- reviewing algorithms, systems, Agents, or ML explanations.

### `references/code-and-math.md`

Read when:

- the document contains code;
- the document contains pseudocode;
- mathematical notation is used;
- complexity is analyzed;
- code fences or language identifiers need review;
- natural-language, mathematical, and programming symbols need disambiguation.

### `references/diagrams.md`

Read when:

- creating a diagram;
- reviewing a diagram;
- choosing between ASCII, Unicode, Mermaid, draw.io, PowerPoint, Figma, plotting tools, or LaTeX;
- converting one diagram format into another;
- deciding whether an existing diagram has become too complex for its current representation.

### `references/review-checklist.md`

Read when:

- performing a full-document review;
- performing publication-readiness review;
- the user asks whether a document is finished;
- assigning issue severity;
- deciding whether further polishing is useful.

---

## Review Output

For a full review, organize findings by severity rather than presenting every issue as equally important.

Use:

### Critical

Technical errors that can invalidate the implementation, explanation, experiment, or conclusion.

### Major

Material problems involving assumptions, reasoning, complexity, terminology, contradictions, or misleading explanations.

### Minor

Formatting, Markdown, punctuation, notation, terminology consistency, or localized wording issues.

### Optional

Improvements that are stylistic and do not materially affect correctness or clarity.

For each substantive issue, prefer providing:

1. the original wording or location;
2. what is wrong;
3. why it matters;
4. a concrete replacement or correction.

Do not manufacture issues merely to make the review appear thorough.

Read `references/review-checklist.md` for the full review protocol.

---

## Stop Condition

Technical writing can be polished indefinitely.

Do not encourage endless revision once the document is already fit for its purpose.

A document may be considered publication-ready when:

- no known material technical errors remain;
- important assumptions and scope are explicit;
- reasoning supports the stated conclusions;
- complexity claims have appropriate assumptions;
- terminology and notation are consistent;
- code and examples agree with the explanation;
- diagrams are readable and semantically correct;
- Markdown and typography are consistently formatted;
- no important reproducibility or citation requirement remains unmet.

Once these conditions are satisfied, report:

> Publication-ready.

Do not continue inventing low-value stylistic changes unless the user explicitly requests further polishing.

---

## Final Principle

Rigorous technical writing makes it easy for the reader to determine:

- what is known;
- what is assumed;
- what is defined;
- what is derived;
- what is observed;
- what is only an intuition or analogy;
- under what conditions a conclusion holds;
- where that conclusion stops applying.

Formatting, diagrams, mathematics, and terminology exist to make this reasoning easier to inspect.

They are not substitutes for it.