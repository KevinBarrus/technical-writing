# Code and Math Style Guide

## Purpose

Define how code, pseudocode, mathematical notation, formulas, complexity expressions, and technical symbols should be written in computer science technical content.

This guide focuses on the boundary between three different notation systems:

1. natural-language technical prose
2. mathematics
3. programming syntax

These systems may express similar ideas, but they MUST NOT be mixed mechanically.

The goal is to preserve:

- semantic correctness
- syntactic correctness
- mathematical precision
- visual consistency
- readability

---

# 1. Core Principle

Use the notation system that belongs to the semantic context.

Do not beautify programming syntax into mathematical notation.

Do not write mathematical expressions using programming operators when LaTeX is available.

Do not use ASCII programming symbols as generic prose symbols when clearer typographic symbols exist.

A useful distinction is:

| Context | Preferred notation |
| --- | --- |
| Natural-language flow | `A → B → C` |
| Mathematical mapping | `$f : X \to Y$` |
| Logical implication | `$A \Rightarrow B$` |
| Programming return annotation | `->` |
| Programming comparison | `<=`, `>=`, `!=`, `==` |
| Mathematical comparison | `\le`, `\ge`, `\neq`, `=` |

---

# 2. Inline Code

Use inline code for literal programming entities.

Examples include:

- variables: `a`, `json1`, `res`
- functions: `merge_json()`
- methods: `append()`
- classes: `AgentExecutor`
- attributes: `node.next`
- parameters: `temperature`
- literals: `True`, `False`, `None`
- expressions: `x not in res`
- filenames: `config.yaml`
- paths: `src/agent/`
- commands: `git status`
- environment variables: `OPENAI_API_KEY`
- API routes: `/v1/chat/completions`

Do not use inline code merely to emphasize ordinary technical concepts.

Correct:

> `deepcopy()` 会递归处理对象图。

Correct:

> 深拷贝用于避免共享嵌套可变对象。

Avoid:

> `深拷贝` 用于避免共享嵌套可变对象。

unless `深拷贝` is literally an identifier in the discussed program.

---

# 3. Code Syntax Must Remain Exact

Never replace actual programming syntax with visually similar Unicode symbols.

Incorrect:

```python
if x ≤ y:
    ...
```

Correct:

```python
if x <= y:
    ...
```

Incorrect:

```cpp
node→next
```

Correct:

```cpp
node->next
```

Incorrect:

```python
def f(x: int) → str:
    ...
```

Correct:

```python
def f(x: int) -> str:
    ...
```

Programming syntax is governed by the language grammar, not by typographic preference.

---

# 4. Code Fences

Use fenced code blocks for multiline code.

Always use the language identifier that matches the actual content when one exists.

Common identifiers include:

- `python`
- `cpp`
- `java`
- `go`
- `javascript`
- `typescript`
- `rust`
- `bash`
- `shell`
- `sql`
- `json`
- `yaml`
- `toml`
- `html`
- `css`
- `text`

Example:

```python
def merge_json(a, b):
    return a
```

For C++:

```cpp
int main() {
    return 0;
}
```

Use `cpp`, not labels such as:

```text
C++
```

as the fence language identifier.

---

# 5. Code Fence Content Must Match the Language

Do not label content as JSON when it contains non-JSON syntax.

Incorrect:

```json
json1 = {"a": 1}
```

This is assignment syntax and is not valid JSON.

Use:

```python
json1 = {"a": 1}
```

Actual JSON:

```json
{
  "a": 1
}
```

Likewise, distinguish among:

- JSON
- JavaScript object literals
- Python dictionaries
- YAML
- shell output
- pseudocode

Do not choose a language tag merely because the data “looks similar”.

---

# 6. Runnable Code vs Pseudocode

Clearly distinguish runnable code from pseudocode.

Runnable code should:

- follow the actual language syntax
- use valid identifiers
- use correct imports where needed
- avoid undefined helper functions unless they are explained
- match the behavior described in the prose

Pseudocode may simplify implementation details, but MUST be labeled as pseudocode.

Example:

```text
function MERGE(a, b):
    if both are dictionaries:
        recursively merge matching keys
    otherwise:
        apply type-specific rule
```

Do not present pseudocode as valid Python, C++, Java, or another language.

---

# 7. Conceptual Code Fragments

Small fragments may omit surrounding boilerplate when the omitted context is obvious.

Example:

```python
if x not in res:
    res.append(x)
```

This is acceptable when explaining one operation.

However, do not imply that an incomplete fragment is a complete runnable solution.

Use wording such as:

> 核心逻辑如下：

or:

> 省略输入输出和异常处理后，关键部分如下：

when necessary.

---

# 8. Code and Prose Must Agree

Review whether:

- variable names in prose match the code
- function names match the implementation
- described branches actually exist
- claimed return values match the code
- examples match actual execution
- edge-case behavior matches implementation
- complexity analysis matches the implementation being shown

Do not describe one algorithm and publish code implementing another.

---

# 9. Comments in Code

Comments should explain intent, constraints, or non-obvious reasoning.

Prefer:

```python
# bool 是 int 的子类，因此必须先处理 bool
if isinstance(a, bool) and isinstance(b, bool):
    ...
```

Avoid comments that merely repeat syntax:

```python
# 判断 a 是否为 bool
if isinstance(a, bool):
    ...
```

Use comments for:

- why
- assumptions
- invariants
- non-obvious edge cases
- implementation trade-offs

not for narrating every line.

---

# 10. Code Formatting

Follow the conventional formatter and style guide of the language when practical.

Examples:

- Python: PEP 8 / formatter conventions
- Go: `gofmt`
- Rust: `rustfmt`
- JavaScript/TypeScript: project formatter
- C++: project style or formatter

Do not manually alter code indentation or spacing merely to match surrounding prose typography.

Code formatting and prose formatting are separate concerns.

---

# 11. Mathematical Variables

Use LaTeX for mathematical variables when Markdown rendering supports it.

Prefer:

> 假设总节点数为 $N$，最大嵌套深度为 $D$。

Avoid:

> 假设总节点数为 N，最大嵌套深度为 D。

Use the same symbol consistently throughout one derivation.

Do not switch between:

- $N$
- $n$
- `N`
- “节点数量”

without a reason after the variable has been defined.

---

# 12. Define Variables Before Use

Define non-obvious mathematical variables before or at first use.

Prefer:

> 设输入长度为 $n$，窗口大小为 $k$。

Then:

> 时间复杂度为 $O(n)$，额外空间复杂度为 $O(k)$。

Avoid introducing symbols without explanation:

> 因此复杂度为 $O(nk)$。

when $n$ and $k$ have not been defined.

---

# 13. Scalar, Vector, Matrix, and Set Notation

When mathematical precision matters, use consistent notation.

A reasonable convention is:

- scalar: $x$
- vector: $\mathbf{x}$
- matrix: $\mathbf{W}$
- dataset or set: $\mathcal{D}$
- loss function: $\mathcal{L}$

This convention is optional rather than universal.

If the source paper, codebase, or established domain convention uses another notation, preserve that notation.

Consistency matters more than enforcing one global style.

---

# 14. Mathematical Operators

Prefer LaTeX operators inside mathematics.

Use:

```latex
$x \le y$
```

rather than:

```text
x <= y
```

Use:

```latex
$a \neq b$
```

rather than:

```text
a != b
```

Use:

```latex
$x \times y$
```

when multiplication is mathematical.

Programming syntax remains unchanged inside code.

---

# 15. Equality, Assignment, and Definition

Distinguish mathematical equality from programming assignment and comparison.

## Mathematics

Equality:

```latex
x = y
```

Definition by convention when appropriate:

```latex
f(x) := x^2 + 1
```

Use `:=` only when explicitly introducing a definition and when the notation is appropriate for the audience.

## Programming

Assignment:

```python
x = y
```

Comparison:

```python
x == y
```

Do not describe these operators as interchangeable merely because they use similar symbols.

---

# 16. Arrows

Different arrows have different meanings.

## Natural-language Flow

Use:

> Input → Parser → Executor → Output

## Mathematical Mapping

Use:

```latex
f : X \to Y
```

## Limit or Convergence

Use domain-appropriate LaTeX notation:

```latex
x_n \to x
```

## Logical Implication

Use:

```latex
A \Rightarrow B
```

Do not use `\Rightarrow` merely as a decorative flow arrow.

## Programming Syntax

Preserve language syntax:

```python
def f() -> int:
    ...
```

```cpp
node->next
```

---

# 17. Logical Symbols

Use mathematical logical symbols only when they improve precision.

Examples:

```latex
A \land B
```

```latex
A \lor B
```

```latex
\neg A
```

For explanatory technical prose, ordinary language is often clearer.

Prefer:

> 当 A 和 B 同时成立时……

over unnecessarily formal symbolic logic when no mathematical reasoning benefits from it.

Do not use `&&`, `||`, or `!` as mathematical logic outside actual code unless explicitly discussing programming syntax.

---

# 18. Sets and Membership

Use standard mathematical notation when discussing abstract sets.

Examples:

```latex
x \in S
```

```latex
x \notin S
```

```latex
A \subseteq B
```

Programming membership remains language-specific:

```python
x in items
```

```python
x not in items
```

Do not mix these two notation layers in the same expression.

---

# 19. Functions

Mathematical function notation:

```latex
f(x)
```

Programming function call:

```python
f(x)
```

Although they look similar, preserve context.

When discussing an actual function implementation, use inline code:

> 调用 `merge_json(a, b)`。

When discussing an abstract mathematical function, use math:

> 定义函数 $f(x) = x^2$。

---

# 20. Fractions

Prefer LaTeX fractions in mathematical expressions:

```latex
\frac{a}{b}
```

rather than:

```text
a/b
```

when the expression is genuinely mathematical and displayed as math.

Use `/` when it belongs to:

- programming syntax
- units
- paths
- established notation
- simple inline ratios where LaTeX would reduce readability

---

# 21. Powers and Subscripts

Use LaTeX:

```latex
x^2
```

```latex
x_i
```

```latex
W_{ij}
```

Do not write prose approximations such as:

> x2

or:

> x_i

outside math mode when the expression is mathematical rather than code.

If `x_i` is an actual variable name in code, use inline code instead:

> `x_i`

---

# 22. Summation and Products

Use:

```latex
\sum_{i=1}^{n} x_i
```

and:

```latex
\prod_{i=1}^{n} x_i
```

rather than trying to reproduce mathematical notation using plain ASCII.

Explain the meaning of the indices when not obvious.

---

# 23. Probability and Statistics

Use standard notation consistently.

Examples:

```latex
P(A)
```

```latex
P(A \mid B)
```

```latex
\mathbb{E}[X]
```

```latex
\operatorname{Var}(X)
```

Do not use `|` as a generic separator when it represents conditional probability.

If statistical notation appears, define non-obvious quantities.

---

# 24. Loss Functions and Objectives

For machine-learning writing, distinguish:

- loss for one sample
- empirical objective
- regularization term
- optimization target

Example:

```latex
\mathcal{L}(\theta)
=
-\frac{1}{N}
\sum_{i=1}^{N}
\log p_\theta(y_i \mid x_i)
```

After presenting a formula, explain:

1. what the formula computes
2. what each important symbol means
3. what minimizing or maximizing it does
4. why it is relevant to the discussed method

Do not drop a formula into the article without interpretation.

---

# 25. Formula Explanation Protocol

For important formulas, prefer the following order:

1. Formula
2. Variable definitions
3. Intuition
4. Small example where useful
5. Engineering or algorithmic implication

Example structure:

> 定义交叉熵损失为：

```latex
\mathcal{L}
=
-\sum_{i=1}^{C} y_i \log p_i
```

Then explain:

- $C$ is the number of classes
- $y_i$ is the target indicator
- $p_i$ is the predicted probability

Then explain the intuition.

Do not assume that displaying a formula is equivalent to explaining it.

---

# 26. Display Math vs Inline Math

Use inline math for short expressions:

> 时间复杂度为 $O(n \log n)$。

Use display math for important or multi-line formulas:

```latex
\[
\mathcal{L}(\theta)
=
-\frac{1}{N}
\sum_{i=1}^{N}
\log p_\theta(y_i \mid x_i)
\]
```

Do not place long derivations inside inline math if they become difficult to read.

---

# 27. Complexity Notation

Use standard asymptotic notation:

- $O(f(n))$
- $\Omega(f(n))$
- $\Theta(f(n))$

Do not treat them as interchangeable.

## Big-O

Describes an asymptotic upper bound.

## Big-Omega

Describes an asymptotic lower bound.

## Big-Theta

Describes an asymptotically tight bound.

In ordinary interview writing, Big-O is often used informally for runtime complexity, but when mathematical precision matters, preserve the distinction.

---

# 28. Define Complexity Variables

Always define complexity variables when they are not obvious.

Prefer:

> 设输入数组长度为 $n$。

> 设 JSON 总节点数为 $N$，最大嵌套深度为 $D$。

> 设列表长度为 $k$。

Avoid mixing variables without defining their relationship.

---

# 29. State Complexity Assumptions

Complexity expressions depend on a cost model.

Examples:

> 若哈希查询按平均 $O(1)$ 计算……

> 若暂时将单个元素相等性比较视为 $O(1)$……

> 若字符串拼接需要复制已有内容……

Put the assumption close to the complexity result it supports.

Do not hide important cost assumptions in a later unrelated section.

---

# 30. Hidden Costs in Expressions

Inspect operations that visually look constant but may not be.

Examples include:

```python
x in list_obj
```

```python
a == b
```

```python
s1 + s2
```

```python
copy.deepcopy(x)
```

```python
sorted(items)
```

```python
json.dumps(x)
```

Their cost may depend on input size.

Do not classify complexity solely from the number of source-code statements.

---

# 31. Nested Equality

When elements are composite structures, equality may recursively inspect content.

For example, comparing two Python lists can require comparing multiple elements.

Comparing nested lists or dictionaries may require recursively inspecting nested values.

Therefore:

> `x not in res`

does not necessarily mean each candidate comparison is $O(1)$.

When simplifying the analysis, state the simplification explicitly.

---

# 32. Hashing Costs

Do not assume hashing is free.

For an object with representation size $m$, computing a canonical or serialized key may require $O(m)$ work or more.

If dictionary keys are sorted during canonicalization, sorting may introduce an additional factor such as:

```latex
O(k \log k)
```

depending on the representation and cost model.

State which part of the algorithm benefits from hashing.

---

# 33. Copying Costs

Operations such as:

```python
copy.copy(x)
```

and:

```python
copy.deepcopy(x)
```

have different cost behavior.

Shallow copy generally processes the outer container.

Deep copy may recursively traverse an object graph.

Do not treat `deepcopy()` as an $O(1)$ operation when analyzing a structure whose size grows with input.

Also consider:

- shared references
- immutable objects
- memoization inside deep-copy implementations
- cycles where supported

when those details affect the argument.

---

# 34. String Operations

Do not automatically treat string concatenation as constant time.

Example:

```python
a + b
```

may require allocating and copying characters.

When repeated concatenation appears inside a loop, inspect whether it can lead to superlinear work.

Language and runtime implementation details may matter.

State assumptions when necessary.

---

# 35. Sorting

Standard comparison sorting is commonly analyzed as:

```latex
O(n \log n)
```

but the cost of comparing two elements may itself depend on element size.

For strings, nested structures, or custom comparison functions, consider comparison cost when it materially changes the conclusion.

---

# 36. Recursion

For recursive code, complexity analysis should consider:

- branching factor
- recursion depth
- work per call
- overlapping subproblems
- repeated traversal
- copying at each level

Do not infer:

> recursion depth is $D$, therefore time complexity is $O(D)$.

Depth and total number of calls are different quantities.

---

# 37. Recursion Stack

When relevant, state recursion-stack space separately.

Example:

> 最大嵌套深度为 $D$，因此递归调用栈最多需要 $O(D)$ 空间。

This does not include the output object unless explicitly stated.

---

# 38. Output Space vs Auxiliary Space

Be explicit about the chosen convention.

Example:

> 返回结果本身需要 $O(N)$ 空间；若不计输出空间，额外递归栈空间为 $O(D)$。

This is clearer than:

> 空间复杂度为 $O(N)$。

when readers may interpret “space complexity” differently.

---

# 39. Average and Worst Case

Do not combine average-case primitive costs with worst-case algorithm claims without saying so.

Example:

> 若按 Python `dict` 查询平均 $O(1)$ 计算……

Then derive the result under that model.

If a worst-case dictionary bound matters, analyze it separately.

---

# 40. Complexity vs Performance

Do not write:

> $O(n)$ 一定比 $O(n \log n)$ 快。

Asymptotic complexity describes growth.

Actual runtime also depends on:

- constant factors
- input size
- memory allocation
- cache behavior
- implementation
- hardware
- I/O
- vectorization
- branch behavior

Prefer:

> 该实现具有更好的渐近复杂度。

when only Big-O analysis is available.

---

# 41. Units in Mathematical and Technical Expressions

Use consistent unit formatting in prose:

> 10 ms

> 32 GB

> 2.4 GHz

> 7.5 GB/s

Do not mix units silently.

When formulas contain physical units, ensure dimensional consistency.

For technical benchmark tables, keep units explicit in either:

- the column heading
- every value

Example:

```markdown
| Method | Latency (ms) |
| --- | ---: |
| A | 120 |
| B | 95 |
```

or:

```markdown
| Method | Latency |
| --- | ---: |
| A | 120 ms |
| B | 95 ms |
```

Choose one style consistently.

---

# 42. Numeric Precision

Do not imply false precision.

Avoid reporting:

> 84.732184%

when the experiment does not justify six decimal places.

Use a precision appropriate to:

- measurement noise
- sample size
- reporting convention
- comparison needs

Keep comparable values at comparable precision.

---

# 43. Formula-Derived Numbers

When a numerical result is derived from a formula, ensure:

- the substituted values are correct
- units are consistent
- rounding is explained when relevant
- the result matches the stated formula

Do not manually copy a numeric result from an earlier version after changing the formula.

---

# 44. Code-Derived Numbers

When reporting benchmark or experiment numbers produced by code, ensure:

- code and configuration match the reported result
- metric definition is clear
- aggregation method is clear when relevant
- units are correct

Do not report values whose provenance is unclear.

---

# 45. Mathematical Assumptions

State assumptions needed for a derivation.

Examples:

> 假设样本独立同分布。

> 假设矩阵可逆。

> 假设 $n > 0$。

> 假设哈希查询按平均 $O(1)$ 计算。

Do not bury essential assumptions after the conclusion.

---

# 46. Boundary Conditions in Formulas

Check whether formulas remain valid at boundaries.

Examples:

- $n = 0$
- division by zero
- empty set
- empty sequence
- logarithm domain
- probability equal to zero
- matrix dimensions
- tensor shapes

Mention boundary constraints when they matter to implementation or correctness.

---

# 47. Tensor and Matrix Shapes

In deep-learning writing, state tensor shapes when shape transformations are important.

Example:

> 输入张量形状为 $B \times C \times T$。

If the notation represents dimensions rather than multiplication, clarify the meaning.

For human-readable dimensions, `×` may be used in prose:

> 输入形状为 $B \times C \times T$。

In code, preserve actual shape syntax:

```python
x.shape == (B, C, T)
```

Do not confuse symbolic dimensions with actual integer values.

---

# 48. Indexing Conventions

Be consistent about whether indices start at:

- 0
- 1

Mathematical derivations often use:

```latex
i = 1, \ldots, n
```

Programming languages commonly use zero-based indexing.

If an article moves between mathematics and code, make the difference clear when it could cause confusion.

---

# 49. Inclusive and Exclusive Bounds

For algorithms, distinguish:

- `[left, right]`
- `[left, right)`
- `(left, right)`
- mathematical interval notation

Do not say only:

> 搜索区间是 left 到 right。

when correctness depends on whether endpoints are included.

Use explicit notation:

> 当前维护闭区间 `[left, right]`。

If mathematical interval notation is intended, use math:

> $[l, r)$

Do not mix code-array notation and mathematical interval notation ambiguously.

---

# 50. Invariants

When a loop or algorithm depends on an invariant, state it precisely.

Example:

> 每轮循环开始时，目标值若存在，则一定位于闭区间 `[left, right]` 内。

Then verify that each branch preserves the invariant.

Do not call a property an invariant if it is not maintained throughout the relevant execution.

---

# 51. Recurrence Relations

For recursive or dynamic-programming algorithms, write recurrences mathematically when useful.

Example:

```latex
T(n) = 2T(n/2) + O(n)
```

Then state the resulting complexity and reasoning.

Do not present a recurrence without defining:

- what $T(n)$ represents
- base cases
- relevant assumptions

---

# 52. Dynamic Programming State Definitions

For DP explanations, define state precisely.

Example:

> 定义 $dp[i]$ 为以索引 $i$ 结尾的最长递增子序列长度。

Then define:

- transition
- initialization
- iteration order
- answer extraction

Do not write transitions before defining the state.

---

# 53. Probability Claims

Do not confuse:

- probability
- frequency
- confidence
- model score
- calibrated probability

If a model outputs `0.9`, do not automatically call it:

> 90% 的真实概率

unless the value is actually calibrated and semantically defined as such.

---

# 54. Logarithm Base

When the logarithm base matters, state it.

Examples:

```latex
\log_2 n
```

```latex
\ln x
```

In Big-O expressions, the logarithm base often changes only by a constant factor:

```latex
O(\log n)
```

so the base may be omitted unless the exact value matters.

---

# 55. Code Identifiers Inside Math

Do not place literal code identifiers into mathematical notation unless intentionally modeling them as variables.

Prefer:

> `batch_size` 设置为 32。

rather than:

> $batch\_size = 32$

when `batch_size` is literally a configuration parameter.

Use math notation only when treating the quantity abstractly:

> 设 Batch Size 为 $B$。

---

# 56. Math Inside Code

Do not alter code to look like mathematical notation.

Incorrect:

```python
loss = −sum(yᵢ * log(pᵢ))
```

Correct:

```python
loss = -sum(y[i] * math.log(p[i]) for i in range(c))
```

A mathematical formula and its code implementation may be shown separately.

---

# 57. Mapping Formula to Code

When a formula is implemented in code and the mapping is non-trivial, explain correspondence.

Example:

Formula:

```latex
z = Wx + b
```

Code:

```python
z = linear(x)
```

Explain that `linear` internally represents the affine transformation rather than implying the source code literally performs the written expression line by line.

---

# 58. Numerical Stability

When mathematical formulas are transformed for implementation, note numerical-stability considerations when relevant.

Examples:

- log-sum-exp trick
- epsilon in denominators
- softmax stabilization
- clipping
- floating-point precision

Do not claim two expressions are implementation-equivalent merely because they are algebraically equivalent over real numbers.

Floating-point arithmetic may change behavior.

---

# 59. Floating-Point Equality

Be careful with claims involving exact floating-point equality.

Avoid teaching:

```python
a == b
```

as universally reliable for results of floating-point computation.

When numerical approximation matters, discuss tolerance-based comparison.

Do not overcomplicate articles where exact values are intentionally used and floating-point error is irrelevant.

---

# 60. Overflow and Numeric Range

For languages with fixed-width integer types, consider overflow when relevant.

Do not assume:

> `int` can hold any integer

in C++, Java, Go, or similar languages.

Python integers have different semantics.

State language-specific behavior when it affects correctness.

---

# 61. Complexity of Built-ins

Do not assume built-in functions are constant-time simply because they are one line.

Examples:

```python
len(x)
```

may be constant-time for some built-in containers.

But:

```python
sorted(x)
```

is not.

Likewise:

```python
copy.deepcopy(x)
```

```python
json.dumps(x)
```

```python
str.join(items)
```

may scale with input size.

When complexity matters, analyze semantics rather than source-code line count.

---

# 62. Library and Runtime Sensitivity

Some complexity or behavior depends on:

- language version
- runtime implementation
- library implementation

State the relevant environment when a conclusion is not guaranteed by the language or API contract.

Do not attribute implementation-specific optimization to the abstract language without qualification.

---

# 63. Mathematical Proof vs Engineering Explanation

Not every technical article requires formal proof.

Use the level of rigor appropriate to the purpose.

For an interview solution, a correctness invariant may be enough.

For a mathematical algorithm article, a proof may be appropriate.

For an engineering blog, mechanism and empirical validation may matter more.

Do not introduce symbolic formalism that does not improve understanding.

---

# 64. Avoid Symbol Overload

Do not use the same symbol for unrelated quantities in one derivation.

Avoid:

> $n$ simultaneously means array length and number of graph nodes.

Choose different symbols or clearly re-scope the notation.

Likewise, avoid assigning multiple meanings to common letters such as:

- $N$
- $K$
- $T$
- $D$

within one section without explanation.

---

# 65. Avoid Excessive Symbols

Do not introduce mathematical notation when prose is clearer.

Bad:

> 设 $A$ 表示 Agent，$T$ 表示 Tool，因此 $A \to T$。

if the only purpose is to write a simple system flow.

Prefer:

> Agent → Tool

Mathematics should add precision, not ceremony.

---

# 66. Formula References

When an article contains several important formulas, number them if readers need to refer back to them.

Example:

```latex
\[
\mathcal{L}
=
-\sum_{i=1}^{C} y_i \log p_i
\tag{1}
\]
```

Then:

> 根据式（1）……

Do not number every trivial expression.

Use numbering when cross-reference improves readability.

---

# 67. Code Example Inputs and Outputs

Label examples consistently.

Prefer:

```markdown
**输入：**

```text
...
```

**输出：**

```text
...
```
```

Use actual output syntax when appropriate.

For JSON output, use a `json` fence only when the output is valid JSON.

For Python representations containing `None`, `True`, or `False`, use `python` or `text`, not `json`.

---

# 68. JSON vs Python Literals

Remember:

JSON uses:

```json
{
  "enabled": true,
  "value": null
}
```

Python uses:

```python
{
    "enabled": True,
    "value": None,
}
```

Do not mix:

- `true` with Python syntax
- `True` with JSON syntax
- `null` with Python syntax
- `None` with JSON syntax

This distinction is especially important in interview write-ups and API examples.

---

# 69. Shell Commands

Use code fences such as:

```bash
git status
git add .
git commit
```

Do not include shell prompts such as `$` unless the prompt itself is useful.

Prefer:

```bash
python main.py
```

over:

```bash
$ python main.py
```

when the reader is expected to copy the command directly.

If showing output, separate command and output when ambiguity is possible.

---

# 70. SQL

Use `sql` fences for SQL.

Example:

```sql
SELECT DISTINCT name
FROM users;
```

Preserve SQL semantics.

Do not apply mathematical formatting to SQL operators.

If discussing execution plans, indexes, or optimizer behavior, distinguish SQL text from explanatory prose.

---

# 71. File Paths and Commands

Use inline code for literal paths and commands:

> 打开 `src/main.py`。

> 执行 `git status`。

For multiline sequences:

```bash
git add .
git commit
git push
```

Do not use quotation marks merely to mark a path if inline code is clearer.

---

# 72. Placeholder Syntax

Clearly distinguish placeholders from literal input.

Examples:

```text
<TAILSCALE_IP>
```

```text
<USERNAME>
```

or:

```text
YOUR_API_KEY
```

State once that the token is a placeholder if readers might copy it literally.

Do not mix placeholder notation styles in the same document without reason.

---

# 73. Redacted Values

When showing credentials, tokens, passwords, or secrets, never expose real values.

Use placeholders:

```text
<API_KEY>
```

or:

```text
********
```

Prefer semantically meaningful placeholders.

Do not include real secrets merely because they appeared in local configuration or command output.

---

# 74. Code Diff

When reviewing or explaining changes, a diff may be clearer than repeating entire files.

Example:

```diff
- res[key] = value
+ res[key] = copy.deepcopy(value)
```

Use diff blocks when the relationship between old and new code is the point.

Do not use diff formatting for unrelated code snippets.

---

# 75. Truncated Code

If code is intentionally shortened, make the omission explicit.

Examples:

```python
def solve():
    ...
```

or prose:

> 以下省略输入校验与日志代码。

Do not silently delete relevant lines from an excerpt if the omission changes how readers interpret the behavior.

---

# 76. Error Messages and Logs

Use `text` fences unless a more specific language is appropriate.

Example:

```text
TypeError: unhashable type: 'dict'
```

Preserve meaningful punctuation and capitalization from the original message.

Do not rewrite an actual error message as if it were exact if it has been paraphrased.

---

# 77. Source Code Quotations

When quoting implementation code from an external project:

- preserve relevant syntax
- identify the source when necessary
- avoid changing code in ways that alter semantics
- clearly mark omitted sections
- respect copyright and quotation limits

When only the mechanism matters, paraphrasing the implementation may be better than reproducing a large block.

---

# 78. Code Review Checklist

When reviewing code embedded in technical writing, verify:

- [ ] The code matches the claimed language.
- [ ] The fence language identifier is correct.
- [ ] The code is syntactically valid unless explicitly labeled pseudocode.
- [ ] Variables and functions referenced in prose match the code.
- [ ] Literal values use the correct language syntax.
- [ ] JSON and Python literals are not mixed.
- [ ] Programming operators have not been replaced by Unicode typography.
- [ ] Important omitted context is acknowledged.
- [ ] Comments explain non-obvious reasoning rather than restating syntax.
- [ ] The implementation actually matches the described algorithm.
- [ ] Examples and outputs agree with the code.

---

# 79. Mathematical Review Checklist

Verify:

- [ ] Mathematical variables are defined before or at first use.
- [ ] The same symbol keeps the same meaning.
- [ ] Mathematical expressions use LaTeX where supported.
- [ ] Programming operators are not used as mathematical notation without reason.
- [ ] Flow arrows and logical implication are distinguished.
- [ ] Equality, assignment, comparison, and definition are not conflated.
- [ ] Formula assumptions are stated.
- [ ] Important boundary conditions are considered.
- [ ] Units are consistent.
- [ ] Numeric precision is justified.
- [ ] Important formulas are explained rather than merely displayed.
- [ ] Tensor/matrix shapes are consistent where relevant.
- [ ] Index conventions are clear.
- [ ] Formula-derived numbers match the formulas.

---

# 80. Complexity Review Checklist

Verify:

- [ ] Input-size variables are defined.
- [ ] Primitive-operation assumptions are stated where needed.
- [ ] Hidden costs in built-ins and container operations are considered.
- [ ] Equality comparison cost is considered for composite elements.
- [ ] Hash computation cost is considered where relevant.
- [ ] Sorting and canonicalization costs are considered.
- [ ] Copying and serialization costs are considered.
- [ ] Recursive call count and recursion depth are distinguished.
- [ ] Average-case and worst-case costs are not mixed silently.
- [ ] Output space and auxiliary space are distinguished when useful.
- [ ] Recursion-stack space is included where relevant.
- [ ] Big-O is not confused with actual runtime performance.

---

# 81. Natural Language / Math / Code Boundary Checklist

Before publication, inspect expressions that cross notation systems.

Ask:

### Is this prose?

Use human-readable technical typography where appropriate:

> A → B

> 1920 × 1080

### Is this mathematics?

Use LaTeX:

> $A \Rightarrow B$

> $x \le y$

### Is this code?

Preserve exact programming syntax:

```python
x <= y
```

Never modify one notation system solely to visually imitate another.

---

# Core Principle

Code should be syntactically faithful.

Mathematics should be semantically precise.

Prose should be readable.

When the same concept appears in all three forms, preserve the conventions of each form and explain the correspondence when necessary.

Do not collapse natural language, mathematics, and programming syntax into one mixed notation system.