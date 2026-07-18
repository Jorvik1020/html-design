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

## Common mistakes (the generic-AI-page tells)

- Purple/blue gradient hero → delete; whitespace + big type is the hero
- 6+ font sizes, weights 300/500/700/900 → collapse to the scale
- Cards with borders AND shadows AND radius → pick radius + bg tint only
- Emoji as icons in headings → remove
- Centered long paragraphs → center only ≤2-line text; prose is left-aligned
- Cramped 60–80px sections → 160px; scrolling is free, clutter is not
