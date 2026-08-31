# Technical Writing Review Checklist

## Purpose

Define a complete review procedure for technical writing.

This checklist is used after writing or rewriting technical content, or when the user explicitly asks for review, proofreading, publication readiness, technical validation, or quality assessment.

The review process should prioritize substantive correctness before typography.

The goal is not to maximize the number of detected issues.

The goal is to determine whether the document is:

- technically correct
- logically rigorous
- internally consistent
- understandable
- reproducible where relevant
- stylistically consistent
- ready for its intended audience and publishing medium

---

# 1. Core Principle

Review in descending order of consequence.

Use this priority:

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

Do not polish punctuation before resolving a technical error that changes the conclusion.

Do not spend review effort equally across all categories.

Prioritize issues according to how much they affect:

- correctness
- reader understanding
- reproducibility
- implementation
- conclusions

---

# 2. Review Modes

The review procedure may operate in different scopes.

## 2.1 Full Review

Use when the user asks for:

- 完整检查
- 全面审查
- publication-ready review
- 技术博客审稿
- 论文式检查
- 最终检查
- 发布前检查

A full review should inspect every major category in this document.

---

## 2.2 Technical Review

Use when the user primarily asks whether the technical content is correct.

Prioritize:

- correctness
- assumptions
- definitions
- reasoning
- complexity
- code behavior
- experiments
- system semantics

Do not spend excessive time on punctuation unless it causes ambiguity.

---

## 2.3 Style Review

Use when the user explicitly asks only for:

- Markdown 格式
- 排版
- 标点
- 空格
- 文风
- 标题
- typography

Do not unnecessarily reopen settled technical conclusions unless a visible technical error is discovered.

---

## 2.4 Focused Review

If the user names a specific concern, review that concern first.

Examples:

- “检查复杂度分析”
- “看看反引号使用”
- “检查 Mermaid 图”
- “看看这个结论严不严谨”
- “检查代码有没有 bug”

Do not mechanically perform a full-document review when the requested scope is narrow unless a severe unrelated issue is discovered.

---

# 3. Severity Levels

Classify issues by consequence.

Use:

- Critical
- Major
- Minor
- Optional

Do not inflate severity merely to make the review appear thorough.

---

# 4. Critical

A Critical issue means the current document contains an error that can invalidate the implementation, explanation, experiment, or main conclusion.

Examples include:

- algorithm is incorrect
- code does not implement the stated specification
- formula is fundamentally wrong
- security guidance creates a serious vulnerability
- experiment uses test data during training while claiming unbiased evaluation
- system explanation reverses protocol semantics
- a central claim contradicts the actual source or implementation
- published command can destroy or corrupt user data unexpectedly
- complexity claim is used to justify a conclusion but is fundamentally based on the wrong algorithm

Critical issues should be fixed before publication.

---

# 5. Major

A Major issue does not necessarily invalidate the whole document but materially weakens correctness, rigor, or reader understanding.

Examples include:

- important assumption is missing
- specification ambiguity is silently resolved
- claim strength exceeds evidence
- causal conclusion is drawn from a simple correlation
- average-case complexity is presented as unconditional worst-case
- important hidden operation cost is ignored
- terminology changes meaning across sections
- analogy may cause a materially incorrect mental model
- code and prose disagree on an edge case
- experiment lacks a baseline needed to support the conclusion
- architecture diagram misrepresents an important system boundary

Major issues should normally be fixed before publication.

---

# 6. Minor

A Minor issue affects clarity, consistency, or local precision but does not materially change the technical conclusion.

Examples include:

- missing Chinese-English spacing
- incorrect punctuation
- inconsistent capitalization
- heading numbering inconsistency
- one code identifier missing backticks
- inconsistent unit formatting
- an ambiguous local pronoun
- slightly unclear sentence structure
- code fence language identifier is suboptimal but still understandable
- figure reference uses “如下图” instead of an explicit figure number

Minor issues may be fixed during final proofreading.

---

# 7. Optional

An Optional issue is a stylistic preference whose correction is not required for technical quality.

Examples include:

- alternative heading wording
- optional diagram redesign
- preference for one valid term over another
- sentence shortening where the original is already clear
- visual-polish suggestions
- optional examples
- optional section reordering

Do not present Optional suggestions as defects.

If the document is already publication-ready, Optional issues should not prevent approval.

---

# 8. Severity Decision Rule

When deciding severity, ask:

1. Does this change technical meaning?
2. Could it cause incorrect implementation?
3. Could it cause the reader to learn the wrong mechanism?
4. Does it invalidate a conclusion?
5. Does it materially affect reproducibility?
6. Does it materially weaken the evidence?
7. Is it only local presentation?

A useful rule is:

> Meaning and conclusion → Critical or Major  
> Precision and consistency → Major or Minor  
> Appearance and preference → Minor or Optional

Use judgment rather than applying this mechanically.

---

# 9. Review Output Format

For substantive issues, provide enough information for the writer to fix them directly.

Prefer the structure:

```text
Severity: Major

Location:
Section 4.2, complexity analysis

Original:
“列表去重的时间复杂度为 O(k²)。”

Problem:
该结论隐含假设单次元素相等性比较为 O(1)。对于嵌套 list 或 dict，相等性比较本身可能递归检查内部结构。

Why:
当前写法把成员扫描成本和元素比较成本合并成一个无条件 O(k²) 结论，会让复杂度边界显得过强。

Suggested replacement:
“若暂时将单个元素的相等性比较视为 O(1)，则长度为 k 的列表使用线性成员查询进行稳定去重时，最坏时间复杂度为 O(k²)。对于嵌套复合元素，相等性比较本身还可能产生额外开销。”
```

Do not force this exact verbose format for trivial punctuation issues.

For Minor formatting issues, concise grouped reporting is acceptable.

---

# 10. Do Not Rewrite Without Diagnosis

When reviewing, do not silently replace text without explaining substantive errors.

For a meaningful change, state:

- what is wrong
- why it is wrong
- what the corrected wording should be

For purely local style polishing, direct replacement may be sufficient.

---

# 11. Check the Main Conclusion First

Before inspecting local details, identify the document's central conclusions.

Ask:

- What is the article trying to establish?
- What is the main implementation result?
- What is the main algorithmic claim?
- What is the main experimental conclusion?
- What is the main engineering recommendation?

Verify these before polishing local prose.

A beautifully formatted article with a wrong central conclusion is not publication-ready.

---

# 12. Technical Correctness Checklist

Verify:

- [ ] The central technical claims are correct.
- [ ] The described mechanism matches actual behavior.
- [ ] The implementation matches the stated algorithm.
- [ ] Examples do not contradict the rules.
- [ ] Important edge cases do not invalidate the approach.
- [ ] Language semantics are described correctly.
- [ ] Framework or library behavior is not invented.
- [ ] Protocol responsibilities are not conflated.
- [ ] Experimental conclusions match the data shown.
- [ ] Recommendations follow from the stated constraints.

Any failure in this category may be Critical or Major.

---

# 13. Specification Checklist

Verify:

- [ ] The task or system specification is stated accurately.
- [ ] Conflicting requirements are explicitly identified.
- [ ] Ambiguities are not silently resolved.
- [ ] The adopted interpretation is stated.
- [ ] The reason for choosing that interpretation is stated when important.
- [ ] Alternative interpretations are mentioned when they materially change the solution.
- [ ] Implementation behavior is distinguished from required behavior.

Example review trigger:

> 题目描述说“拼接”，样例却表现为去重。

This should not be silently normalized.

---

# 14. Assumption Checklist

Verify:

- [ ] Important assumptions are explicit.
- [ ] Assumptions appear close to the conclusions they support.
- [ ] Removing an assumption would not silently invalidate the analysis.
- [ ] Cost-model assumptions are stated.
- [ ] Environment assumptions are stated where relevant.
- [ ] Version assumptions are stated where relevant.
- [ ] Experimental assumptions are clear.

Common hidden assumptions include:

- average $O(1)$ hash lookup
- constant-time equality comparison
- no network failure
- single-process execution
- no concurrent mutation
- fixed framework version
- deterministic preprocessing

---

# 15. Claim Strength Checklist

Search for high-risk wording such as:

- 一定
- 必然
- 显然
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
- 本质上
- 无需
- 总是
- 从不
- 很快
- 很强
- 很好

For each occurrence, verify:

- [ ] Evidence supports the strength.
- [ ] Scope is visible.
- [ ] Important exceptions are absent or acknowledged.
- [ ] A weaker phrase would not be more accurate.
- [ ] A measurable quantity could not replace a vague adjective.

Do not mechanically flag every occurrence.

---

# 16. Definition Checklist

Verify:

- [ ] Important terms are defined before being used ambiguously.
- [ ] Local definitions are labeled as local.
- [ ] Definition is not confused with implementation.
- [ ] Project-specific terminology is not presented as universal.
- [ ] Related terms are distinguished when readers could confuse them.
- [ ] Terms retain the same meaning throughout the article.

Examples that often require distinction:

- Context vs Memory
- model vs Agent
- specification vs implementation
- process vs thread
- shallow copy vs deep copy
- concurrency vs parallelism
- cache vs persistence

---

# 17. Terminology Consistency Checklist

Verify:

- [ ] The same component uses the same name throughout.
- [ ] Capitalization is stable.
- [ ] Chinese and English translations are consistent.
- [ ] Abbreviations are introduced consistently.
- [ ] Code names and prose names match.
- [ ] Diagram labels match prose terminology.
- [ ] No term changes meaning silently.

Example:

Do not alternate among:

```text
Tool Manager
Tool Registry
工具注册中心
工具管理器
```

if all four refer to exactly the same component.

Choose one primary term and define aliases only when necessary.

---

# 18. Reasoning Checklist

Verify:

- [ ] Important conclusions include their actual reasoning.
- [ ] “显然” does not replace a missing step.
- [ ] Examples are not treated as proofs.
- [ ] Passing tests is not treated as exhaustive verification.
- [ ] Necessary conditions are not confused with sufficient conditions.
- [ ] Local optimality is not confused with global optimality.
- [ ] Recommendations follow from constraints.
- [ ] Trade-offs are acknowledged where relevant.
- [ ] Counterexamples have been considered for strong claims.

---

# 19. Analogy Checklist

Verify:

- [ ] Analogy is labeled as intuition rather than exact equivalence.
- [ ] The analogy explains a useful relationship.
- [ ] Important limitations are stated.
- [ ] A beginner is unlikely to mistake the analogy for the actual language or system semantics.
- [ ] The formal explanation appears when the distinction matters.

Example:

Prefer:

> 可以把 Python 变量名近似理解为指向对象的引用……

rather than:

> Python 变量就是 C++ 指针。

---

# 20. Causality Checklist

Verify:

- [ ] Correlation is not presented as causation without evidence.
- [ ] Experimental variables are controlled where causal language is used.
- [ ] Alternative explanations are considered.
- [ ] Single-run observations are not generalized too aggressively.
- [ ] “导致” and “因为” are justified.
- [ ] Observational evidence uses appropriately bounded wording.

Prefer:

> 在本次实验中观察到……

when causality has not been established.

---

# 21. Complexity Checklist

Verify:

- [ ] Input-size variables are defined.
- [ ] Multiple dimensions use distinct variables.
- [ ] Primitive-operation assumptions are visible.
- [ ] Visible loops are not the only operations analyzed.
- [ ] Container operations are considered.
- [ ] Equality comparison cost is considered.
- [ ] Hash computation cost is considered.
- [ ] Sorting cost is considered.
- [ ] Copying cost is considered.
- [ ] Serialization or canonicalization cost is considered where relevant.
- [ ] Recursive call count is distinguished from recursion depth.
- [ ] Average and worst case are distinguished.
- [ ] Output space and auxiliary space are distinguished where useful.
- [ ] Recursion-stack space is considered.
- [ ] Big-O is not equated directly with wall-clock speed.

---

# 22. Complexity Conclusion Proximity

Important assumptions should appear near the complexity conclusion.

Avoid:

> 时间复杂度为 $O(k^2)$。

followed several sections later by:

> 这里其实是假设比较操作为常数时间。

Prefer:

> 若将单次元素比较视为 $O(1)$，则该列表判重过程的最坏时间复杂度为 $O(k^2)$。

Readers should not need to discover hidden assumptions later.

---

# 23. Optimization Checklist

Verify:

- [ ] The optimization target is explicitly identified.
- [ ] The optimized operation is distinguished from the entire algorithm.
- [ ] New preprocessing costs are counted.
- [ ] New memory costs are counted.
- [ ] Hashability constraints are considered.
- [ ] Canonicalization cost is considered where relevant.
- [ ] Sorting cost is considered.
- [ ] Collision/equality behavior is considered when important.
- [ ] Improvement claims do not exceed what the analysis supports.

Do not accept:

> 使用 set 后复杂度从 $O(n^2)$ 变为 $O(n)$。

without verifying the full algorithm and data representation.

---

# 24. Correctness Proof Checklist

For algorithms requiring correctness reasoning, verify:

- [ ] The key invariant or property is stated.
- [ ] Initialization is correct.
- [ ] Each update preserves the property.
- [ ] Termination produces the desired result.
- [ ] Boundary conditions are handled.
- [ ] Greedy choices are justified when relevant.
- [ ] Recurrences represent the actual subproblem structure.

Formal proof is not required for every article.

The level of proof should match the difficulty and purpose.

---

# 25. Code Review Checklist

Verify:

- [ ] Code fence language identifiers are correct.
- [ ] Runnable code is syntactically valid.
- [ ] Pseudocode is labeled as pseudocode.
- [ ] Python and JSON syntax are not mixed.
- [ ] Programming operators remain ASCII syntax.
- [ ] Imports are included when needed for the shown code.
- [ ] Undefined helpers are explained.
- [ ] Code matches prose.
- [ ] Code matches examples.
- [ ] Code matches complexity analysis.
- [ ] Important edge cases are handled.
- [ ] Comments explain why rather than narrating every line.
- [ ] Placeholder values are clearly placeholders.
- [ ] Secrets are not exposed.

---

# 26. Code Example Validity

When a code block is described as executable, mentally or actually verify:

- syntax
- imports
- variable definitions
- control flow
- return value
- data types

If execution cannot be verified, avoid claiming:

> 代码可以直接运行。

Use:

> 示例实现如下。

unless confidence is sufficient.

---

# 27. Pseudocode Checklist

Verify:

- [ ] Pseudocode is not falsely labeled as a real language.
- [ ] Control flow is understandable.
- [ ] Important operations are not hidden.
- [ ] Simplification does not invalidate complexity reasoning.
- [ ] Pseudocode terminology matches prose.

Pseudocode may omit boilerplate, but not the mechanism being explained.

---

# 28. Mathematical Notation Checklist

Verify:

- [ ] Mathematical variables use consistent notation.
- [ ] Variables are defined.
- [ ] The same symbol does not have conflicting meanings.
- [ ] LaTeX is used where supported.
- [ ] Mathematical comparison uses mathematical notation.
- [ ] Programming syntax is not mixed into formulas.
- [ ] Equality, assignment, comparison, and definition are distinguished.
- [ ] Logical implication and flow arrows are distinguished.
- [ ] Indexing conventions are clear.
- [ ] Tensor or matrix dimensions are consistent.

---

# 29. Formula Checklist

For each important formula, verify:

- [ ] The formula is correct.
- [ ] Symbols are defined.
- [ ] Assumptions are stated.
- [ ] Units are consistent.
- [ ] Boundary conditions are valid.
- [ ] The surrounding explanation matches the formula.
- [ ] Numerical examples match the formula.
- [ ] The engineering meaning is explained where useful.

A formula should not be treated as self-explanatory.

---

# 30. Numerical Results Checklist

Verify:

- [ ] Reported numbers match the source or experiment.
- [ ] Units are correct.
- [ ] Precision is appropriate.
- [ ] Comparable values use comparable precision.
- [ ] Percentage points and relative percentages are distinguished.
- [ ] Aggregation methods are clear when relevant.
- [ ] Rounding does not change the interpretation.
- [ ] Derived values were recomputed after formula changes.

---

# 31. Experimental Result Checklist

Verify:

- [ ] Dataset is identified.
- [ ] Split strategy is known when relevant.
- [ ] Evaluation metric is defined.
- [ ] Baseline is appropriate.
- [ ] Model/configuration is identifiable.
- [ ] Experimental variables are controlled sufficiently for the conclusion.
- [ ] Random seed or repeated runs are discussed when variance matters.
- [ ] Hardware is documented when performance is reported.
- [ ] Framework/version is documented when relevant.
- [ ] Test data is not improperly used for model selection.
- [ ] Claim scope matches the experiment scope.

Not every article needs every field.

Require the information necessary to support the specific claim.

---

# 32. Statistical Language Checklist

Verify:

- [ ] “显著” has a defined meaning.
- [ ] Statistical significance is not implied without statistical analysis.
- [ ] Practical significance is expressed with magnitude where possible.
- [ ] Variance or uncertainty is considered when relevant.
- [ ] One measurement is not presented as a stable distributional property.

Prefer concrete numbers over vague adjectives.

---

# 33. Benchmark Checklist

Verify:

- [ ] Benchmark name is clear.
- [ ] Metric is clear.
- [ ] Baseline is clear.
- [ ] Evaluation conditions are comparable.
- [ ] Model versions are known when relevant.
- [ ] Prompting or inference settings are comparable where relevant.
- [ ] The conclusion does not exceed what the benchmark measures.

Avoid:

> 模型 A 全面优于模型 B。

when only one metric was compared.

---

# 34. Performance Checklist

Verify:

- [ ] Latency metric is specified, such as P50 or P99.
- [ ] Throughput units are explicit.
- [ ] Hardware/environment is known when necessary.
- [ ] Warm-up behavior is considered where relevant.
- [ ] Cache state is considered.
- [ ] Input size/distribution is known.
- [ ] Measurement duration or sample size is sufficient.
- [ ] Big-O claims are separated from measured speed.

Avoid vague claims such as:

> 性能非常高。

Prefer measurements.

---

# 35. Backend and Systems Checklist

Verify:

- [ ] Process and thread semantics are not conflated.
- [ ] Local and distributed behavior are distinguished.
- [ ] Concurrency assumptions are visible.
- [ ] Lock scope is clear.
- [ ] Retry behavior is clear.
- [ ] Idempotency is considered where needed.
- [ ] Failure behavior is described.
- [ ] Persistence semantics are clear.
- [ ] Ordering guarantees are not assumed without support.
- [ ] Consistency model is not oversimplified.

---

# 36. Database Checklist

Verify:

- [ ] Database engine is specified when behavior is engine-specific.
- [ ] SQL semantics and optimizer behavior are distinguished.
- [ ] Logical transaction semantics and storage-engine implementation are distinguished.
- [ ] Isolation level is clear where relevant.
- [ ] Locking and MVCC are not conflated.
- [ ] Index behavior is described accurately.
- [ ] Query-plan assumptions are not presented as guarantees.
- [ ] Replication behavior is scoped where relevant.

---

# 37. Network Checklist

Verify:

- [ ] TCP, IP, HTTP, TLS, DNS, and application responsibilities are not conflated.
- [ ] Packet/message/request terminology is used correctly.
- [ ] Connection establishment and application protocol behavior are distinguished.
- [ ] NAT, routing, VPN, tunnel, and proxy semantics are not mixed.
- [ ] Failure or timeout behavior is not oversimplified.
- [ ] Deployment-specific behavior is distinguished from protocol semantics.

---

# 38. Agent Checklist

Verify:

- [ ] Agent terms have operational meanings.
- [ ] Model and Agent are distinguished.
- [ ] Runtime behavior is distinguished from model behavior.
- [ ] Tool execution is not anthropomorphized.
- [ ] Context and Memory are distinguished when relevant.
- [ ] Planning describes an actual mechanism.
- [ ] Reflection describes an actual feedback step.
- [ ] Observation is connected to execution output.
- [ ] Tool Call and Tool Result flow is correct.
- [ ] Retry/replanning/fallback behavior is described mechanically.

Avoid:

> Agent 发现自己错了。

Prefer:

> Validation 失败后，Runtime 将错误信息作为 Observation 回注模型，并触发下一轮规划。

---

# 39. RAG Checklist

Verify:

- [ ] RAG is not reduced to vector search.
- [ ] Ingestion and online retrieval are distinguished.
- [ ] Chunking method is described where relevant.
- [ ] Retrieval strategy is clear.
- [ ] Reranking is distinguished from retrieval.
- [ ] Retrieval depth is known where metrics depend on it.
- [ ] Evaluation metric is appropriate.
- [ ] Retrieval quality is not automatically equated with answer quality.
- [ ] Baselines are comparable.

---

# 40. Deep Learning Checklist

Verify:

- [ ] Architecture is described correctly.
- [ ] Objective function matches implementation.
- [ ] Optimizer is distinguished from loss.
- [ ] Training and inference behavior are distinguished.
- [ ] Tensor shapes are correct where relevant.
- [ ] Dataset split is methodologically sound.
- [ ] Evaluation metric is appropriate.
- [ ] Claims about “learning” are not more mechanistic than evidence supports.
- [ ] Hyperparameters needed for reproduction are available where relevant.

---

# 41. Reproducibility Checklist

When reproducibility matters, verify:

- [ ] Environment is documented.
- [ ] Dependency versions are available.
- [ ] Required commands are provided.
- [ ] Input data is identifiable.
- [ ] Configuration is available.
- [ ] Random seed is recorded where relevant.
- [ ] Hardware is documented where relevant.
- [ ] Expected output or metric is known.
- [ ] External services or APIs are identified.

Do not require excessive reproducibility metadata for a simple conceptual article.

Use proportional rigor.

---

# 42. Diagram Checklist

Verify:

- [ ] Diagram type matches the information.
- [ ] ASCII and Unicode diagrams are named correctly.
- [ ] Text diagrams use a `text` fence.
- [ ] Arrows have clear semantics.
- [ ] Arrow direction is correct.
- [ ] Node labels match prose.
- [ ] Abstraction level is consistent.
- [ ] System boundaries are visible where relevant.
- [ ] Internal and external systems are distinguishable.
- [ ] Edge crossings are not excessive.
- [ ] Diagram remains readable at normal size.
- [ ] Mermaid has not become overloaded with layout hacks.
- [ ] Complex architecture has been escalated to a more suitable tool where needed.
- [ ] Important figures are numbered and referenced.
- [ ] Editable source is preserved when appropriate.

---

# 43. Markdown Checklist

Verify:

- [ ] Heading hierarchy is continuous.
- [ ] Heading numbering is consistent.
- [ ] Heading markers contain a space.
- [ ] List markers contain a space.
- [ ] Adjacent block elements use exactly one blank line.
- [ ] Multiple blank lines are not used to create hierarchy.
- [ ] Code fences are balanced.
- [ ] Code fences use correct language identifiers.
- [ ] Tables render correctly.
- [ ] Links use meaningful anchor text.
- [ ] Important code entities use inline code.
- [ ] Ordinary concepts are not backticked unnecessarily.

---

# 44. Chinese Typography Checklist

Verify:

- [ ] Chinese sentences use Chinese punctuation.
- [ ] Chinese-English spacing is consistent.
- [ ] Chinese-number spacing is consistent.
- [ ] No space appears before Chinese punctuation.
- [ ] Chinese parentheses are used in Chinese prose.
- [ ] `%` has no preceding space.
- [ ] Units use appropriate spacing.
- [ ] Numeric ranges use `–` where appropriate.
- [ ] Chinese ellipsis uses `……`.
- [ ] `/` and `\` are not used as enumeration separators.
- [ ] `→` is used for conceptual flow rather than programming syntax.

---

# 45. Inline Code Checklist

Verify concrete program entities such as:

- variables
- functions
- methods
- classes
- attributes
- parameters
- files
- paths
- commands
- environment variables
- literal expressions

Use backticks where appropriate.

Verify ordinary concepts such as:

- Agent
- RAG
- Memory
- Context
- shallow copy
- deep copy

are not wrapped in backticks merely for emphasis.

---

# 46. Heading Checklist

Verify:

- [ ] One H1 is used when appropriate.
- [ ] Heading levels are not skipped.
- [ ] Numbering format is consistent.
- [ ] Headings normally have no ending punctuation.
- [ ] Technical headings are descriptive.
- [ ] Conversational headings are used intentionally rather than accidentally.
- [ ] Code entities in headings use backticks where appropriate.

---

# 47. Paragraph Checklist

Verify:

- [ ] Each paragraph has one coherent purpose.
- [ ] Sentences do not contain too many independent claims.
- [ ] Important antecedents are unambiguous.
- [ ] Paragraphs are not artificially fragmented.
- [ ] Transitions are used only where they help.
- [ ] Repetition is functional rather than accidental.
- [ ] Definitions, mechanism, implementation, and evaluation are not unnecessarily collapsed into one paragraph.

---

# 48. Language Style Checklist

Avoid excessive use of:

- 首先
- 其次
- 然后
- 再然后
- 最后
- 我们知道
- 显然
- 众所周知
- 可以看到
- 很容易发现

when structure already makes the relationship clear.

These expressions are not forbidden.

Use them only when they contribute meaning.

Prefer mechanism and evidence over rhetorical filler.

---

# 49. Reference Checklist

Verify:

- [ ] Important factual claims use appropriate sources where needed.
- [ ] Primary sources are preferred for primary claims.
- [ ] Language semantics use official docs/specification where practical.
- [ ] Research claims use original papers where possible.
- [ ] Implementation claims use source code or official implementation documentation.
- [ ] Source scope matches claim scope.
- [ ] A source is not cited for a stronger claim than it supports.
- [ ] Version-sensitive references are sufficiently current.

---

# 50. Source Hierarchy

When several sources are available, roughly prefer:

1. Specification or standard
2. Original paper
3. Official documentation
4. Official source code
5. Official engineering blog
6. High-quality secondary technical source
7. Community discussion

This hierarchy is contextual.

For implementation details, source code may be more relevant than general documentation.

For API guarantees, specification or official documentation may be stronger than source code.

---

# 51. Cross-Section Consistency

After reviewing individual sections, check the document globally.

Verify:

- [ ] The same variable has the same meaning everywhere.
- [ ] Terminology is stable.
- [ ] Earlier assumptions are not contradicted later.
- [ ] Complexity conclusions match optimization sections.
- [ ] Examples match final code.
- [ ] Diagrams match prose.
- [ ] Tables match surrounding analysis.
- [ ] Conclusions match the evidence presented.
- [ ] The final summary does not introduce stronger claims than the main body.

Global inconsistency is often more serious than local wording problems.

---

# 52. Cross-Artifact Consistency

If the technical content includes multiple artifacts, compare them.

Possible artifacts include:

- prose
- source code
- README
- architecture diagram
- benchmark table
- configuration
- API example
- CLI command
- screenshot

Verify that they describe the same system and version.

Do not assume the newest-looking artifact is correct.

---

# 53. Review Original vs Revised Text

When reviewing a revision, check whether the edit introduced new errors.

Common regression patterns include:

- fixing prose but breaking technical meaning
- changing variable names inconsistently
- updating code without updating complexity
- updating numbers without updating conclusions
- updating diagram labels without updating prose
- strengthening wording unintentionally

A revision should be reviewed as a new technical artifact.

---

# 54. Avoid Silent Technical Rewrites

When operating in Rewrite Mode, do not silently change technical claims merely to make the prose sound better.

If the original statement is wrong or unsupported:

1. identify the problem
2. explain the issue
3. provide corrected wording

Do not disguise a technical correction as simple copy editing.

---

# 55. Group Repetitive Minor Issues

Do not report the same typography issue dozens of times individually.

Instead of:

```text
Minor: 第 10 行缺少空格
Minor: 第 18 行缺少空格
Minor: 第 23 行缺少空格
...
```

prefer:

> Minor：全文存在多处中文与英文之间缺少半角空格的问题，例如……建议统一按 `style-guide.md` 批量修正。

List representative examples.

This keeps review output actionable.

---

# 56. Do Not Group Distinct Major Issues

Do not over-compress substantively different problems.

For example, these should normally be separate:

- complexity assumption missing
- `deepcopy()` semantics overstated
- experiment conclusion has causal overreach

Each requires different reasoning and correction.

---

# 57. Avoid Invented Problems

Do not invent a defect merely because a review is expected to contain criticism.

A technically correct and well-written sentence does not need to be rewritten.

Do not convert valid stylistic variation into fake errors.

Examples:

- a clear question-style heading may be acceptable
- a simple diagram may not need redesign
- a short paragraph may not need expansion
- a valid term may not need replacement

Review quality is not measured by issue count.

---

# 58. Preserve Author Intent

When suggesting revisions, preserve:

- intended audience
- teaching style
- technical depth
- article purpose
- level of formality
- project terminology

Do not transform a practical engineering blog into academic-paper prose unless the user requested that style.

Do not remove useful intuition merely because it is informal.

Improve rigor while preserving readability.

---

# 59. Proportional Rigor

The required rigor depends on the artifact.

Examples:

## Interview Notes

Prioritize:

- correctness
- concise explanation
- complexity
- edge cases
- interview-ready reasoning

## Technical Blog

Prioritize:

- correctness
- mechanism
- readability
- diagrams
- examples
- consistent terminology

## Project Documentation

Prioritize:

- exact behavior
- setup reproducibility
- commands
- interfaces
- architecture
- limitations

## Research-Style Article

Prioritize:

- definitions
- assumptions
- methodology
- experiments
- reproducibility
- citations
- limitations

Do not impose all research-paper conventions on every document.

---

# 60. Publication Readiness Levels

Use one of the following final verdicts.

## Not Ready

Use when:

- Critical issues remain
- multiple Major issues invalidate central reasoning
- implementation and explanation significantly disagree
- conclusions are unsupported

---

## Technically Sound but Needs Revision

Use when:

- central approach is basically correct
- no fatal issue exists
- one or more Major issues remain
- assumptions, complexity, terminology, or experiments need substantive revision

---

## Ready After Minor Proofreading

Use when:

- no Critical issues remain
- no substantive Major issues remain
- only Minor formatting, wording, or consistency issues remain

This means the technical content is effectively settled.

---

## Publication-Ready

Use when:

- technical claims are correct
- assumptions and scope are sufficient
- reasoning is coherent
- terminology is consistent
- code and formulas are correct
- complexity analysis is appropriately scoped
- diagrams are clear where used
- Markdown is consistent
- no important reproducibility information is missing
- remaining suggestions are only Optional

Do not withhold Publication-ready status merely because another valid stylistic rewrite is possible.

---

# 61. Publication-Ready Checklist

Before declaring Publication-ready, verify:

## Technical

- [ ] No Critical issue remains.
- [ ] No substantive Major issue remains.
- [ ] Central conclusions are correct.
- [ ] Important assumptions are visible.
- [ ] Technical terminology is stable.

## Reasoning

- [ ] Important claims are supported.
- [ ] Claim strength is appropriate.
- [ ] Examples are not treated as proofs.
- [ ] Causality is not overstated.
- [ ] Analogies are bounded.

## Code and Math

- [ ] Code matches prose.
- [ ] Code syntax is valid where claimed runnable.
- [ ] Mathematical notation is correct.
- [ ] Variables are defined.
- [ ] Complexity analysis has an explicit enough cost model.

## Experiments

- [ ] Metrics are clear.
- [ ] Baselines are appropriate.
- [ ] Reported numbers are consistent.
- [ ] Scope matches evidence.
- [ ] Reproduction details are sufficient for the claim.

## Structure and Visuals

- [ ] Heading hierarchy is coherent.
- [ ] Diagrams use appropriate tools.
- [ ] Figures match prose.
- [ ] Tables are readable.
- [ ] Visual structure helps rather than obscures reasoning.

## Style

- [ ] Markdown is consistent.
- [ ] Chinese-English typography is consistent.
- [ ] Inline code is used consistently.
- [ ] Units and symbols are consistent.
- [ ] No severe readability issue remains.

---

# 62. Final Review Output

For a full review, prefer the following structure:

```text
## Overall Verdict

Publication-ready / Ready after minor proofreading / Technically sound but needs revision / Not ready

## Critical

No issues.

## Major

1. ...
2. ...

## Minor

1. ...
2. ...

## Optional

1. ...

## Final Assessment

Summarize whether the technical conclusions are trustworthy, what still requires correction, and whether the document can be published.
```

If a severity category contains no issues, say:

> No issues.

Do not invent entries to fill every category.

---

# 63. Concise Review Output

For shorter documents or focused review, a shorter format is acceptable:

```text
结论：Ready after minor proofreading。

Major：无。

Minor：
1. ...
2. ...

其余技术内容未发现实质性问题。
```

Output depth should match document complexity.

---

# 64. Suggested Replacement Rules

When giving replacement wording:

- preserve technical meaning
- preserve surrounding terminology
- preserve article voice
- avoid introducing stronger claims
- avoid adding assumptions that the source does not support
- keep replacements directly copyable

If a correction depends on unknown information, do not fabricate the missing value.

Use a placeholder or explicitly state what must be verified.

---

# 65. Location Precision

Identify issue locations precisely enough for the writer to find them.

Possible references include:

- section heading
- paragraph opening
- code block
- function name
- formula number
- figure number
- table row
- quoted original sentence

Line numbers may be used when available and stable.

Do not depend only on vague descriptions such as:

> 前面有一处。

---

# 66. Contradiction Review

Explicitly search for contradictions.

Common patterns include:

- introduction claims $O(n)$, later section claims $O(n^2)$
- diagram shows async queue, prose describes synchronous call
- text says deep copy, code performs shallow copy
- table reports 84.7%, summary reports 85.7%
- section says no mutation, code mutates input
- abstract claims generality, experiment covers one dataset

Contradictions are often Major or Critical.

---

# 67. Edge-Case Review

Inspect edge cases that challenge the core mechanism.

Possible categories include:

- empty input
- duplicate values
- null values
- deeply nested input
- shared references
- cyclic structures
- maximum/minimum values
- malformed input
- concurrent execution
- timeout
- retry
- partial failure

Do not enumerate every theoretical edge case.

Prioritize those capable of disproving the main claim.

---

# 68. Failure-Mode Review

For system articles, check whether the document explains important failure behavior.

Potential failures include:

- model timeout
- tool timeout
- database failure
- malformed response
- network loss
- retry duplication
- cache miss
- permission denial
- invalid arguments
- missing retrieval result

If the article is only about the happy-path mechanism, failure coverage may be optional.

If reliability is a central claim, failure coverage becomes important.

---

# 69. Security Claim Review

Treat security language carefully.

Search for claims such as:

- 安全
- 防止攻击
- 完全隔离
- 不会泄露
- 权限受控
- 保证安全

Verify the concrete mechanism.

Prefer scoped descriptions such as:

> Tool Executor 在执行前验证参数 Schema，并根据权限策略拒绝未授权工具。

over:

> Tool 系统是安全的。

Security conclusions require explicit threat scope.

---

# 70. Reliability Claim Review

Likewise, inspect:

- 高可用
- 可靠
- 不会失败
- 自动恢复
- 保证成功

Ask:

- failure model?
- timeout?
- retry?
- fallback?
- state persistence?
- recovery semantics?
- metric?

Prefer:

> 连续失败 2 次后进入 30 s 冷却。

over:

> 系统具有完善的熔断机制。

when only the concrete behavior is known.

---

# 71. Source-Based Review

When a source document, paper, specification, repository, or uploaded file is the basis of the article:

- preserve source terminology
- distinguish source claims from interpretation
- do not silently add unsupported details
- verify quoted or paraphrased claims against the source
- state when the source does not support a conclusion

Do not “correct” the source using outside knowledge unless the task explicitly asks for verification or comparison.

---

# 72. Source Conflict Review

If multiple sources disagree:

1. identify the disagreement
2. identify source type and version
3. determine whether the difference is due to version, specification, implementation, or interpretation
4. report the conflict
5. avoid silently choosing one unless a justified basis exists

For example:

> Official documentation describes X, while current source code implements Y.

This distinction may itself be the important result.

---

# 73. Version Review

Search for claims likely to be version-sensitive.

Examples:

- language implementation
- library API
- framework behavior
- model capabilities
- command syntax
- UI procedures
- database optimizer behavior

Verify that version scope is included where needed.

Do not add version qualifiers to timeless concepts unnecessarily.

---

# 74. Review of Tutorials

For step-by-step tutorials, verify:

- [ ] Prerequisites are stated.
- [ ] Commands are in correct order.
- [ ] Placeholders are defined.
- [ ] Expected outputs are clear where useful.
- [ ] Platform-specific differences are stated.
- [ ] Dangerous commands are explained.
- [ ] Later steps do not depend on an unstated earlier action.
- [ ] Screenshots and text instructions agree.
- [ ] Commands remain copyable.

A tutorial can be technically correct yet unusable if prerequisite state is missing.

---

# 75. Review of Interview Write-Ups

Verify:

- [ ] Problem interpretation is explicit.
- [ ] Ambiguities are disclosed.
- [ ] Core idea can be explained concisely.
- [ ] Code is correct.
- [ ] Complexity is appropriately analyzed.
- [ ] Edge cases are identified.
- [ ] Language/runtime subtleties are accurate.
- [ ] Optimization claims are not overstated.
- [ ] The final explanation is interview-ready rather than unnecessarily academic.

---

# 76. Review of Source-Code Analysis

Verify:

- [ ] Repository/version is clear where needed.
- [ ] Functions/classes are named correctly.
- [ ] Call chain matches source.
- [ ] Runtime behavior is distinguished from architectural intent.
- [ ] Source-code evidence supports the interpretation.
- [ ] Current implementation is not presented as an eternal guarantee.
- [ ] Important abstractions are not reduced to one implementation detail.

---

# 77. Review of Project Documentation

Verify:

- [ ] Project purpose is clear.
- [ ] Architecture matches current implementation.
- [ ] Setup instructions work.
- [ ] Dependencies are documented.
- [ ] Commands are correct.
- [ ] Configuration examples are safe.
- [ ] API or CLI behavior is accurate.
- [ ] Limitations are stated.
- [ ] Diagrams match the repository.
- [ ] Metrics are reproducible where claimed.

---

# 78. Review of Algorithm Articles

Verify:

- [ ] Problem definition is precise.
- [ ] Input/output semantics are clear.
- [ ] Algorithm idea is correct.
- [ ] Correctness reasoning exists where needed.
- [ ] Complexity variables are defined.
- [ ] Hidden operation costs are considered.
- [ ] Boundary conditions are covered.
- [ ] Code and derivation agree.
- [ ] Examples demonstrate rather than replace proof.

---

# 79. Review of AI/ML Articles

Verify:

- [ ] Model, Agent, runtime, and tool responsibilities are distinguished.
- [ ] Training and inference are distinguished.
- [ ] Architecture and objective are distinguished.
- [ ] Evaluation protocol is clear.
- [ ] Dataset leakage is absent or disclosed.
- [ ] Metrics are appropriate.
- [ ] Causal claims are bounded.
- [ ] Benchmark claims do not exceed benchmark scope.
- [ ] Terms such as “reasoning”, “memory”, and “learning” have sufficiently clear operational meanings.

---

# 80. Review of Architecture Articles

Verify:

- [ ] System boundary is clear.
- [ ] Major components are correctly identified.
- [ ] Responsibilities are separated.
- [ ] Communication paths are correct.
- [ ] Data flow and control flow are understandable.
- [ ] Persistence is represented.
- [ ] Failure/recovery paths are present when central.
- [ ] Deployment assumptions are stated.
- [ ] Diagram and prose match.
- [ ] Trade-offs are discussed when design choices are recommended.

---

# 81. Final Pass Order

After substantive issues have been resolved, perform the final pass in this order:

1. Terminology consistency
2. Cross-section consistency
3. Code and formula consistency
4. Figure and table consistency
5. Heading hierarchy
6. Markdown block spacing
7. Inline code
8. Chinese-English spacing
9. Punctuation
10. Units and symbols
11. Minor wording
12. Links and references

This pass is for polishing, not reopening settled architecture without reason.

---

# 82. Stop Condition

Stop reviewing when all of the following are true:

- no Critical issue remains
- no substantive Major issue remains
- technical conclusions are correct
- important assumptions are visible
- terminology is stable
- code and formulas match the explanation
- complexity claims are sufficiently scoped
- figures and tables are understandable
- formatting is consistent
- remaining differences are only stylistic preferences

At this point, say that the document is publication-ready or ready after minor proofreading.

Do not continue inventing low-value changes.

---

# 83. Anti-Perfectionism Rule

Rigor is not perfectionism.

A document does not need:

- maximal formalism
- maximal citations
- maximal diagrams
- maximal mathematical notation
- maximal section count
- maximal detail

It needs enough precision for its purpose.

Do not expand a clear explanation merely to make it longer.

Do not replace simple language with academic jargon without technical benefit.

Do not redesign a readable diagram because another tool could make it prettier.

---

# 84. Reviewer Self-Check

Before finalizing a review, ask:

- Did I verify technical correctness before style?
- Did I distinguish facts from preferences?
- Did I overstate any issue?
- Did I invent a problem because I expected to find one?
- Did I preserve the author's intended level and voice?
- Are suggested replacements technically safer than the originals?
- Did I accidentally introduce a new assumption?
- Did I distinguish source-supported content from my own inference?
- Is every Major or Critical issue actually consequential?
- Can the writer act directly on the feedback?

If not, revise the review.

---

# 85. Minimal Publication Decision

If the user asks only:

> 这篇现在能不能发？

do not necessarily return the full checklist.

Return:

1. verdict
2. remaining Critical/Major issues
3. the most important Minor issues
4. whether further polishing is optional

Example:

```text
结论：Ready after minor proofreading。

Critical：无。
Major：无。

Minor：
1. 第 4.2 节复杂度结论前补充“单次元素比较视为 O(1)”的假设。
2. 全文还有少量中文与英文之间缺少空格的问题。

技术内容已经稳定，完成以上两处后即可发布，不需要继续做结构性修改。
```

---

# 86. Review Completion Rule

A review is complete when it answers:

- Is the document technically trustworthy?
- What must be fixed?
- What should be fixed?
- What is merely optional?
- Can it be published now?

If the answer to these questions is clear, do not extend the review merely to appear comprehensive.

---

# Core Principle

A good technical review reduces uncertainty.

It should tell the writer exactly:

> 哪些地方是错的，哪些地方是不严谨的，哪些地方只是格式问题，以及文章现在到底能不能发布。

The reviewer should be strict about correctness and restrained about preference.

Once the document is technically sound, internally consistent, and publication-ready, stop.