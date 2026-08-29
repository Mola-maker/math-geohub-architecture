# Math GeoHub provenance

These skills generalize architecture decisions from the public [Math GeoHub repository](https://github.com/Mola-maker/mathhub). The reusable principles are primarily documented in:

- [Math GeoHub TikZ Semantic Kernel v5](https://github.com/Mola-maker/mathhub/blob/main/docs/superpowers/specs/2026-08-01-tikz-semantic-kernel-v5-architecture.md): five independent support lanes, source/construction/rendering truth, `GeometryDoc`, typed triad transactions, exact execution, and failure semantics.
- [TikZ Studio v3 architecture](https://github.com/Mola-maker/mathhub/blob/main/docs/superpowers/specs/2026-07-27-tikz-studio-v3-architecture-design.md): the interactive/exact renderer split, compiler job lifecycle, deployment boundary, and performance budgets.
- [Agentic code-editor architecture for the TikZ triad](https://github.com/Mola-maker/mathhub/blob/main/docs/superpowers/research/2026-08-16-agentic-code-editor-triad-architecture.md): durable agent events, revision-bound semantic intents, broker replay, and post-commit verification.
- [Project rules](https://github.com/Mola-maker/mathhub/blob/main/AGENTS.md): the operational form of the source-truth, direct-manipulation, compiler-isolation, and deployment boundaries.

Do not imply that the source project endorses a different product, renderer, protocol, or library merely because this skill applies the same design principles there.
