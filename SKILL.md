---
name: html-design
description: Use when building ANY HTML page, deck, artifact, landing page, report, or presentation. Load BEFORE writing the first line of markup or CSS.
---

# HTML Design — house template

## Overview

Design system distilled from **live computed-style teardowns** of apple.com/airpods-pro and linear.app — real extracted numbers, not folklore. Two themes: **Apple-light** (default, for decks/briefs/reports) and **Linear-dark** (`data-theme="dark"`, for technical/product pages).

**Core principle: the design IS the type scale and the whitespace. Color, decoration, and motion are condiments.**

## Start here

Copy `template.html` (same folder) and replace content. It contains all tokens, both themes, every component, and the scroll-reveal system. Do NOT write page CSS from scratch.

## The extracted DNA (quick reference)

| Token | Apple-light | Linear-dark |
|---|---|---|
| Background | `#ffffff`, alt `#f5f5f7` | `#08090a` (never pure black), card `#141516` |
| Ink / secondary | `#1d1d1f` / `#6e6e73` | `#f7f8f8` / `#8a8f98` |
| Accent (ONE only) | `#0066cc` link, `#0071e3` button | one hue max, desaturated |
| Font | system stack (SF Pro) | Inter Variable, weight 510 |
| Display scale | 96 / 56 / 28 / 21px, all weight 600 | 64 / 48 / 24px, weight 510 |
| Letter-spacing | **−1.5% at 96px → +0.7% at 28px** | ≈ −2.2% of font-size |
| Body | 17px, lh 1.47, ls −0.022em | 17–18px |
| Section rhythm | **160px** top/bottom, alternate bg | same |
| Content width | 1024px standard, 1260px wide, ~700px prose | same |
| Radius | 18px cards, 980px (pill) buttons | 9999px pills |
| Stats | value 80px/600, caption 19px/600 | same pattern |

## The ten rules (what the masters actually do)

1. **One idea per viewport.** Each section makes exactly one claim; the headline IS the claim ("The best thing you've never heard."), never a label ("Features").
2. **Five font sizes max** on a page. Two weights (600/400). If it needs a sixth size, the hierarchy is broken, not the scale.
3. **Tracking follows size**: tighten display type (−1% to −1.5%), loosen small type (+0.5%). This is 80% of "why does it look like Apple."
4. **Color discipline**: ink + one gray + ONE accent. No gradients, no second accent, no colored headings.
5. **Whitespace is the luxury**: 160px between sections, ~700px prose column. When in doubt, delete an element rather than shrink the spacing.
6. **Numbers are heroes**: any stat gets the 80px treatment with a 19px caption ("2x more" / "Active Noise Cancellation").
7. **One primary button per screen**, pill-shaped. Secondary actions are plain accent-colored text links ("Learn more >").
8. **Alternate section backgrounds** (white/#f5f5f7) instead of divider lines. Never use `<hr>`.
9. **Motion = reveal only**: opacity + 20px rise, 0.7s ease-out, staggered ≤100ms, on scroll-into-view. Nothing loops, bounces, or parallaxes. Respect `prefers-reduced-motion`.
10. **The squint test before shipping**: blur your eyes — you should still see the hierarchy (one big thing per screen). Then ask the hostile-critic question: *what is the single ugliest thing here?* Fix it before delivery.

## Brand surface vs product surface — decide FIRST

The template's big-type/whitespace DNA is for **brand surfaces** (decks, landing pages, narratives). A **product surface** (dashboard, tool, report the user works FROM) follows the opposite register — in our test, applying brand rules to a working dashboard cost 1.82× the vertical space and scored worse on all task-fit heuristics:

- Fixed rem scale, ratio ~1.2 (11/13/16/19/28px), no `clamp()`, no display heroes; section headers/subtitles ≥13px in a deep neutral, not weak light-gray small caps
- Density is a feature: whole artifact ≤2.5 viewports; task content (actions) before context (charts)
- **Unified palette**: all cards share ONE background (white) on a subtly layered page wash (soft accent glow + very faint grid, masked to fade); semantic state hue appears only at edges — a 6px left border + tinted chip + bullet dots — in DESATURATED dusty tones. Full tinted card backgrounds read cheap and inconsistent.
- **Depth, not flatness**: data graphics may use same-hue vertical gradients + `filter:drop-shadow` + small segment separation (stacked-plate depth — never multi-hue or PowerPoint-3D); cards get layered elevation (inset top highlight + tight shadow + long soft shadow)
- **Number-color semantics, page-wide**: blue = fact · green = good signal · amber = watch · red = act today. One logic for every numeral; print the legend in the footer; never color numbers decoratively.
- **Motion**: fast staggered entrances (.42s, 70ms stagger; in-view content shows instantly), charts draw in level-by-level, big numerals count up slowly (~2.2s ease-out) when their group scrolls into view, and charts may be interactive where it aids the task (click a funnel stage → related metrics spotlight + re-count). Always progressive (no-JS = fully visible), `prefers-reduced-motion` + `beforeprint` safe.
- Domain conventions beat aesthetic preference: if a domain has a canonical chart form (e.g. sales pipeline = inverted trapezoid funnel), keep the form and restyle it within the system.
- WCAG AA is part of the system: all text ≥4.5:1 on its actual background; lint deterministically with `npx -y impeccable detect <file>`.

## Real-paper background (brand surfaces)

Flat white/gray backgrounds read monotonous. The fix is a **paper material layer**, not stronger decoration — and true paper feel comes from **lighting** (SVG relief), not flat noise. Key lesson: `feTurbulence type='turbulence'` reads as marble; use `fractalNoise` for pulp.

The stack (bottom→top): ① vertical wash gradient ② one or two soft accent radial glows ③ **relief-lit paper** (noise as a bump map into `feDiffuseLighting`, tiled, multiplied) ④ soft pulp clouds ⑤ sparse flecks ⑥ optional faint grid on `::before`, masked to fade down (paper stays uniform; grid fades).

```css
background:
  url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='480' height='480'><filter id='p' x='0' y='0' width='100%25' height='100%25'><feTurbulence type='fractalNoise' baseFrequency='0.04' numOctaves='5' stitchTiles='stitch' result='n'/><feDiffuseLighting in='n' lighting-color='%23ffffff' surfaceScale='1.5' diffuseConstant='1.05'><feDistantLight azimuth='235' elevation='58'/></feDiffuseLighting></filter><rect width='100%25' height='100%25' filter='url(%23p)' opacity='0.45'/></svg>") repeat,
  url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='900' height='900'><filter id='m'><feTurbulence type='fractalNoise' baseFrequency='0.007' numOctaves='3' stitchTiles='stitch'/><feColorMatrix type='saturate' values='0'/></filter><rect width='100%25' height='100%25' filter='url(%23m)' opacity='0.07'/></svg>") repeat,
  url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='320' height='320'><filter id='s'><feTurbulence type='fractalNoise' baseFrequency='0.45' numOctaves='2' stitchTiles='stitch'/><feColorMatrix type='saturate' values='0'/><feComponentTransfer><feFuncA type='discrete' tableValues='0 0 0 0 0 0 0 0 0 0.55'/></feComponentTransfer></filter><rect width='100%25' height='100%25' filter='url(%23s)' opacity='0.05'/></svg>") repeat,
  radial-gradient(1100px 560px at 10% -8%, rgba(0,102,204,.10), transparent 62%),
  radial-gradient(820px 460px at 96% 4%, rgba(64,100,160,.07), transparent 62%),
  linear-gradient(180deg,#ffffff 0%,#f5f7fa 100%);
background-size:480px 480px,900px 900px,320px 320px,auto,auto,auto;
background-blend-mode:multiply,multiply,multiply,normal,normal,normal;
```

Knobs: `baseFrequency 0.04` (higher = finer tooth) · `surfaceScale 1.5` (bump depth) · relief `opacity 0.45` (strength). Keep the color system cool — never let the paper drift warm/beige even when a warm reference photo is supplied. Cards sitting on paper are **white everywhere** (drop the white/gray card alternation); layered elevation carries the contrast.

## Slide-deck register (structure)

The presentation form of the system:
- **Paged slides**: `.slide{position:absolute;inset:0}` + an `.active` class toggling opacity/visibility; a 2px top progress bar (animate `transform:scaleX`, never `width`); arrow keys / space / PgUp / PgDn / Home / End + touch swipe; deep links via `#n`; print = `position:relative` + `page-break-after` with a landscape `@page`; small screens fall back to vertical scroll.
- **Per-slide reveal**: scope the template's reveal system to `.slide.active` so each slide replays its entrance when entered.
- **Equal-geometry locks**: `.cards{align-items:stretch;grid-auto-rows:1fr}` with columns `repeat(3,minmax(0,1fr))` — `minmax(0,1fr)` is mandatory: a `white-space:nowrap` line otherwise silently widens its column. Equal card sizes are a hard rule.
- **Bilingual lockup** (optional): primary-language headline + secondary-language subtitle as a `display:block` span at `.56em`, muted ink, 12px top margin; cards open with a short keyword lead line. Keyword-capitalize titles and sublabels.
- **Don't double-list**: if a visual (badges, chips, diagram) enumerates items, the adjacent text must not repeat the list — one lead line and a pointer instead.
- **Live-artifact embed**: a slide may iframe a live page (fixed height, radius, elevation, scrollable). Single-source rule: numbers shown elsewhere in the deck must match the embedded artifact — refresh the artifact, never fork the numbers.

## Annotation system + honest-claims harness

**Asterisk annotations**: any stat, claim, or headline word needing qualification gets a trailing `*` (muted, not accent). ALL asterisk notes collect into ONE block: bottom-left, caption size, `line-height:2`, each note on its own line prefixed `*`, ordered by where their markers appear. The block's left edge aligns with the CONTENT BODY's visible left edge (e.g. the first big stat numeral), not the page margin — and stays clearly separated from both content and footer. Annotations stay out of the body (the body stays the hero) but remain findable in one place.

**Honest-claims harness** (what makes numbers defensible in front of a tough audience):
- **Measure, don't estimate.** If a number can be computed from logs/records, compute it and be ready to show the method.
- **Pair hero metrics with a reference class.** A conversion or performance number is meaningless alone; add a benchmark annotation line (`*Benchmark: industry range X–Y% …`) so the reader can place it.
- **Keep the zero visible.** An honest "0 so far" out-converts hype with any experienced audience.
- **Claim language must match the system.** If humans gate the sends, say "autonomous-first, human-gated" — an absolute like "100% auto" contradicts the harness and invites the attack.

## Common mistakes (the generic-AI-page tells)

- Purple/blue gradient hero → delete; whitespace + big type is the hero
- 6+ font sizes, weights 300/500/700/900 → collapse to the scale
- Cards with borders AND shadows AND radius → pick radius + bg tint only
- Emoji as icons in headings → remove
- Centered long paragraphs → center only ≤2-line text; prose is left-aligned
- Cramped 60–80px sections → 160px; scrolling is free, clutter is not
