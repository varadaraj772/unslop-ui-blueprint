# unslop-ui-blueprint

Agent skill and `./DESIGN.md` contract template for enforcing consistent, non-generic frontend UI across repositories.

## Repository Structure

```text
unslop-ui-blueprint/
├── README.md
├── SKILL.md
└── assets/
    └── DESIGN.template.md
```

## Core Rules

- **Ask First & Confirm:** Inspects existing codebase tokens, config, and dependencies; asks clarifying questions on ambiguities; waits for approval before creating `./DESIGN.md`, modifying UI, installing packages, or pulling reference components.
- **Spacing & Layout:** `4px` spacing scale, four-directional symmetry (`top`, `right`, `bottom`, `left`), consistent section gutters, equal-height grid cards, and responsive layouts across `390px` mobile, `768px` tablet, and `1280px+` desktop.
- **Typography & Copy:** Semantic hierarchy (`Hero`, `Title`, `Subtitle`, `Body`, `Caption / Meta`, `Label / Action`), standard hyphens (`-`) instead of em/en dashes, and zero filler text in UI copy or developer output.
- **Forms & Selection Controls:** Explicit labels, required (`*`) indicators, `>= 4.5:1` placeholder contrast, library calendar/popover date pickers (no native `<input type="date">`), and strict separation of `Checkbox`, `RadioGroup`, `Switch`, and `Select` / `Command`.
- **Action & CRUD Colors:** One primary action per view/section, no buried or duplicate primary CTAs, and default CRUD/Save color semantics (`Create/Save` = Green, `Update` = Orange, `Delete` = Red).
- **Hard Bans:** No inline `<svg>` icons (use library icon packages), no custom reinvention of existing library primitives, no decorative badges or pulsing live dots, and no raw hexes or arbitrary pixel brackets.

## Setup

1. Clone `https://github.com/varadaraj772/unslop-ui-blueprint` into your agent skills directory.
2. Let the agent inspect the target repository and confirm tokens, dependencies, and `./DESIGN.md` customization with you.
3. Fork `assets/DESIGN.template.md` into `./DESIGN.md` at the repository root and replace `TBD` slots for the target project (`Persuade` or `Operate`).

## Support

If you find this useful, you can support it at [buymeacoffee.com/varadaraj2f](https://buymeacoffee.com/varadaraj2f).
