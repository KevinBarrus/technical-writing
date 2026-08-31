# Technical Rigor Guide

## Purpose

Define the reasoning standards used when writing or reviewing computer science technical content.

This guide focuses on:

- technical correctness
- claim strength
- assumptions
- scope
- definitions
- derivations
- causality
- analogies
- complexity analysis
- experiments
- engineering observations
- implementation-specific behavior
- domain-specific reasoning

The goal is not to make technical writing sound academic.

The goal is to make it easy for a reader to determine:

- what is known
- what is assumed
- what is derived
- what is observed
- what is inferred
- what is only an intuition
- under what conditions a conclusion holds
- where the conclusion stops applying

---

# 1. Core Principle

Do not optimize for the appearance of rigor.

Optimize for actual rigor.

A technically rigorous explanation should answer, where relevant:

1. What exactly is being claimed?
2. What evidence or reasoning supports the claim?
3. What assumptions does the claim depend on?
4. What is the scope of the claim?
5. Is the claim a definition, fact, derivation, observation, analogy, or opinion?
6. Does the wording overstate the available evidence?
7. Would the conclusion change under another reasonable assumption?

---

# 2. Classify Claims Before Evaluating Them

When reviewing an important statement, first determine what kind of statement it is.

Common categories include:

- Definition
- Established fact
- Specification
- Assumption
- Mathematical derivation
- Algorithmic argument
- Experimental result
- Engineering observation
- Implementation detail
- Analogy
- Intuition
- Hypothesis
- Opinion
- Recommendation

Do not let one category masquerade as another.

---

## 2.1 Definition

A definition states what a term means within a language, paper, framework, standard, or explicitly declared local context.

Example:

> 在本文中，Context 指一次模型调用时实际进入 prompt 的信息集合。

A local definition should be labeled as local when it differs from broader usage.

Prefer:

> 在本文中……

> 在该系统中……

> 这里将……定义为……

Do not silently present a project-specific definition as a universal one.

---

## 2.2 Established Fact

An established fact should be supported by:

- language semantics
- official documentation
- standards
- source code
- a well-established theorem
- primary literature
- reproducible behavior where implementation-specific

Example:

> 在 Python 中，`bool` 是 `int` 的子类。

This is different from:

> Python 一般会把布尔值当作整数处理。

The first is a concrete language-level fact.
The second is vague and may mislead readers about semantics.

---

## 2.3 Specification

A specification describes required behavior rather than observed behavior.

Examples:

> 题目要求返回新的 JSON，且不能修改原始输入。

> API 规定该字段不能为空。

Do not confuse:

> should behave this way

with:

> currently behaves this way.

Implementation behavior may violate a specification.

---

## 2.4 Assumption

An assumption is a condition accepted for the current analysis.

Examples:

> 假设哈希查询的平均时间复杂度为 $O(1)$。

> 假设单个元素的相等性比较为 $O(1)$。

> 假设网络不存在丢包。

Important assumptions MUST be stated when removing them could change the conclusion.

---

## 2.5 Derivation

A derivation follows from previously stated premises, formulas, invariants, or rules.

Prefer explicit logical structure:

> 因为 A，并且 B，所以 C。

Do not hide missing reasoning behind words such as:

- 显然
- 易知
- 不难发现
- 很容易看出

If a step matters, state the actual reason.

---

## 2.6 Experimental Result

An experimental result describes what happened under a specific experimental configuration.

Prefer:

> 在该数据集和当前配置下，Accuracy 从 82.1% 提升到 84.7%。

Do not automatically generalize this into:

> 该方法能够提升准确率。

unless the evidence supports the broader claim.

---

## 2.7 Engineering Observation

An engineering observation describes behavior seen in a concrete system or implementation.

Examples:

> 在当前测试环境中，缓存命中后请求延迟明显降低。

> 在本次压测中，该实现的 P99 Latency 为 120 ms。

Do not present an engineering observation as a universal theoretical property.

---

## 2.8 Analogy and Intuition

Analogies and intuitive models are teaching tools.

They are not definitions.

Prefer:

> 可以将 Python 变量名近似理解为指向 Python 对象的引用，以帮助理解对象共享关系。

Avoid:

> Python 变量就是 C++ 指针。

When the analogy has important limitations, state them.

---

# 3. Control Claim Strength

Technical writing should use wording that matches the strength of available evidence.

A useful rough scale is:

> 可能 < 通常 < 会 < 必然

These words are not interchangeable.

---

## 3.1 Possible

Use wording such as:

- 可能
- 可能会
- 在某些情况下
- 存在……的可能

when the behavior depends on conditions not fully controlled.

Example:

> 嵌套对象的相等性比较可能产生额外开销。

---

## 3.2 Typical or Common

Use:

- 通常
- 一般情况下
- 在常见实现中
- 在多数情况下

when describing common but non-universal behavior.

Always ask whether there are meaningful exceptions.

---

## 3.3 Expected or Deterministic Behavior

Use:

- 会
- 将
- 导致

when the stated conditions are sufficient to produce the result.

Example:

> 当 `a[0]` 和 `b[0]` 指向同一个可变 `list` 对象时，通过 `b[0].append(...)` 修改该对象后，通过 `a[0]` 也能观察到变化。

---

## 3.4 Necessary or Universal Claims

Use:

- 必然
- 一定
- 所有
- 任何
- 永远
- 保证
- 唯一

only when the relevant specification, theorem, logic, or explicitly stated assumptions justify the universal claim.

Universal words have high proof obligations.

---

# 4. High-Risk Words

Treat the following words as review triggers:

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
- 无需
- 不可能
- 总是
- 从不

Do not ban them mechanically.

Instead ask:

1. What exactly justifies this strength?
2. What scope does the statement apply to?
3. Are there counterexamples?
4. Is a weaker phrase more accurate?

---

# 5. Scope Every Important Claim

A claim should state its scope when the conclusion is not universal.

Common scope dimensions include:

- programming language
- language version
- runtime
- framework
- operating system
- database engine
- database version
- deployment topology
- hardware
- dataset
- model
- benchmark
- input distribution
- concurrency model
- network conditions
- implementation
- experiment configuration

Prefer:

> 在 CPython 3.x 的当前实现中……

when discussing implementation-specific behavior.

Prefer:

> 在该数据集和当前划分方式下……

when discussing experimental results.

Prefer:

> 对于使用 B-Tree 索引的该查询模式……

when the conclusion depends on a specific index structure.

---

# 6. Specification Ambiguity

NEVER silently resolve meaningful ambiguity in a problem, paper, API, or requirement.

If two sources of expected behavior conflict, explicitly record the conflict.

Use this protocol:

1. Identify the conflict.
2. State the adopted interpretation.
3. State the basis for that interpretation.
4. State the consequence of alternative interpretations when material.

Example:

> 题目文字描述列表规则为“拼接”，但给定样例表现出重复元素需要被移除，因此本文按照样例实现为稳定拼接去重，即保留元素第一次出现的位置并维持原有顺序。

This is better than silently implementing deduplication.

---

# 7. Do Not Hide Missing Reasoning

Avoid phrases that replace reasoning with rhetoric.

High-risk phrases include:

- 显然
- 我们知道
- 很容易看出
- 不难发现
- 众所周知
- 毫无疑问

If the statement is important, replace these phrases with the reason.

Instead of:

> 显然这里应该使用递归。

Prefer:

> JSON 具有递归结构：`dict` 的 value 仍可能是 `dict` 或 `list`。当两个相同 key 对应的 value 仍是复合结构时，需要再次应用相同合并规则，因此可以自然地将该过程定义为递归函数。

---

# 8. Definition Is Not Implementation

Do not define a general concept using only one concrete implementation.

Bad:

> Memory 就是把历史对话存进数据库。

Better:

> Memory 指跨时间保存并在需要时重新引入当前推理过程的信息。数据库持久化只是其中一种实现方式。

Bad:

> RAG 就是向量数据库。

Better:

> RAG 是将外部检索结果引入生成过程的一类方法；向量检索是常见实现之一。

When explaining an important concept, prefer:

> Definition → Motivation → Mechanism → Implementation → Evaluation

where appropriate.

---

# 9. Analogy Is Not Equivalence

Analogy is useful only when its boundary is clear.

Bad:

> Python 变量就是 C++ 指针。

Better:

> 为理解对象共享关系，可以将 Python 变量名近似类比为指向对象的引用；这个模型有助于理解别名和对象共享，但并不意味着 Python 变量在语言语义或底层实现上等同于 C++ 指针。

When reviewing an analogy, ask:

1. What does the analogy explain well?
2. Where does it break?
3. Could a beginner mistake the analogy for an exact definition?

If yes, add a boundary statement.

---

# 10. Separate Intuition from Formal Explanation

Intuition is valuable but should be labeled when it simplifies reality.

Useful phrases include:

- 可以直观理解为
- 可以建立如下心智模型
- 从……角度看
- 粗略地说
- 作为一种近似理解

After giving intuition, provide the more exact explanation when the distinction matters.

Example:

> 可以直观地把浅拷贝理解为“只复制第一层”。更精确地说，浅拷贝创建新的最外层容器，但容器中保存的对象引用会被复制，不会递归复制引用所指向的对象。

---

# 11. Correlation Is Not Causation

Do not infer causality merely because two values changed together.

Bad:

> Batch Size 从 32 调到 64 后准确率下降，因此更大的 Batch Size 会降低准确率。

Better:

> 在本次实验中，将 Batch Size 从 32 调整为 64 后，Accuracy 从 X 降至 Y。由于其他潜在影响因素尚未被充分控制，该结果不足以单独证明准确率下降由 Batch Size 增大导致。

For causal language, ask whether:

- other variables were controlled;
- the experiment was repeated;
- random variation was considered;
- the mechanism is understood;
- alternative explanations were excluded.

---

# 12. Experiment Does Not Equal Proof

Prefer:

- 表明
- 支持
- 观察到
- 在当前实验中表现为
- 与……一致

over:

- 证明

unless the statement is genuinely established by formal proof or evidence sufficient for that level of claim.

Experimental results usually support a claim rather than prove a universal proposition.

---

# 13. Statistical and Practical Significance

Do not use the word:

> 显著

ambiguously.

“显著” may refer to:

- statistically significant
- practically meaningful
- visually obvious
- numerically large

If statistical significance is intended, report the relevant statistical methodology where appropriate.

If practical significance is intended, state the concrete magnitude instead.

Prefer:

> Accuracy 提升 2.6 个百分点。

over:

> Accuracy 得到显著提升。

unless “significant” is explicitly defined.

---

# 14. Percentage Points vs Relative Percentage

If a metric changes from 80% to 84%:

- absolute change: 4 percentage points
- relative change: 5%

Do not write:

> 提升了 4%

when the intended meaning is:

> 提升了 4 个百分点。

The distinction matters in technical comparisons.

---

# 15. Complexity Analysis Requires a Cost Model

Complexity claims are conditional on how primitive operations are counted.

Before giving a complexity result:

1. Define input-size variables.
2. Identify relevant operations.
3. State the cost assumptions of those operations.
4. Analyze loops and recursion.
5. Inspect hidden costs.
6. Distinguish average and worst case.
7. Analyze space separately.
8. Include recursion-stack depth where relevant.

---

## 15.1 Define Input Size

Do not write only:

> 时间复杂度为 $O(n)$。

when the meaning of $n$ is unclear.

Prefer:

> 设两个输入 JSON 的总节点数为 $N$，最大嵌套深度为 $D$。

For multiple dimensions, define each variable explicitly.

---

## 15.2 Hidden Operation Costs

Do not count only visible loops.

Operations that may contain hidden work include:

- list membership
- dictionary lookup
- equality comparison
- hashing
- sorting
- copying
- serialization
- deserialization
- string concatenation
- canonicalization
- regex matching
- database access
- network calls
- filesystem operations

Example:

```python
if x not in res:
    ...
```

If `res` is a Python `list`, membership testing performs a linear scan.

However, the cost of comparing `x` with one candidate element may itself be non-constant.

For nested `list` or `dict` values, equality comparison may recursively inspect nested contents.

Therefore a rigorous statement may be:

> 若暂时将单个元素的相等性比较视为 $O(1)$，则长度为 $k$ 的列表使用线性成员查询进行稳定去重时，最坏时间复杂度为 $O(k^2)$。对于嵌套 `list` 或 `dict` 元素，相等性比较本身还可能产生额外开销。

---

## 15.3 Average vs Worst Case

Do not mix average-case and worst-case costs.

Example:

Python dictionary lookup is commonly treated as average $O(1)$.

Do not silently use average $O(1)$ for one operation and then describe the entire result as an unconditional worst-case bound.

State the model clearly.

Example:

> 若按 Python `dict` 查询平均 $O(1)$ 计算……

---

## 15.4 Recursive Algorithms

For recursive algorithms, inspect:

- number of recursive calls;
- work performed at each call;
- maximum recursion depth;
- whether subproblems overlap;
- whether the same input region is processed repeatedly.

Do not infer complexity from recursion depth alone.

---

## 15.5 Result Space vs Auxiliary Space

Distinguish when useful:

- result/output space
- auxiliary space
- recursion-stack space

Example:

> 由于题目要求构造新的合并结果，输出结果本身需要 $O(N)$ 空间；除此之外，递归调用栈最多需要 $O(D)$ 空间。

Do not automatically call output space “extra space” without clarifying the convention being used.

---

# 16. Optimization Claims Require Full Accounting

Do not claim that an optimization changes the entire asymptotic complexity merely because one local operation becomes faster.

Example:

Replacing:

```python
x not in res
```

with a hash-based `seen` structure may reduce duplicate lookup cost.

But the complete algorithm may still need to account for:

- hashability
- hash computation
- canonical representation
- nested traversal
- sorting dictionary keys
- object allocation
- memory overhead
- equality checks after hash collisions

Prefer:

> 使用 `seen` 可以将判重查询从线性扫描优化为平均常数时间，但如果 JSON 元素需要先递归转换为 canonical representation，则生成该表示本身仍有额外成本，因此不能直接将整个算法概括为从 $O(k^2)$ 降为 $O(k)$。

State exactly what is optimized.

---

# 17. Big-O Is Not Wall-Clock Performance

Do not equate asymptotic complexity with actual runtime.

An $O(n)$ algorithm may be slower than an $O(n \log n)$ algorithm for realistic input sizes because of:

- constants
- memory access patterns
- cache locality
- vectorization
- runtime implementation
- allocations
- branch behavior
- system calls
- network or disk access

Use Big-O to describe growth behavior, not absolute speed.

Prefer:

> 该实现具有更好的渐近复杂度。

rather than:

> 该实现一定更快。

unless measured performance also supports the claim.

---

# 18. Correctness Arguments

When an algorithm depends on a non-obvious invariant, greedy choice, recurrence, or data-structure property, explain why the algorithm is correct.

A useful structure is:

1. State the invariant or key property.
2. Show it holds initially.
3. Show each operation preserves it.
4. Explain why termination implies the desired result.

Not every interview note needs a formal proof.

However, do not replace correctness reasoning with:

> 代码跑过样例，所以算法是正确的。

Passing tests provides evidence, not proof of general correctness.

---

# 19. Examples Are Not Proof

Examples are useful for:

- intuition
- demonstrating execution
- explaining edge cases
- validating implementation behavior

Examples do not establish correctness for all possible inputs.

Prefer:

> 下面通过一个例子说明该过程。

Do not imply:

> 这个例子说明算法对所有输入都成立。

without a general argument.

---

# 20. Tests Are Evidence, Not Exhaustive Verification

Passing tests increases confidence.

It does not automatically establish:

- correctness for all inputs
- absence of race conditions
- absence of security vulnerabilities
- production reliability
- portability across environments

State test scope when relevant.

Example:

> 当前测试覆盖基本合并规则、嵌套对象以及列表去重场景，但尚未覆盖循环引用或自定义对象。

---

# 21. Distinguish Language Semantics from Implementation Details

This distinction is essential in systems and programming-language writing.

Possible layers include:

1. language semantics
2. standard/library contract
3. runtime behavior
4. implementation detail
5. operating-system behavior
6. hardware behavior

Do not attribute an implementation detail to the language specification unless the specification actually requires it.

Example:

> CPython currently uses reference counting as part of its memory-management implementation.

is more precise than:

> Python uses reference counting.

when discussing language-independent Python semantics.

---

# 22. Distinguish API Contract from Current Behavior

An API contract describes what callers may rely on.

Observed implementation behavior may be narrower, broader, or accidental.

Avoid documenting accidental current behavior as guaranteed API semantics.

When relevant, state:

> 当前实现……

versus:

> API 保证……

---

# 23. Backend and Distributed Systems Claims

For backend, database, network, and distributed-system explanations, explicitly inspect hidden environmental assumptions.

Relevant dimensions may include:

- single process vs multi-process
- single machine vs distributed deployment
- concurrency model
- isolation level
- replication
- consistency model
- failure model
- retry behavior
- network partitions
- clock assumptions
- idempotency
- persistence
- ordering guarantees

Avoid claims such as:

> 加锁后就不会有并发问题。

Instead state:

- what resource is locked;
- who shares the lock;
- lock scope;
- failure behavior;
- whether the lock is process-local or distributed;
- what class of race condition is prevented.

---

# 24. Database Explanations

When discussing databases, distinguish:

- logical SQL semantics
- optimizer behavior
- storage-engine behavior
- transaction isolation
- locking
- MVCC
- durability
- replication

Avoid universal statements that depend on a specific engine.

Prefer:

> 在 InnoDB 中……

when the behavior is InnoDB-specific.

Do not use terms such as “事务安全” or “线程安全” without describing the relevant property.

---

# 25. Network Explanations

Keep protocol layers and responsibilities distinct.

Do not attribute behavior to TCP when it belongs to:

- IP
- TLS
- HTTP
- DNS
- application logic

Avoid shorthand that collapses multiple layers unless clearly presented as an intuition.

State whether the explanation is:

- protocol semantics
- common implementation behavior
- deployment behavior

---

# 26. AI Agent Explanations

Avoid anthropomorphic descriptions when they hide the mechanism.

Bad:

> Agent 意识到计划失败了，于是重新思考。

Better:

> Executor 返回失败 Observation 后，Replanner 根据当前计划、执行状态和历史 Observation 生成新的 Plan。

When using terms such as:

- Agent
- Planning
- Reflection
- Reasoning
- Memory
- Context
- Tool
- Observation
- Skill

define their operational meaning in the system when ambiguity matters.

Do not assume these terms have one universal architecture-independent definition.

---

# 27. Context vs Memory

Do not casually equate Context and Memory.

A useful distinction is:

> Context 是当前模型调用实际可见的信息。

> Memory 是跨时间保存、并在需要时重新进入 Context 的信息或状态。

This distinction is an operational model, not necessarily the only valid terminology across all systems.

State the local architecture when needed.

---

# 28. Tool Use and Agent Capabilities

Do not describe a model capability as an Agent capability when the behavior actually depends on:

- external tools
- runtime orchestration
- middleware
- retrieval
- memory
- prompt construction
- permission system

Prefer mechanism-level descriptions.

Example:

> Runtime 将 Tool Schema 提供给模型，并在模型返回 Tool Call 后执行对应工具，再把 Tool Result 回注到下一轮 Context。

This is more informative than:

> 模型会使用工具。

---

# 29. RAG Explanations

Do not reduce RAG to vector search.

A RAG system may involve:

- document ingestion
- chunking
- indexing
- lexical retrieval
- dense retrieval
- hybrid retrieval
- reranking
- filtering
- context construction
- generation
- evaluation

When claiming retrieval quality improvement, state:

- metric
- dataset
- baseline
- retrieval depth
- evaluation method

Do not infer answer-quality improvement automatically from retrieval-score improvement.

---

# 30. Deep Learning Explanations

Separate:

- model architecture
- objective function
- optimization algorithm
- training procedure
- regularization
- inference
- evaluation

Do not describe:

> 模型学到了某个概念

as a precise mechanistic statement unless the context supports such an interpretation.

Prefer:

> 模型参数经过训练后，对该模式表现出更高的预测概率。

when a mechanism-level statement is needed.

---

# 31. Experimental Machine Learning

When discussing ML experiments, consider recording:

- model
- model version
- dataset
- dataset preprocessing
- train/validation/test split
- random seed
- hardware
- framework
- framework version
- batch size
- learning rate
- optimizer
- scheduler
- number of epochs
- number of steps
- evaluation metric
- baseline
- checkpoint selection rule
- evaluation protocol

Not every blog requires every field.

Include the variables needed for readers to understand and reproduce the claimed result.

---

# 32. Benchmark Claims

Avoid:

> 模型 A 比模型 B 更强。

Prefer:

> 在 benchmark X 的 metric Y 上，模型 A 得分为 84.7，模型 B 得分为 81.2。

A benchmark comparison is bounded by:

- benchmark design
- task distribution
- evaluation implementation
- prompting
- inference settings
- model version

Do not generalize beyond what the benchmark measures.

---

# 33. Performance Claims

Use measured quantities when possible.

Avoid:

- 很快
- 很慢
- 很省内存
- 性能很好
- 延迟很低
- 吞吐量很高

Prefer:

> P50 Latency 为 80 ms，P99 Latency 为 210 ms。

> 峰值内存从 2.1 GB 降到 1.4 GB。

If a qualitative word is used, define the comparison baseline.

---

# 34. Security and Reliability Claims

Words such as:

- 安全
- 可靠
- 保证
- 不会失败
- 完全隔离

require particularly careful scope.

Prefer describing concrete guarantees:

> 该校验可以阻止未通过 Schema 验证的参数进入 Tool Executor。

rather than:

> 该机制保证工具调用安全。

Security and reliability are multidimensional properties.

---

# 35. “Solved” vs “Mitigated”

Avoid saying a mechanism:

> 解决了某问题

when it only reduces probability, impact, or frequency.

Possible alternatives:

- 缓解
- 降低
- 减少
- 限制
- 避免某一特定场景
- 处理某类失败
- 提供兜底

Use “解决” when the stated scope is actually satisfied.

---

# 36. Reproducibility

When a result matters, readers should be able to understand what conditions produced it.

Depending on the task, include:

- environment
- dependency versions
- input data
- configuration
- commands
- random seeds
- hardware
- expected output

Do not burden simple explanatory articles with unnecessary reproducibility metadata.

Use proportional rigor.

---

# 37. Citations and Source Strength

Prefer evidence roughly in this order when available:

1. specification or standard
2. original paper
3. official documentation
4. official source code
5. official engineering blog
6. high-quality secondary technical source
7. community discussion

The best source depends on the claim.

Examples:

- language semantics → language docs/specification
- implementation behavior → source code
- research result → original paper
- API usage → official docs

Do not cite a source for a stronger claim than the source actually supports.

---

# 38. Source Code as Evidence

When discussing implementation details, source code is often stronger evidence than a secondary article.

When relevant, record:

- repository
- file
- function/class
- commit or version

Avoid treating current source code as a permanent API guarantee unless the behavior is also specified.

---

# 39. Version Sensitivity

Technical facts may change across versions.

Be version-specific when relevant.

Examples:

> Python 3.13

> MySQL 8.0

> PyTorch 2.x

> Linux kernel 6.x

> API version v2

Do not add version numbers when they do not materially affect the explanation.

---

# 40. Avoid Ambiguous Pronouns

When several objects, modules, models, or variables are in scope, words such as:

- 它
- 这个
- 该对象
- 这里
- 前者
- 后者

may become ambiguous.

Repeat the technical noun if necessary.

Clarity is more important than avoiding repetition.

---

# 41. One Sentence, One Main Claim

Avoid packing multiple independent technical conclusions into one long sentence.

Bad pattern:

> A 会导致 B，而且 C 的原因是 D，所以 E 一般是 O(n)，同时它也能解决 F。

Split independent claims and show their relationships explicitly.

A long sentence is acceptable when all clauses serve one coherent claim.

---

# 42. Separate What, Why, and How

For important technical concepts, distinguish:

- What: what the concept is
- Why: what problem it addresses
- How: how it works
- Implementation: how the current system realizes it
- Evaluation: how effectiveness is measured

Do not mix all five into one paragraph when the distinction matters.

---

# 43. Explain Mechanism Before Recommendation

Avoid unsupported recommendations such as:

> 所以应该使用 deepcopy。

Explain why:

> 普通赋值会让结果和输入共享嵌套可变对象，而题目要求返回结果后不能通过结果修改原始输入。因此，对于直接保留的复合值，需要构造独立副本；在当前实现中可以使用 `copy.deepcopy()`。

Recommendation should follow from constraints.

---

# 44. Edge Cases and Boundaries

When an explanation or algorithm relies on type, input, or environment constraints, state important edge cases.

Possible examples:

- empty input
- `None`
- duplicate elements
- negative values
- very deep recursion
- cycles
- shared references
- integer overflow
- Unicode text
- concurrent mutation
- malformed input

Do not enumerate every imaginable edge case.

Focus on cases that challenge the core reasoning.

---

# 45. Negative Claims

Statements of impossibility have high proof obligations.

Examples:

- 不可能
- 无法
- 绝不会
- 不存在

Ask whether the statement means:

- impossible by specification;
- impossible under current assumptions;
- unsupported by current implementation;
- merely difficult or impractical.

Prefer scoped wording.

---

# 46. Necessary vs Sufficient Conditions

Do not confuse:

- necessary condition
- sufficient condition
- necessary and sufficient condition

Example:

> 使用锁可能是避免某类竞争条件的手段，但“使用了锁”本身并不自动充分保证整个系统线程安全。

When the distinction matters, state it explicitly.

---

# 47. Local Optimality vs Global Optimality

Do not use:

> 最优

without specifying:

- objective
- constraints
- search space
- proof or benchmark basis

Examples:

> 在当前 benchmark 上得分最高

is not equivalent to:

> 最优方法

Similarly:

> greedy chooses the locally best option

does not imply:

> greedy produces the globally optimal solution

without a correctness argument.

---

# 48. Trade-Offs

Engineering design usually involves trade-offs.

Avoid presenting one dimension of improvement as an unqualified overall improvement.

Example:

> 增加缓存可以降低重复计算延迟，但会引入额外内存占用和缓存一致性问题。

When recommending a design, consider:

- latency
- throughput
- memory
- complexity
- maintainability
- reliability
- consistency
- cost
- operational burden

Only include dimensions relevant to the problem.

---

# 49. Failure Modes

For important systems, explain what happens when components fail.

Questions may include:

- What if the tool times out?
- What if retrieval returns nothing?
- What if the database is unavailable?
- What if parsing fails?
- What if the model returns malformed arguments?
- What if retry is not idempotent?

Do not describe the happy path as the entire system.

---

# 50. Review Protocol

When reviewing technical rigor, inspect the document in this order:

1. Check whether the main technical conclusion is correct.
2. Check whether the implementation matches the stated rules.
3. Check assumptions and specification ambiguity.
4. Check definitions and terminology.
5. Check causal claims.
6. Check complexity claims.
7. Check analogies and intuition.
8. Check experiments and metrics.
9. Check implementation-specific claims.
10. Check edge cases and failure modes.
11. Check whether wording is stronger than evidence.
12. Only then focus on local wording improvements.

---

# 51. High-Risk Claim Checklist

Search for or mentally inspect terms such as:

- 一定
- 必然
- 显然
- 本质上
- 完全
- 所有
- 任何
- 永远
- 唯一
- 最优
- 显著
- 证明
- 保证
- 解决
- 不可能
- 无需
- 很快
- 很大
- 很强
- 很好

For each occurrence, ask:

- Is the statement true?
- Is the scope clear?
- Is the evidence sufficient?
- Is a weaker term more accurate?
- Can a number or mechanism replace the adjective?

---

# 52. Final Rigor Checklist

Before declaring a technical article rigorous enough for publication, verify:

## Claims

- [ ] Important claims are technically correct.
- [ ] Claim strength matches the evidence.
- [ ] Universal statements are genuinely universal within the stated scope.
- [ ] Negative claims have sufficient justification.

## Assumptions and Scope

- [ ] Important assumptions are explicit.
- [ ] Specification ambiguity is disclosed.
- [ ] Version or implementation scope is stated when relevant.
- [ ] Conclusions do not silently exceed the evaluated scope.

## Definitions

- [ ] Definitions are not confused with implementations.
- [ ] Local definitions are labeled as local.
- [ ] Analogies are not presented as exact equivalence.
- [ ] Intuition is separated from formal explanation when necessary.

## Reasoning

- [ ] Important conclusions include the actual reason.
- [ ] “显然” or similar wording does not hide missing steps.
- [ ] Examples are not treated as proofs.
- [ ] Tests are not treated as exhaustive verification.
- [ ] Necessary and sufficient conditions are not confused.

## Complexity

- [ ] Input-size variables are defined.
- [ ] Operation-cost assumptions are explicit when relevant.
- [ ] Hidden library/container costs are considered.
- [ ] Equality, hashing, sorting, copying, and canonicalization costs are considered where relevant.
- [ ] Average and worst case are distinguished.
- [ ] Output, auxiliary, and recursion-stack space are handled consistently.
- [ ] Big-O is not presented as direct wall-clock performance.

## Experiments

- [ ] Observations are separated from causal conclusions.
- [ ] Important environment and configuration details are available.
- [ ] Metrics and baselines are clear.
- [ ] Percentage points and relative percentages are distinguished.
- [ ] “显著” is used only with a clear meaning.

## Systems

- [ ] Language semantics and implementation details are separated.
- [ ] Framework, runtime, OS, and network responsibilities are not conflated.
- [ ] Reliability and security claims have concrete scope.
- [ ] Important failure modes are considered where relevant.

---

# Core Principle

A rigorous technical statement should make its own boundary visible.

The reader should be able to tell:

> Under these assumptions, for this system or input model, because of these mechanisms or observations, this conclusion follows.

Anything stronger requires stronger evidence.