# DESIGN.md - Master Frontend Architecture & UI Contract

> Agent Operating Rule (Read First):
> Before creating or forking ./DESIGN.md or refactoring any UI in a project, inspect the codebase, dependencies, Tailwind config, and CSS variables first. If there are any doubts, ambiguities, missing brand tokens, or conflicting requirements, ask concise clarifying questions first and wait for explicit approval before creating ./DESIGN.md or writing UI code. Once approved, fork this template into ./DESIGN.md at the repository root, replace every TBD block to match the project's domain, brand tokens, and mode (Persuade | Operate), confirm with the user before installing dependencies or pulling components from reference libraries, and output code and concise tables only with zero filler explanations.

---

## 1. Project Identity & Mode (Customize Per Project)

- **Project Name:** `TBD`
- **Primary Mode:** `TBD` (`Persuade` | `Operate`)
- **Target Audience & Context:** `TBD`
- **Aesthetic Direction & Mood:** `TBD`
- **Brand Palette Tokens (CSS Variables / Tailwind - derive from project brand, no arbitrary hexes):**
  - `--bg-canvas`: `TBD`
  - `--bg-surface`: `TBD`
  - `--bg-surface-elevated`: `TBD`
  - `--border-subtle`: `TBD`
  - `--border-strong`: `TBD`
  - `--text-primary`: `TBD`
  - `--text-secondary`: `TBD`
  - `--text-placeholder`: `TBD` (must meet `>= 4.5:1` contrast against `--bg-surface`)
  - `--accent-primary` & `--accent-primary-foreground`: `TBD`
  - `--accent-secondary` & `--accent-highlight`: `TBD`
  - `--state-required`: `TBD` (asterisk & validation border)
  - `--crud-create`: `TBD` (shade of green aligned with project theme)
  - `--crud-update`: `TBD` (shade of orange aligned with project theme)
  - `--crud-delete`: `TBD` (shade of red aligned with project theme)
  - `--state-success` / `--state-warning` / `--state-danger`: `TBD`

---

## 2. Reference Component & Icon Libraries (Confirm Before Use)

Treat these libraries and registries as references only: never install packages, pull registry components, or add dependencies without asking and getting explicit confirmation from the user first. Always check what is already installed in the repository before proposing additions:

1. **Icons (`lucide-react`, `@tabler/icons-react`, `@radix-ui/react-icons`):** Reference for standard UI icons (**zero raw `<svg>` tags** in JSX/TSX; confirm package before installing if missing). Never use sparkle icons unless explicitly requested, and always pick icons that match the exact context of the word, heading, or action.
2. **`shadcn/ui` (`https://ui.shadcn.com`):** Reference for accessible primitives (`Button`, `Input`, `Textarea`, `Select`, `Checkbox`, `RadioGroup`, `Switch`, `Calendar`, `Popover`, `Dialog`, `Sheet`, `Tabs`, `Table`, `Form`, `Skeleton`, `Alert`, `Command`, `Carousel`, `DropdownMenu`).
3. **`Origin UI` (`https://originui.com`):** Reference for form controls, labeled inputs, calendar/date pickers, required-field states, inline validation, search bars, segmented controls, and operational controls.
4. **`Magic UI` (`https://magicui.design`):** Reference for hero sections, bento grids, marquees, number tickers, shimmer CTAs, and social-proof blocks (`Persuade` mode only).
5. **`Aceternity UI` (`https://ui.aceternity.com`):** Reference for feature spotlights, textured backdrops, and showcase cards (`Persuade` mode only, max 1-2 per page).
6. **Drag-and-Drop / Kanban (`@dnd-kit/core` + `@dnd-kit/sortable` or `@hello-pangea/dnd`):** Reference for lists, queues, table rows, galleries, and Kanban boards needing reordering or stage moves.
7. **Optional Review / Design Skill (`impeccable` or project-specific):** Reference only; confirm before invoking or installing if not already active.

---

## 3. Non-Negotiable UI/UX Rules

### 3.1 Four-Directional Spacing, Margins, Padding & Layout Rhythm
- **Strict Spacing Scale:** Only multiples of `4px` (`0`, `4px`, `8px`, `12px`, `16px`, `20px`, `24px`, `32px`, `48px`, `64px` - Tailwind `0`, `1`, `2`, `3`, `4`, `5`, `6`, `8`, `12`, `16`). No arbitrary pixel values (`p-[13px]`, `mt-[7px]`).
- **Four-Directional Symmetry Rule (Top, Right, Bottom, Left):**
  - **Cards & Containers:** Equal padding on all 4 sides (`p-4`, `p-5`, or `p-6`). Only use paired axis padding (`px-*` + `py-*`) when an internal divider or media edge spans full width; never leave one side (`pt`, `pr`, `pb`, `pl`) mismatched against its opposite side.
  - **Page & Section Gutters (Left & Right):** Identical horizontal padding (`px-4 sm:px-6 lg:px-8`) and max-width alignment (`mx-auto w-full max-w-*`) across every section, header, and footer.
  - **Vertical Flow & Margins (Top & Bottom):** Prefer `flex`/`grid` with `gap-*` over scattered `mt-*` / `mb-*` margins. Never leave trailing `mb-*` on the last child inside a padded container. Keep section separation (`py-12 md:py-16` or `space-y-8`) and sibling gaps uniform across peer items.
- **Grid Alignment:** Cards in a grid row share equal height (`h-full flex flex-col`) with the footer/CTA pinned to the bottom (`mt-auto`).

### 3.2 Semantic Typography, Weight Hierarchy & Concise Copy
Size, weight, and word count must reflect what the text means, with zero unnecessary words or filler copy anywhere:

- **Hero (`<h1>` display / primary value proposition):** Largest step (`clamp(2rem, 4vw, 3.5rem)` or `text-3xl sm:text-5xl`), `font-bold` / `font-extrabold`, `tracking-tight`, `leading-[1.1]`.
- **Title (`<h2>` section heading / `<h3>` card or modal title):** `text-xl sm:text-2xl` (sections) or `text-base sm:text-lg` (cards/modals), `font-semibold` / `font-bold`, `--text-primary`, `leading-snug`.
- **Subtitle (Supporting context):** `font-normal` / `font-medium`, `--text-secondary`, `text-sm` or `text-base`, `leading-relaxed` - 1 concise line max, never a multi-sentence paragraph.
- **Body (Core descriptions & data):** `text-sm` or `text-base` (`>= 14px`), `font-normal`, `--text-primary` or high-contrast `--text-secondary`, `leading-normal` / `leading-relaxed`, `max-w-prose`.
- **Caption / Meta (Timestamps, counts, prices, validity tags):** `text-xs`, `font-medium` / `font-normal`, `--text-secondary`, `tabular-nums`.
- **Label / Action (Form `<label>`, button text, table headers, nav links):** `font-medium` / `font-semibold`, `whitespace-nowrap`, 1-3 words max on buttons/tabs.
- **Zero Filler Copy (User-Facing & Developer-Facing):**
  - **User-Facing UI:** Never add helper paragraphs, instructional blurbs, onboarding fluff, redundant subtitles under self-explanatory headings, or verbose empty-state essays. Let labels, values, and actions speak directly.
  - **Developer-Facing Output:** Never add long-winded explanations, code walkthrough essays, or redundant comments. Report changes in terse bullet points or compact tables only.

### 3.3 Form Clarity, Placeholders, Date Pickers, Selection Controls & Required Fields
- **Visible Placeholders:** Every `<input>` and `<textarea>` MUST define an explicit background (`--bg-surface`), visible 1px border (`--border-strong` or `--border-subtle` with clear hover/focus ring), and `placeholder:text-[var(--text-placeholder)]` with **at least 4.5:1 contrast**.
- **Library Date & Time Pickers Only (No Native `type="date"`):** Never use browser-native `<input type="date">`, `<input type="datetime-local">`, or `<input type="time">`. Use structured calendar/popover pickers (`Calendar` + `Popover` with `date-fns`, or reference date pickers) after confirming installation if not already present.
- **Strict Selection Control Separation (Checkbox vs. Radio vs. Switch vs. Select):**
  - **Checkbox (`Checkbox`):** Multi-select options (`0..N` independent choices) or explicit terms/consent acknowledgment - always square (`rounded-sm`), never circular.
  - **Radio Group (`RadioGroup`):** Mutually exclusive single-choice (`1` of `2-5` visible options) - always circular (`rounded-full`).
  - **Switch (`Switch`):** Instant boolean on/off toggle that takes effect immediately without a form submit - never use inside a multi-option list or as a substitute for a checkbox in a submit form.
  - **Select / Combobox (`Select` / `Command`):** Single-choice (or searchable multi-select) from `5+` options - never render checkboxes inside a single-select `Select` dropdown, and never confuse row-selection checkboxes in tables with dropdown triggers.
- **Explicit Labels Always:** Every input, picker trigger, or selection control must have a visible `<label>` above or beside it (`text-sm font-medium`) - never use placeholders as labels, and omit redundant sub-captions below inputs unless showing a validation error.
- **Required Field Highlighting:**
  - Every required field MUST show a visible asterisk (`<span className="text-destructive ml-0.5" aria-hidden="true">*</span>`) inside `<label>`, plus `required` and `aria-required="true"`.
  - Optional fields in mixed forms carry `(optional)` in `--text-secondary`.
  - Validation errors render directly beneath the offending field (`text-xs text-destructive mt-1`) with a `border-destructive` ring.

### 3.4 Action Hierarchy & Anti-Burying Rule
- **One Primary Action Per View/Section:** At most one high-contrast primary button per screen, modal, or card. Secondary actions use outline or ghost variants.
- **Never Bury Primary CTAs:** Primary actions must NEVER be hidden inside `...` overflow menus, collapsed accordions, hover-only overlays, or deeply nested sub-cards. Pin submit actions in a visible sticky footer bar in long forms/drawers.
- **Zero Duplicate Actions or Blocks:** Never render duplicate primary buttons, duplicate search inputs, or duplicate summary blocks on the same viewport (except explicit responsive breakpoint mirrors `md:hidden` / `hidden md:block`).

### 3.5 CRUD & Save Semantic Color Coding (Default Rule)
Unless `./DESIGN.md` or an explicit user instruction specifies otherwise, all CRUD and persistence actions, row accents, icon buttons, and confirmation modals MUST follow:

- **Create & Save (`C` - Add / New / Create / Save / Confirm):** **Green / shade of green**
- **Update (`U` - Edit / Modify / Update):** **Orange / shade of orange**
- **Delete (`D` - Remove / Archive / Delete):** **Red / shade of red**

### 3.6 Semantic Domain Cards (Context-Aware Design)
Never render distinct domain entities with the same generic card layout:

- **Promotional / Offer / Deal Entities:** Distinct deal framing/border, prominent value/discount callout in `tabular-nums`, concise validity/terms tag, and explicit redemption CTA pinned at the bottom.
- **Media / Location / Profile Entities:** Fixed-ratio imagery, category/status tag, clean metadata hierarchy, and direct navigation/action affordance.
- **Scheduled / Pass / Booking Entities:** Date/time hierarchy, tier/pricing clarity, availability indicator, and direct booking/action button.
- **Project-Specific Entity Rules (Define in Fork):** `TBD`

### 3.7 Reordering, Drag-and-Drop & Kanban Boards
- **Explicit Drag Handle:** Attach drag listeners to a visible `GripVertical` icon (`cursor-grab active:cursor-grabbing`, `aria-label="Reorder item"`), never the entire card.
- **Clear Visual Feedback:** Elevated shadow + `ring-2 ring-[var(--accent-primary)]` + `opacity-90` on dragged items; `border-dashed border-[var(--border-strong)]` placeholder at drop target.
- **Kanban Columns:** Horizontal scroll container (`overflow-x-auto flex gap-4 pb-4`), uniform column widths (`w-72` to `w-80 shrink-0`), sticky column headers (title + count), supporting intra-column reorder and cross-column moves.
- **Optimistic Persistence & Accessibility:** Update state optimistically on drop with rollback on API error; include keyboard reordering and mobile move controls.

### 3.8 Loading States, Spinners & Skeletons
- **Button / Mutation Spinners:** Prefix/replace action icon with a spinning icon (`animate-spin`, `w-4 h-4`), set `disabled` + `aria-busy="true"`, keep button width stable (`whitespace-nowrap`), and preserve CRUD/Save hues (`Green` / `Orange` / `Red`).
- **Lists, Cards & Tables:** Use layout-matched skeleton placeholders (`animate-pulse`) matching card/row dimensions; use small inline spinners (`w-5 h-5`) only for compact live refreshes.
- **Route Transitions:** Top progress bar or section skeleton; never blocking full-screen modal spinners unless auth gating requires it.
- **Reduced Motion & A11y:** Respect `motion-reduce:animate-none` and provide `sr-only` / `aria-live="polite"` status labels.

### 3.9 Responsiveness, Interactive States, Overlays & Feedback
- **Breakpoint Scaling (`390px` Mobile -> `768px` Tablet -> `1280px+` Desktop):**
  - Build mobile-first (`390px`) with single-column flow by default, scaling cleanly to multi-column grids (`grid-cols-1 md:grid-cols-2 lg:grid-cols-3` or `lg:grid-cols-4`) and split/sidebar operational layouts on desktop without clipping or squishing text.
  - Enforce touch targets `>= 40x40px` (`min-h-10 min-w-10`) on mobile interactive controls, keep horizontal overflow at zero (`overflow-x-hidden` on root/page wrappers; `overflow-x-auto` only on intentional Kanban lanes or wide data tables), and keep body text `>= 14px`.
  - Swap full modals for bottom/side drawers (`Sheet`) on narrow viewports when appropriate, and keep primary action bars thumb-reachable or sticky without overlapping content.
- **Interactive States & Focus:** Explicit `:hover`, `:focus-visible` (`ring-2 ring-offset-2`), and `:disabled` states; modals/drawers manage focus and close on `Escape` / backdrop click.
- **Toasts vs. Inline Errors:** Transient toasts (`sonner` / `toast`) for async completion; inline errors directly below invalid form fields.
- **Empty & Error States:** Concise library icon + 1-line label + primary recovery CTA; no multi-sentence descriptions.

### 3.10 Data Tables, Border Radius, Layering & Anti-Drift Guardrails
- **Data Tables & Lists:** Left-align text, right-align numbers/prices/counts (`tabular-nums`), pin row actions right, wrap in `overflow-x-auto` with `sticky top-0` headers, and distinguish empty state (Create CTA) vs. filtered-empty state (`"Reset filters"`).
- **Destructive & Unsaved-Changes Safety:** Delete (`D`) opens a confirmation modal naming the item with a **Red** confirm CTA (`"Delete <Item>"`). Dirty forms warn before discarding changes.
- **Border Radius & Z-Index Scale:** Concentric radii (cards/modals > inputs/buttons > small controls) and strict stacking (`base` < `sticky` < `popover/dropdown` < `modal/drawer` < `toast`).
- **Hard Bans (What Never to Create):**
  - **No Inline `<svg>` Icons & No Custom Reinvention:** Never write raw `<svg>` icon paths or custom-build components (pickers, dialogs, dropdowns, carousels, tabs, drag-and-drop, toasts) when a reference library component exists, and always confirm with the user before installing or pulling from reference registries.
  - **No Sparkle Icons or Mismatched Icons:** Never use sparkle icons unless explicitly requested, and never place icons that do not match the exact context of the word, label, or action.
  - **No Unnecessary Words or Explanations:** Zero filler sentences, verbose helper text, or redundant descriptions in user-facing UI or developer-facing summaries/comments.
  - **Normal Dash Only (`-`):** Always use standard hyphens (`-`) instead of em dashes or en dashes across UI copy, code comments, and developer responses.
  - **No Decorative Badges or Pulsing "Live" Dots:** Never add decorative pills/badges (`"NEW"`, `"FEATURED"`, `"LIVE"`, `"POPULAR"`) or pulsing/pinging status dots (`animate-ping`) unless backed by real-time state explicitly specified in `./DESIGN.md`.
  - **No One-Off Primitives or Arbitrary Values:** Never invent page-specific card/input/badge variants, raw hexes, or arbitrary pixel brackets (`p-[13px]`, `text-[15px]`).
  - **No Color-Only Status:** Pair error/status colors with a library icon or concise label.

---

## 4. Agent Execution Checklist (Run Before Marking Any UI Task Done)

1. [ ] Asked clarifying questions on any doubts and received explicit approval before creating `./DESIGN.md` or modifying UI?
2. [ ] Forked into `./DESIGN.md` with every `TBD` replaced from this repo?
3. [ ] Confirmed with the user before installing dependencies or pulling components from reference libraries, and used zero raw `<svg>` icons?
4. [ ] Zero sparkle icons (unless explicitly requested) and every icon matches its exact label/context?
5. [ ] Zero unnecessary user-facing filler copy or verbose developer-facing explanations?
6. [ ] All placeholders high-contrast (`>= 4.5:1`), paired with `<label>`, and marked with `*` on required fields?
7. [ ] All date/time fields built with library calendar/popover pickers (no native `type="date"`)?
8. [ ] Selection controls strictly separated (`Checkbox` for multi-select/consent, `RadioGroup` for 2-5 mutually exclusive choices, `Switch` for instant boolean toggles, `Select`/`Combobox` for 5+ options)?
9. [ ] Typography hierarchy (`Hero`, `Title`, `Subtitle`, `Body`, `Caption/Meta`, `Label/Action`) matches semantic weight and role?
10. [ ] Each domain entity uses its own context-appropriate card anatomy rather than a generic card?
11. [ ] Primary actions surfaced at top level with zero duplicate buttons/blocks?
12. [ ] Create/Save (`C`) = Green, Update (`U`) = Orange, Delete (`D`) = Red unless overridden?
13. [ ] Reorderable lists/Kanban use `GripVertical` handles, drop placeholders, optimistic updates, and keyboard/mobile controls?
14. [ ] Loading states use layout-matched skeletons or stable inline button spinners with `disabled`/`aria-busy`?
15. [ ] 4-directional padding, section gutters (`px-*`), and top/bottom margins uniform with zero trailing bottom-margin bloat?
16. [ ] Verified responsive layout, column reflow, touch targets (`>= 40x40px`), and zero horizontal overflow across mobile (`390px`), tablet (`768px`), and desktop (`1280px+`)?
17. [ ] Decorative badges and pulsing live-indicator dots completely absent?
18. [ ] Standard hyphens (`-`) used everywhere instead of em dashes or en dashes?
19. [ ] Build and typecheck pass with zero errors?