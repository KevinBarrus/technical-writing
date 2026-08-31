# Technical Diagram Guide

## Goal

Use the simplest representation that accurately communicates the structure or
behavior a reader needs to inspect. Diagram complexity should follow information
complexity, not an attempt to make an article look professional.

## Choose a representation

| Need | Preferred form |
| --- | --- |
| Mathematical relationship | LaTeX |
| Quantitative comparison or trend | Appropriate chart/plot |
| Small local object, pointer, memory, or request relationship | Unicode text diagram |
| Strict terminal compatibility | ASCII text diagram |
| Simple flow, state, sequence, pipeline, or dependency | Mermaid |
| Dense/formal architecture or reusable exported figure | draw.io or equivalent source-controlled diagram |
| Presentation with progressive reveal | PowerPoint or equivalent |
| UI, branding, or high visual control | Figma or equivalent |
| Automatically generated graph | Graphviz or equivalent |

ASCII contains only ASCII characters; box-drawing characters such as `┌`, `│`,
and `→` make a Unicode text diagram. Put alignment-sensitive text diagrams in a
fenced `text` block, use spaces rather than tabs, avoid emoji, and limit mixed
Chinese/English labels when renderer width could break alignment. Escalate when
manual alignment, crossing edges, long labels, nested groups, legends, zooming,
reuse, or export quality becomes important.

## Diagram semantics

Every diagram should answer one main question and use a consistent abstraction
level. State or visibly encode:

- what nodes represent and which boundaries/groupings they belong to;
- what each arrow means, its direction, and whether it is data, control,
  dependency, request/response, synchronous, asynchronous, success, or failure;
- storage, external systems, trust/deployment boundaries, and legends when they
  materially affect the mechanism;
- whether the view is static structure, execution flow, happy path, failure
  path, before/after comparison, or lifecycle/state transition.

Do not let an arrow crossing resemble a junction. Avoid unexplained color,
decorative screenshots, inconsistent node names, or a diagram that mixes system
context, service topology, component internals, and execution sequence without
clear separation.

## Common forms

- **Flowcharts:** show decision conditions and branch outcomes; do not hide
  error paths that change the described behavior.
- **Sequence diagrams:** preserve actor order, message direction, response,
  synchronous/asynchronous semantics, and significant retries or timeouts.
- **State diagrams:** name states and transition triggers; distinguish terminal,
  error, and retry transitions.
- **Architecture diagrams:** choose one level—system context, container/service,
  component, or execution flow—per figure. Show relevant data stores, external
  dependencies, security/trust boundaries, and deployment boundaries.
- **Data charts:** choose a chart that supports the claimed comparison; label
  axes, units, series, sample/configuration, uncertainty where relevant, and
  avoid scale choices that misrepresent the result.
- **Agent/RAG/ML diagrams:** separate offline and online paths where applicable;
  distinguish model, tool, retrieval, index, context, memory, control loop,
  training, and evaluation instead of using anthropomorphic labels.

## Source, accessibility, and review

Keep editable Mermaid/draw.io/Graphviz/PPT/Figma sources with the article and
version-control them when feasible. Export at readable dimensions and aspect
ratio for the target medium; verify dark/light backgrounds, mobile readability,
caption, figure number/reference, and useful alt text.

Review in order: semantic correctness, abstraction level and boundaries, arrow
meaning/direction, missing failure or async behavior, label readability,
crossings/density, rendering portability, then visual polish. Replace a diagram
when its layout obscures the mechanism; do not preserve an early text diagram
only because it already exists.
