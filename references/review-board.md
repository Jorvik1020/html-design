# Review-board register

A shareable internal board that people **review and operate**: a funnel summary, a prioritised briefing, categorised record tables with per-reviewer marks, and a pipeline table with per-row settings. It is a product surface (see "Brand surface vs product surface"), so everything in that section holds. It needs script for tabs, filters and saving marks: that is behaviour, not motion, and the static rule still applies to everything visual. These settings survived six rounds of owner review on a production board; start the next board from them.

Stylesheet: `references/review-board.css`. Copy it whole.

## Page order

1. **Header**: H1 28px/600 (−0.022em) + one 13px subtitle line. Right side: a freshness chip ("Live data · updated 19 Sep 08:01", green tint; say when the data was generated, never claim live if it is a snapshot) and the reviewer name input.
2. **Summary**: two cards side by side (`1.05fr 1fr`, stacks under 900px). Left = funnel + conversion strip. Right = briefing.
3. **Records** (leads): main tabs → sub-category pills → table.
4. **Pipeline**: one row per engaged account, with the per-row setting control.
5. **Footer**: the number-colour legend (fact · good signal · watch · act now) and one sentence on what the page cannot do ("read and review only: nothing on this page sends a message").

Section heads are 13px/600 uppercase, +0.06em, `--ink-2`, with a lower-case 13px `<small>` that says what the section is for.

## Tokens

Blue-slate, one card background, dusty state hues. Light: `--bg #eef2f8`, `--card #fff`, `--line #dfe5ee`, ink `#101c2c / #47556e / #5d6b80`, accent `#0066cc`. States: fact `#22687f`, good `#20714b`, watch `#7a5717`, act `#a63d4e`, info `#44598a`, each with a `-tint` background. Dark is **blue-grey, never neutral black**: `--bg #0d1420`, `--card #151f2c`, `--line #26344a`, ink `#eef2f7 / #b6c1d1 / #8795aa`, accent `#6ea3f0`, state hues lifted to pastels (`#7dbbdb #70c79b #e0b566 #ee909c #a3b6e0`) on deep tints. Radius 13px cards, 8px controls, 999px chips and pills.

Every colour is a variable, defined in the bare `:root`, then redefined under `@media (prefers-color-scheme: dark)` as `:root:not([data-theme="light"])` and again under `:root[data-theme="dark"]`. No colour literal outside those three blocks (the only exception is white text on the saturated funnel bands). `body` paints its own background: one soft accent radial glow + the 36px engineering grid on `body::before`, masked to fade by 68%.

Give a board its **own audited stylesheet**. Do not inherit a sibling page's CSS: a borrowed stylesheet drags in dead rules and one-theme literals.

## Left rail (section nav)

- Fixed, full height, its **own colour** so it reads as a separate surface: `--rail #1f3a5f` (light), `#1b2a40` (dark), text `--rail-ink`, active/hover `--rail-on` on `--rail-on-bg`.
- **Auto-hide**: 52px collapsed (a 24px initial tile per section), opens to 168px on hover or keyboard focus and **overlays** the content with a soft shadow, so nothing reflows. The static edition switches width and labels instantly.
- **Pin** at the bottom ("Keep open" / "Collapse") shifts the content instead of overlaying; remembered per viewer in localStorage inside try/catch.
- Content offset: `margin-left:max(52px, calc(50% - 620px))`, pinned `max(168px, …)`, so a wide screen keeps the page centred.
- Mark the section currently in view (`.on`), first link on by default.
- Under 1000px the rail becomes a sticky top bar of text links (initial tiles and pin hidden). Phones never get a side rail.
- `aria-label="Sections"`, visible `:focus-visible` ring in `--rail-on`, hidden in print.

## Funnel

Inverted trapezoid, one hue, opacity ladder `0.16 → 1` (`0.16 + 0.84·(i/(n−1))^1.15`), 50px bands with 3px gaps, label inside each band ("Invited · 20", 16px/600; ink on pale bands, white once opacity > 0.5), a 14px grey annotation to the right of each band (hidden under 700px). The **last band is the north star**: filled with `--act`, full opacity, 2px stroke. Bands are buttons (`tabindex=0 role=button`, Enter/Space, `aria-label` with the count): clicking one filters the pipeline table to that stage and beyond; unselected bands drop to 35%. Hover/focus = brightness 1.08 + drop shadow + 1.5px ink stroke. Caption under the figure says what clicking does.

**Conversion strip** under the funnel: four cells, value 22px/600 tabular in `--fact`, label 12px, "n of m" 12px. A cell whose north-star rate is zero becomes `.cv.alert`: `--act-wash` fill, 1px inset `--act` ring at 28%, red value. One alert at most.

## Briefing

Three blocks, P0 · act now / P1 · this week / P2 · keep warm, each a 3px left rule in the state hue (act / watch / fact), 12px uppercase head, 13px lines. Each line = **bold subject** + what happened + `→` the next action. Computed from the data, never hand-written; an empty block is omitted.

## Chips: one meaning per hue

| Chip | Hue |
|---|---|
| P0, Act now | act (red) |
| P1 | watch (amber) |
| P2 | fact (blue-teal) |
| P3, Waiting, Held (Held also struck through) | neutral |
| New | info (slate-blue) |
| Approved, Replied, freshness | good (green) |

12px/600, +0.03em, 3×9px, pill. Status words are sentence case ("Approved", "Held", "New"). The next-step column uses two states only: **Act now** and **Waiting**, followed by the plain-words step.

## Tabs and sub-category pills

- Main tabs: ≤4, underline style (2px accent under the selected one), count after the label, arrow-key navigation, `role=tablist/tab/tabpanel`.
- Sub-categories are **pills**, not a second tab row: `role="group"`, first pill "All n" selected (ink fill, card-colour text), the rest sorted by count with "Other" last. Filtering renumbers the visible rows.
- **Category names come from published standards, never invented**: Salesforce Account Type for the main tabs, Salesforce Industry (+ sub-industry) for customers, analyst/G2 market categories for vendors. A collapsed "How accounts are categorised" block under the table names each source.

## Tables

13px body, 12px uppercase headers (+0.05em), rows ruled with `--line-soft`, no zebra, numbers right-aligned tabular. Each table sits in its own `overflow-x:auto` wrapper with a `min-width` (900 / 980px) so it scrolls instead of crushing. Account cell = name as a link to the official site (↗) + 12px grey meta on the same baseline. The "why" text is clamped to one line until the row opens; an open row gets a faint fact-tint wash.

## Review cell (per-reviewer marks)

Collapsed by default: a one-line summary ("Owner ok · 2 others" / "No review yet") + a **Review** pill button. Opening the row shows every reviewer's line (`name` bold, verdict coloured ok/no, comment), then the controls: `ok` / `no` pills + a one-row auto-growing textarea. It opens on its own when the current reviewer already has a mark. With no reviewer name entered the controls are real `button[disabled]` and an amber 12px line says why. Marks persist per reviewer (one doc per person), mirrored to localStorage in try/catch; the owner's earlier decisions are seeded from the data so the page never opens empty.

## Multi-select setting in a table row

`<details class="ms">` with checkbox labels in an absolutely positioned menu: summary shows the picks comma-separated, **first pick leads** and that rule is printed above the table. The last five rows open **upward** (`.ms.up`) so the menu never gets clipped by the table wrapper. A "Copy settings" button next to the rule line hands the state back to the machine when the page cannot write to it.

## Text floors and numerals

Nothing under 12px. Task text 13px, table meta and chips 12px. All counts `font-variant-numeric: tabular-nums`. Number colour obeys the page-wide legend (blue fact, green good, amber watch, red act today).

## States and a11y checklist

`[hidden]{display:none!important}` (a chip's `display` otherwise beats the attribute). Visible `:focus-visible` on every control. Tabs by arrow keys, funnel bands by Enter/Space, review toggle is a real button with `aria-expanded`. Empty tables say "Nothing here yet." Print hides the rail and the background grid. Render the page and look at desktop-light, desktop-dark and phone before shipping.

## The matching workbook

When a board has a spreadsheet twin (openpyxl): header fill `#1F3A5F` white bold, **hand-edited columns get a different header** (`#5D6B80`) and are read back by key before every rebuild so they survive; zebra `#F5F8FC`, bottom hairlines `#DFE5EE`, gridlines off, freeze `B2`, autofilter on. Chips become **conditional formats** (so a hand edit recolours too) with the same tint/ink pairs: P0 `F6E1E5/A63D4E`, P1 `F5ECD9/8A6425`, P2 `DDEBF7/22687F`, neutral `EEF2F8/5D6B80`, good `DFF0E7/20714B`. Dropdowns point at a `Lists` sheet. A Summary sheet repeats the funnel with a `█` bar column, the north-star row in red.
