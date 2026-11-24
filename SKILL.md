---
name: unslop-ui-blueprint
description: Enforces non-generic UI architecture, 4-directional spacing, semantic typography, Create/Save (Green), Update (Orange), and Delete (Red) color rules, library-first components with explicit user confirmation before installing/pulling from reference libraries, and zero-filler copy by forking assets/DESIGN.template.md into ./DESIGN.md after clarifying doubts first.
---

# Unslop UI Blueprint

1. Inspect the repository's existing codebase, dependencies, Tailwind config, and CSS variables before acting.
2. If there are any doubts, missing brand tokens, or conflicting requirements, ask concise clarifying questions first and wait for explicit approval before creating `./DESIGN.md` or modifying UI code.
3. Once approved, copy `assets/DESIGN.template.md` into `./DESIGN.md`, replace every `TBD` slot with project-specific values derived from the repo, and ask for explicit user confirmation before installing packages or pulling components from reference libraries.
4. Keep user-facing UI copy and developer-facing responses free of filler - output code and concise tables only.