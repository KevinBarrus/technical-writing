# Technical Writing Skill

[中文](README.md)

A Skill for writing, rewriting, and reviewing technical content. It is suitable
for technical blogs, learning notes, algorithm explanations, source-code
analyses, project documentation, and interview write-ups. It covers code,
mathematics, complexity, diagrams, experiments, and systems.

## Installation

Run the following command to install this repository into Codex's personal
Skills directory:

```bash
git clone https://github.com/KevinBarrus/technical-writing.git \
  ~/.codex/skills/technical-writing
```

Start a new Codex session to use the Skill. To update an existing installation:

```bash
git -C ~/.codex/skills/technical-writing pull --ff-only
```

If the destination already exists, update it instead of cloning it again.

For Claude Code, install it in the Claude Skills directory:

```bash
git clone https://github.com/KevinBarrus/technical-writing.git \
  ~/.claude/skills/technical-writing
```

The same layout applies to Pi, Hermes, and OpenCode. To make the Skill
available to all agents, install it in the shared directory:

```bash
git clone https://github.com/KevinBarrus/technical-writing.git \
  ~/.agents/skills/technical-writing
```

## What It Solves

The Skill aims for technical-blog readability with paper-like rigor. Its
priorities are:

> Correctness → Rigor → Clarity → Consistency → Concision → Presentation

It separates claims, evidence, assumptions, scope, and mechanisms. This avoids
treating experiments as proof, implementations as definitions, analogies as
equivalence, or incomplete cost models as complexity conclusions.

## Use Cases

- Write or rewrite technical Markdown.
- Review algorithms, source code, system design, databases/networks, Agent/RAG,
  or machine-learning content.
- Check that code, formulas, complexity analysis, experimental conclusions,
  diagrams, and prose agree.
- Run a publication review and report findings as Critical, Major, Minor, or
  Optional.

For sentence polishing, local formatting, or a single code fragment, the Skill
uses local review. It performs a full review only when explicitly requested.

## How It Works

[`SKILL.md`](SKILL.md) defines Writing, Rewrite, and Review modes, as well as
Local, Technical, and Publication review depth. It loads reference material only
when the task requires it.

| File | Purpose |
| --- | --- |
| [`technical-rigor.md`](references/technical-rigor.md) | Claims, evidence, assumptions, causality, system semantics, and reproducibility. |
| [`code-and-math.md`](references/code-and-math.md) | Code, pseudocode, formulas, numerical reasoning, and complexity. |
| [`diagrams.md`](references/diagrams.md) | Diagram selection, semantics, readability, and review. |
| [`style-guide.md`](references/style-guide.md) | Chinese technical Markdown, typography, and formatting. |
| [`review-checklist.md`](references/review-checklist.md) | Full-document review, severity, and publication decisions. |

## Example Requests

```text
Review this RAG article for technical correctness, focusing on the definitions
of Context and Memory and the retrieval flow.
```

```text
Polish this algorithm explanation without changing its conclusion, and check
whether its complexity analysis omits hashing or comparison costs.
```

```text
Perform a publication-readiness review of this project documentation and provide
directly usable revisions grouped by severity.
```

## Design Principles

- Do not use formatting to conceal technical problems.
- Do not replace risk-based review with an indiscriminate checklist.
- Do not add formalism, diagrams, or experiments merely to look rigorous.
- Make mechanisms, conditions, and evidence boundaries inspectable.
