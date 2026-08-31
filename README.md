# Technical Writing Skill

[English](README.en.md)

面向技术内容的写作、改写与审阅 Skill。它适用于技术博客、学习笔记、算法讲解、源码分析、项目文档和面试复盘，覆盖代码、数学、复杂度、图表、实验、系统等主题。

## 安装

在终端执行以下命令，将本仓库安装到 Codex 的个人 Skill 目录：

```bash
git clone https://github.com/KevinBarrus/technical-writing.git \
  ~/.codex/skills/technical-writing
```

重新开启 Codex 会话后即可使用。更新已安装的 Skill：

```bash
git -C ~/.codex/skills/technical-writing pull --ff-only
```

如果目标目录已存在，请先执行更新命令；不要再次 `git clone` 到同一路径。

同理，如果你使用的是 ClaudeCode，那么安装命令为：

```bash
git clone https://github.com/KevinBarrus/technical-writing.git \
  ~/.claude/skills/technical-writing
```

对于 Pi/Hermes/OpenCode 也同理。如果你想要为所有 Agent 都安装这个 Skill，那么安装命令为：

```bash
git clone https://github.com/KevinBarrus/technical-writing.git \
  ~/.agents/skills/technical-writing
```

## 解决的问题

Skill 以“技术博客的可读性 + 论文式的严谨性”为目标，按以下顺序取舍：

> 正确性 → 严谨性 → 清晰性 → 一致性 → 简洁性 → 呈现

它要求将主张、证据、假设、适用范围和机制明确区分，避免把实验当证明、把实现当定义、把类比当等价，或在未声明成本模型时断言复杂度结论。

## 使用场景

- 撰写或改写中文技术 Markdown。
- 审查算法、源码、系统设计、数据库/网络、Agent/RAG 或机器学习内容。
- 检查代码、公式、复杂度、实验结论、图表和正文是否一致。
- 进行发布前审稿，并按 Critical、Major、Minor、Optional 输出问题。

对于一句话润色、局部格式调整或单个代码片段，Skill 使用局部审阅；只有明确要求完整审稿或发布就绪评估时，才进行全量检查。

## 工作方式

入口文件 [`SKILL.md`](SKILL.md) 定义写作、改写、审阅三种模式，以及局部、技术、发布三个审阅深度。它按任务按需读取参考文件，不会机械加载整套规则。

| 文件 | 用途 |
| --- | --- |
| [`technical-rigor.md`](references/technical-rigor.md) | 主张、证据、假设、因果、系统语义和可复现性。 |
| [`code-and-math.md`](references/code-and-math.md) | 代码、伪代码、公式、数值与复杂度。 |
| [`diagrams.md`](references/diagrams.md) | 图表选型、语义、可读性与审查。 |
| [`style-guide.md`](references/style-guide.md) | 中文技术 Markdown、排版和格式。 |
| [`review-checklist.md`](references/review-checklist.md) | 全文审阅、严重度和发布判断。 |

## 示例请求

```text
检查这篇 RAG 文章的技术正确性；重点核对 Context、Memory 与检索链路的定义。
```

```text
润色这段算法讲解，保留原有结论，并检查复杂度是否遗漏哈希和比较成本。
```

```text
对这份项目文档做发布前审阅，按严重度给出可直接替换的修改建议。
```

## 设计原则

- 不以格式掩盖技术问题。
- 不以完整清单替代按风险审阅。
- 不为显得严谨而无故增加形式化、图表或实验。
- 在读者能复核的地方，优先说明机制、条件和证据边界。
