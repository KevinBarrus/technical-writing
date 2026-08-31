# Technical Writing Style Guide

## Purpose

Define the typography, Markdown, punctuation, spacing, naming, and formatting conventions used in Chinese computer science technical writing.

This guide primarily targets:

- Chinese technical blogs
- learning notes
- algorithm explanations
- interview write-ups
- project documentation
- source-code analyses
- engineering articles written in Markdown

The goal is consistency and readability rather than imitation of academic typesetting.

When a publishing platform imposes incompatible formatting constraints, preserve semantic correctness first and adapt presentation second.

---

# 1. General Principles

Apply the following priorities:

1. Semantic correctness
2. Readability
3. Consistency
4. Typographic quality

Do not sacrifice technical meaning merely to satisfy a visual formatting rule.

Apply the same convention consistently throughout one document.

Do not alternate between multiple equivalent styles without a reason.

---

# 2. Chinese and English Punctuation

## 2.1 Sentence Language Determines Punctuation

The language of the sentence determines sentence-level punctuation.

Chinese sentence:

> 本文使用 Python 实现了一个 Agent。

Do not write:

> 本文使用 Python 实现了一个 Agent.

English sentence:

> ReAct interleaves reasoning and acting.

Do not determine punctuation based only on the final token.

For example:

> 调用 `merge_json()` 后即可得到结果。

The sentence is Chinese, so the final period is `。`.

---

## 2.2 Chinese Punctuation

Use full-width Chinese punctuation in Chinese prose:

- `，`
- `。`
- `：`
- `；`
- `？`
- `！`
- `、`
- `（）`
- `“”`
- `……`
- `——`

Examples:

> 首先读取配置，然后初始化 Agent。

> 这里需要考虑三个问题：时间复杂度、空间复杂度和边界条件。

Do not insert spaces before Chinese punctuation.

Correct:

> 使用 Python，实现该算法。

Incorrect:

> 使用 Python ，实现该算法。

---

## 2.3 English Punctuation

Use half-width punctuation in English prose.

Example:

> The runtime contains a planner, an executor, and a tool registry.

Normally place one space after English commas, colons, semicolons, and sentence-ending punctuation when another token follows.

---

## 2.4 Colon

Chinese sentence:

> 主要包含三个模块：Planner、Executor 和 Memory。

Do not write:

> 主要包含三个模块: Planner、Executor 和 Memory。

English sentence:

> The system contains three modules: Planner, Executor, and Memory.

---

## 2.5 Enumeration

Use `、` for ordinary enumeration in Chinese prose:

> 系统包含 Planner、Executor、Memory 和 Tool Registry。

For English prose, use commas and conjunctions:

> Planner, Executor, Memory, and Tool Registry

Do not use `/` or `\` as replacements for Chinese `、`.

---

# 3. Chinese-English Spacing

## 3.1 Chinese and English

Normally insert one half-width space between Chinese text and English words.

Correct:

> 使用 Python 实现。

> Agent 可以调用 Tool。

> 本文介绍 RAG 的基本原理。

Avoid:

> 使用Python实现。

> Agent可以调用Tool。

---

## 3.2 Chinese and Numbers

Normally insert one half-width space between Chinese text and Arabic numerals.

Correct:

> 共进行了 10 次实验。

> 使用 3 个 Agent。

Avoid:

> 共进行了10次实验。

---

## 3.3 Exceptions

Do not mechanically insert spaces where established syntax or typography requires otherwise.

Examples:

> Python 3.13

> GPT-5

> IPv4

> UTF-8

> 92.3%

> `list[int]`

> `config.yaml`

Code syntax must remain unchanged.

---

# 4. Inline Code

## 4.1 What Should Use Inline Code

Use backticks for concrete program entities.

Examples include:

### Variables

> `json1`

> `res`

> `key`

### Functions and Methods

> `merge_json()`

> `copy.deepcopy()`

> `append()`

### Classes and Types

When referring to the concrete programming-language entity:

> `dict`

> `list`

> `bool`

> `AgentExecutor`

### Literals

> `True`

> `False`

> `None`

### Expressions

> `a is b`

> `x not in res`

> `b[0] = [100]`

### Files and Paths

> `config.yaml`

> `README.md`

> `src/agent/`

> `~/.agents/skills/`

### Commands

> `git status`

> `python main.py`

### Parameters, Attributes, Environment Variables, and Endpoints

Use inline code when referring to their literal program representation.

---

## 4.2 What Should Not Use Inline Code

Do not use backticks merely for emphasis.

Normally do not write:

> `Agent`

> `RAG`

> `Memory`

> `Context`

> `深拷贝`

> `浅拷贝`

when they are ordinary technical concepts rather than literal program identifiers.

Prefer:

> Agent 使用 Memory 保存跨会话信息。

Use bold or sentence structure for semantic emphasis when emphasis is genuinely needed.

---

## 4.3 Inline Code Adjacent to Chinese

Treat inline code as a technical token and keep surrounding Chinese prose readable.

Prefer:

> 调用 `forward()` 方法。

> 修改 `config.yaml` 文件。

> `copy.deepcopy(a)` 会递归处理对象图。

Do not write:

> 调用`forward()`方法。

Maintain the same Chinese-English spacing rhythm used for ordinary English technical terms.

---

# 5. Bold and Emphasis

Use bold sparingly.

Bold should indicate genuinely important concepts, conclusions, warnings, or distinctions.

Do not bold every technical term.

Do not use inline code as a substitute for bold.

Avoid excessive patterns such as:

> **第一步**……**第二步**……**第三步**……

unless the visual hierarchy materially improves comprehension.

When a complete Chinese sentence contains a bold phrase, normally keep sentence punctuation outside the bold span.

Prefer:

> 这里的关键是**对象共享关系**。

rather than:

> 这里的关键是**对象共享关系。**

Exceptions are acceptable when the punctuation semantically belongs to the emphasized quotation or content.

---

# 6. Parentheses and Quotation Marks

## 6.1 Chinese Parentheses

Use Chinese full-width parentheses in Chinese prose:

> 强化学习（Reinforcement Learning, RL）

> 检索增强生成（Retrieval-Augmented Generation, RAG）

Do not normally write:

> 强化学习 (Reinforcement Learning, RL)

when the surrounding sentence is Chinese prose.

---

## 6.2 Programming Syntax

Do not replace programming parentheses with Chinese parentheses.

Correct:

> `merge_json(a, b)`

Incorrect:

> `merge_json（a, b）`

---

## 6.3 Quotation Marks

Use Chinese quotation marks in Chinese prose:

> 这里的“引用”并不等同于 C++ 引用类型。

Use quotation marks for quoted language or explicitly discussed terminology, not as a generic emphasis mechanism.

For literal code strings, use inline code when appropriate:

> 字符串 `"hello"`

---

# 7. Headings

## 7.1 Heading Hierarchy

Use a continuous heading hierarchy.

Example:

```markdown
# Title

## 1. Agent Runtime

### 1.1 Agent Loop

#### 1.1.1 Tool Execution
```

Do not skip directly from H2 to H4.

Use one H1 for a standalone article when the publishing environment permits it.

---

## 7.2 Heading Punctuation

Do not end headings with sentence-ending punctuation.

Correct:

```markdown
### 3.1 Context Management
```

Avoid:

```markdown
### 3.1 Context Management。
```

Question marks may be retained when the heading is intentionally written as a question:

```markdown
### 为什么浅拷贝会影响原对象？
```

Prefer descriptive technical headings for formal technical articles when possible.

---

## 7.3 Numbered Headings

For paper-style hierarchical numbering, prefer:

```text
3. Agent Runtime
3.1 Context Management
3.2 Tool Runtime
```

Do not write:

```text
3.1Context Management
```

For hierarchical section numbering, normally prefer:

```text
3.1 Context Management
```

rather than:

```text
3.1. Context Management
```

Do not mix multiple numbering systems without a reason.

Avoid combining styles such as:

```text
一、
1、
（1）
①
```

within the same hierarchy.

---

# 8. Block Spacing

Use exactly one blank line between adjacent block-level Markdown elements.

This applies to:

- heading ↔ heading
- heading ↔ paragraph
- paragraph ↔ heading
- paragraph ↔ code block
- paragraph ↔ equation
- paragraph ↔ table
- paragraph ↔ image
- code block ↔ paragraph
- table ↔ paragraph

Example:

```markdown
## 3. Agent Runtime

### 3.1 Agent Loop

Agent Loop 负责……

### 3.2 Context Management

Context Management 负责……
```

Do not use multiple blank lines to express section hierarchy.

Incorrect:

```markdown
## 3. Agent Runtime



### 3.1 Agent Loop
```

Visual hierarchy should normally be handled by the renderer or stylesheet, not by adding blank lines to the Markdown source.

---

# 9. Lists

## 9.1 Unordered Lists

Use one space after the marker:

```markdown
- Planner
- Executor
- Memory
```

Not:

```markdown
-Planner
-Executor
```

---

## 9.2 Ordered Lists

Use:

```markdown
1. 第一项
2. 第二项
3. 第三项
```

Not:

```markdown
1.第一项
2.第二项
```

---

## 9.3 List Punctuation

For short phrase-style items, sentence-ending punctuation is usually unnecessary:

```markdown
- Planner
- Executor
- Tool Registry
```

For complete sentences, use punctuation consistently:

```markdown
- Planner 负责生成执行计划。
- Executor 负责执行具体步骤。
- Replanner 根据 Observation 更新计划。
```

Do not randomly mix punctuated and unpunctuated items of the same grammatical form.

---

## 9.4 Blank Lines Inside Lists

Simple lists normally do not need blank lines between items.

Use blank lines when list items contain multiple paragraphs, code blocks, or other complex block content.

---

# 10. Arrows

## 10.1 Natural-Language Flow

Use Unicode arrows for conceptual flows, mappings, and state transitions in prose and Unicode text diagrams.

Prefer:

> User → Planner → Executor → Tool

> `PENDING` → `RUNNING` → `SUCCESS`

Use spaces around arrows in inline conceptual flows.

Avoid:

> User→Planner→Executor

---

## 10.2 Programming Syntax

Preserve programming-language syntax.

Examples:

```cpp
node->next
```

```python
def f(x: int) -> str:
    ...
```

Do not replace programming `->` with `→`.

---

## 10.3 Logical Implication

Do not use `→` and `⇒` interchangeably when the distinction matters.

Use:

- `→` for flow, mapping, transition, or directional relation
- `⇒` for logical implication

In mathematical expressions, prefer LaTeX forms such as `\to` and `\Rightarrow`.

---

# 11. Hyphen, En Dash, and Dash

## 11.1 Hyphen `-`

Use the ASCII hyphen for:

- programming syntax
- compound technical names where convention requires it
- command-line options
- Markdown syntax

Examples:

> UTF-8

> `--help`

---

## 11.2 En Dash `–`

Use an en dash for numeric and temporal ranges in prose.

Examples:

> 10–20 ms

> 2024–2026

> 第 3–5 节

Do not normally use `~` for formal ranges.

Avoid:

> 10~20 ms

---

## 11.3 Dash in Prose

Use punctuation according to the language of the sentence.

English prose may use an em dash `—`.

Chinese prose may use the Chinese double em dash:

> 这里存在一个关键问题——对象共享。

Do not mix dash conventions arbitrarily within the same prose style.

---

# 12. Slash and Backslash

## 12.1 Slash `/`

Use `/` for established combinations or technical syntax.

Examples:

> TCP/IP

> input/output

> client/server

> `/usr/local/bin`

Do not use `/` as a generic replacement for:

- `、`
- `和`
- `或`

when ordinary prose is clearer.

Prefer:

> Planner、Executor 和 Memory

rather than:

> Planner/Executor/Memory

unless the slash has an intentional semantic meaning.

---

## 12.2 Backslash `\`

Use backslash only where the syntax requires it.

Examples:

> Windows path syntax

> escape sequences

> LaTeX commands

Do not use `\` as an enumeration separator.

---

# 13. Other Symbols

## 13.1 Multiplication and Dimensions

Use `×` for human-readable dimensions:

> 1920 × 1080

Use `*` only when required by programming syntax or a specific notation.

---

## 13.2 Comparison Operators

In mathematical prose, prefer LaTeX:

> $x \le y$

> $a \neq b$

In code, preserve:

```python
x <= y
a != b
```

Do not beautify code operators into mathematical Unicode symbols.

---

## 13.3 Equality

Distinguish:

- mathematical equality: `=`
- programming comparison: language-specific operators such as `==`
- definition: use prose or `:=` only when the notation is explicitly defined and appropriate

Do not use these interchangeably.

---

## 13.4 Vertical Bar

Do not use `|` as a generic prose separator.

Valid uses include:

- Markdown tables
- mathematical notation such as conditional probability
- programming syntax
- shell pipelines

---

## 13.5 Ampersand

Do not replace ordinary Chinese `和` or English `and` with `&` unless:

- it is part of an official name
- the notation is conventional
- the context is deliberately compact

---

## 13.6 Plus Sign

Do not use `+` as a universal substitute for natural-language relationships.

For example:

> RAG = Retriever + LLM

may be useful as an explicitly labeled intuition, but it is usually not a rigorous definition.

---

# 14. Ellipsis

Use Chinese ellipsis in Chinese prose:

> 等等……

Use three ASCII periods in English prose when an ellipsis is appropriate:

> and so on...

In mathematical notation, prefer LaTeX commands such as:

> `\ldots`

Do not mix these conventions without reason.

---

# 15. Numbers, Units, and Percentages

## 15.1 Units

Normally place one space between a number and a unit symbol or abbreviation:

> 10 ms

> 32 GB

> 2.4 GHz

> 7.5 GB/s

Follow domain-specific conventions when they differ.

---

## 15.2 Percentages

Do not insert a space before `%`:

> 92.3%

Not:

> 92.3 %

---

## 15.3 Precision

Use consistent numeric precision when values are directly compared.

Prefer:

```markdown
| Method | Accuracy |
| --- | ---: |
| A | 82.1% |
| B | 84.7% |
```

Avoid unnecessary mixtures such as:

```markdown
| Method | Accuracy |
| --- | ---: |
| A | 82% |
| B | 84.7321% |
```

unless the underlying data or reporting convention justifies the difference.

---

## 15.4 Percentage Points

Distinguish absolute percentage-point changes from relative percentage changes.

If accuracy changes from 80% to 84%:

- absolute increase: 4 percentage points
- relative increase: 5%

Do not describe both simply as:

> 提高了 4%

---

# 16. Code Fences

Use fenced code blocks for multiline code.

Always use the language identifier that matches the actual content when one exists.

Examples:

```python
def hello():
    print("hello")
```

```cpp
int main() {
    return 0;
}
```

```json
{
    "name": "Agent"
}
```

```text
User → Agent → Tool
```

Do not label Python assignments as JSON.

Incorrect:

```json
a = {"x": 1}
```

Use:

```python
a = {"x": 1}
```

Use `text` for conceptual diagrams and plain non-language-specific output when appropriate.

Detailed code and pseudocode rules are defined in `code-and-math.md`.

---

# 17. Tables

Use tables when readers need to compare values or properties across the same dimensions.

Do not use a table merely to place unrelated text side by side.

Keep column semantics consistent.

Align numeric columns to the right when useful:

```markdown
| Method | Accuracy | Latency |
| --- | ---: | ---: |
| A | 82.1% | 120 ms |
| B | 84.7% | 95 ms |
```

Keep units and precision consistent within the same comparison.

Avoid extremely wide tables when prose or multiple smaller tables would be easier to read.

---

# 18. Figures and Tables in Prose

For formal technical articles, number important figures and tables consistently.

Examples:

> 图 1：Agent Runtime 架构

> 表 2：不同检索方法的评测结果

Refer to numbered figures and tables explicitly:

> 如图 1 所示……

Prefer this over ambiguous references such as:

> 如下图所示……

when the document contains multiple figures.

Detailed figure-format selection belongs to `diagrams.md`.

---

# 19. Links

Prefer descriptive link text over naked URLs in prose.

Prefer:

> 参见 Python 官方文档。

over inserting a long raw URL directly into the sentence.

When the publishing platform or task explicitly requires raw URLs, follow that requirement.

Do not use vague anchor text such as:

> 点击这里

when a descriptive label is available.

---

# 20. Naming Consistency

Preserve official capitalization and spelling.

Examples:

Correct:

> GitHub

> JavaScript

> TypeScript

> PyTorch

> MySQL

> PostgreSQL

> LaTeX

Avoid inconsistent variants such as:

> Github

> Javascript

> Pytorch

within the same article.

When a project defines its own official spelling, follow the project's spelling.

---

# 21. Abbreviations

At first occurrence, define abbreviations when the target audience may not know them.

Example:

> Retrieval-Augmented Generation (RAG)

Subsequent occurrences may use:

> RAG

Do not repeatedly expand the same abbreviation unless needed for a new context.

For a primarily Chinese article, either of the following may be appropriate depending on context:

> 检索增强生成（Retrieval-Augmented Generation, RAG）

or:

> Retrieval-Augmented Generation (RAG)

Choose one style and remain consistent.

---

# 22. Paragraph Style

Prefer one main claim per sentence.

Prefer one coherent idea per paragraph.

Avoid excessively long sentences containing multiple independent technical claims.

When a sentence contains several conditions, consequences, exceptions, and implementation details, consider splitting it.

Do not fragment every sentence into its own paragraph merely to create visual whitespace.

Technical prose should remain cohesive.

---

# 23. Formality

The target is rigorous technical writing, not bureaucratic or artificially academic prose.

Teaching-oriented expressions are allowed.

Examples, intuition, questions, and mental models are useful when they improve comprehension.

Prefer:

> 为什么这里不能直接使用浅拷贝？

when it naturally introduces an explanation.

Do not replace every readable phrase with abstract academic terminology merely to sound formal.

At the same time, avoid unnecessarily conversational headings such as:

> `deepcopy` 到底干了啥？

when:

> `deepcopy` 的递归复制机制

communicates the same idea more precisely.

---

# 24. High-Risk Formatting Patterns

During review, explicitly check for:

- Chinese sentences ending with English punctuation
- missing Chinese-English spaces
- missing Chinese-number spaces
- spaces before Chinese punctuation
- inconsistent inline-code usage
- code identifiers without backticks in prose
- ordinary concepts unnecessarily wrapped in backticks
- inconsistent heading numbering
- skipped heading levels
- multiple blank lines between blocks
- `1.Item` instead of `1. Item`
- `#Title` instead of `# Title`
- mixed `->` and `→` in conceptual diagrams
- `~` used for formal ranges
- incorrect code-fence language tags
- inconsistent units or numeric precision
- accidental mixtures of ASCII and Unicode notation

Do not report these issues before more important technical errors during a full technical review.

---

# 25. Final Style Checklist

Before declaring formatting complete, verify:

## Punctuation

- [ ] Chinese sentences use Chinese punctuation.
- [ ] English sentences use English punctuation.
- [ ] Chinese colons and parentheses are used consistently.
- [ ] No unnecessary spaces appear before Chinese punctuation.

## Spacing

- [ ] Chinese-English spacing is consistent.
- [ ] Chinese-number spacing is consistent.
- [ ] Number-unit spacing is consistent.
- [ ] Percentages use no space before `%`.

## Inline Code

- [ ] Variables, functions, methods, literal code expressions, filenames, paths, and commands use inline code where appropriate.
- [ ] Ordinary concepts are not wrapped in backticks merely for emphasis.
- [ ] Inline code integrates cleanly with surrounding Chinese prose.

## Headings and Blocks

- [ ] Heading hierarchy is continuous.
- [ ] Heading numbering is consistent.
- [ ] Headings normally do not end in punctuation.
- [ ] Adjacent block elements have exactly one blank line.
- [ ] Extra blank lines are not used to create hierarchy.

## Lists

- [ ] Markdown markers are followed by one space.
- [ ] Similar list items use consistent punctuation.
- [ ] Simple lists do not contain unnecessary blank lines.

## Symbols

- [ ] Conceptual flows use `→`.
- [ ] Programming syntax preserves `->` where required.
- [ ] Logical implication is distinguished from flow.
- [ ] Numeric ranges use `–` where appropriate.
- [ ] `/`, `\`, `|`, `&`, and `+` are not being used as arbitrary prose separators.

## Code Blocks

- [ ] Every fenced code block uses the correct language identifier.
- [ ] Conceptual text diagrams use `text`.
- [ ] JSON fences contain actual JSON rather than Python or JavaScript assignments.

## Numbers

- [ ] Units are formatted consistently.
- [ ] Numeric precision is consistent where comparison matters.
- [ ] Percentage points and relative percentages are distinguished.

---

# Core Principle

Formatting rules exist to reduce ambiguity and make technical reasoning easier to inspect.

Consistency is more important than ornamental typography.

When a style rule conflicts with technical correctness, code syntax, mathematical meaning, an official project name, or a publishing-platform requirement, preserve the underlying semantics first.