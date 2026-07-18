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

## Common mistakes (the generic-AI-page tells)

- Purple/blue gradient hero → delete; whitespace + big type is the hero
- 6+ font sizes, weights 300/500/700/900 → collapse to the scale
- Cards with borders AND shadows AND radius → pick radius + bg tint only
- Emoji as icons in headings → remove
- Centered long paragraphs → center only ≤2-line text; prose is left-aligned
- Cramped 60–80px sections → 160px; scrolling is free, clutter is not
