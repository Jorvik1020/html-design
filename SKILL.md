---
name: html-design
description: Use when building ANY HTML page, deck, artifact, landing page, report, or presentation. Load BEFORE writing the first line of markup or CSS.
---

# HTML Design — house template

## Overview

Design system distilled from **live computed-style teardowns** of apple.com/airpods-pro and linear.app — real extracted numbers, not folklore. Two themes: **Apple-light** (default, for decks/briefs/reports) and **Linear-dark** (`data-theme="dark"`, for technical/product pages).

**Core principle: the design IS the type scale and the whitespace. Color and decoration are condiments.**

**This edition ships fully static** — no scripts, no entrance animation, no loops. Every rule below assumes the page must carry itself with type, spacing, and color alone.

## Start here

Copy `template.html` (same folder) and replace content. It contains all tokens, both themes, and every component — static, script-free, print/headless safe. Do NOT write page CSS from scratch.

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
9. **Ship static.** No entrance choreography, no loops, no parallax, no scroll effects. A page that needs motion to look alive has a hierarchy problem, not a motion deficit — fix the type and spacing instead.
10. **The squint test before shipping**: blur your eyes — you should still see the hierarchy (one big thing per screen). Then ask the hostile-critic question: *what is the single ugliest thing here?* Fix it before delivery.

## Brand surface vs product surface — decide FIRST

The template's big-type/whitespace DNA is for **brand surfaces** (decks, landing pages, narratives). A **product surface** (dashboard, tool, report the user works FROM) follows the opposite register — in our test, applying brand rules to a working dashboard cost 1.82× the vertical space and scored worse on all task-fit heuristics:

- Fixed rem scale, ratio ~1.2 (11/13/16/19/28px), no `clamp()`, no display heroes; section headers/subtitles ≥13px in a deep neutral, not weak light-gray small caps
- Density is a feature: whole artifact ≤2.5 viewports; task content (actions) before context (charts)
- **No load choreography**: a product surface loads into a task — everything visible instantly; interactivity is navigation and filtering, never decoration
- **Unified palette**: all cards share ONE background (white) on a subtly layered page wash (soft accent glow + very faint grid, masked to fade); semantic state hue appears only at edges — a 6px left border + tinted chip + bullet dots — in DESATURATED dusty tones. Full tinted card backgrounds read cheap and inconsistent.
- **Depth, not flatness**: data graphics may use same-hue vertical gradients + `filter:drop-shadow` + small segment separation (stacked-plate depth — never multi-hue or PowerPoint-3D); cards get layered elevation (inset top highlight + tight shadow + long soft shadow)
- **Number-color semantics, page-wide**: blue = fact · green = good signal · amber = watch · red = act today. One logic for every numeral; print the legend in the footer; never color numbers decoratively.
- Domain conventions beat aesthetic preference: if a domain has a canonical chart form (e.g. sales pipeline = inverted trapezoid funnel), keep the form and restyle it within the system.
- WCAG AA is part of the system: all text ≥4.5:1 on its actual background; lint deterministically with `npx -y impeccable detect <file>`.

## Review-board register

For a shareable board people review and operate (funnel summary + prioritised briefing + categorised record tables with per-reviewer marks + a pipeline table). Full spec: `references/review-board.md`; stylesheet to copy whole: `references/review-board.css`. The settings that matter most:

- **Left rail in its own colour** (`--rail #1f3a5f` light / `#1b2a40` dark), **auto-hiding**: 52px strip of initial tiles, opens to 168px on hover/focus as an overlay (no reflow), a pin keeps it open and shifts the content, scroll highlight, sticky top bar under 1000px.
- **Funnel = inverted trapezoid**, one hue on an opacity ladder, the last band (north star) in `--act` red; bands are keyboard-reachable buttons that filter the table below. A conversion strip sits under it; a zero north-star rate gets the single red alert cell.
- **Briefing** in three blocks (P0 act now / P1 this week / P2 keep warm), each line "**subject** what happened → next action", computed from data.
- **Chips, one meaning per hue**: P0/Act now red, P1 amber, P2 blue-teal, P3/Waiting/Held neutral (Held struck through), New slate-blue, Approved green.
- **≤4 main tabs + sub-category pills** (never a second tab row); category names from published standards (Salesforce Account Type / Industry, analyst and G2 categories), never invented, sources listed in a collapsed block.
- **Review cells collapse** to a one-line summary + Review button; per-reviewer marks; disabled controls are real `button[disabled]` with the reason shown.
- **Dark theme is blue-grey** (`#0d1420` / `#151f2c`), every colour a variable defined in all three theme blocks, the board carries its own audited stylesheet.
- Nothing under 12px; tables scroll in their own wrapper; in-table multi-select menus open upward on the last rows.
- A spreadsheet twin uses the same palette: `#1F3A5F` headers, a second header colour for hand-edited columns that survive rebuilds, chips as conditional formats.

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

The presentation form of the system — all state changes are instant (show/hide), never animated:
- **Paged slides**: `.slide{position:absolute;inset:0}` + an `.active` class toggling visibility instantly; a 2px top progress bar sized per slide; arrow keys / space / PgUp / PgDn / Home / End + touch swipe; deep links via `#n`; print = `position:relative` + `page-break-after` with a landscape `@page`; small screens fall back to vertical scroll.
- **Equal-geometry locks**: `.cards{align-items:stretch;grid-auto-rows:1fr}` with columns `repeat(3,minmax(0,1fr))` — `minmax(0,1fr)` is mandatory: a `white-space:nowrap` line otherwise silently widens its column. Equal card sizes are a hard rule.
- **Bilingual lockup** (optional): primary-language headline + secondary-language subtitle as a `display:block` span at `.56em`, muted ink, 12px top margin; cards open with a short keyword lead line. Keyword-capitalize titles and sublabels. When a caption pairs two languages, break the second language onto its own line rather than joining with a separator — mixed-script lines wrap mid-phrase at narrow widths.
- **Flow diagrams (SVG), static**: white pill nodes (rx = half height) with per-node `feDropShadow`, cool desaturated strokes, ONE accent hue; connectors dotted (`stroke-dasharray:1 7`, round caps); a domain funnel may embed inside the core node (opacity ladder + stage labels); the caption is one line of caption-size text below the white container, never inside the SVG.
- **Brand/logo badges**: white chips (radius 12, card elevation), 24px rounded official logo + brand-color wordmark. Source logos from GitHub org avatars (`github.com/<org>.png`) first but VERIFY visually — fake/fan orgs exist; fall back to the official site's favicon/webclip, and confirm identity via the page `<title>`. Never substitute a parent company's mark. The badge cluster sits close to the text it illustrates, not flush to a far edge.
- **Don't double-list**: if a visual (badges, chips, diagram) enumerates items, the adjacent text must not repeat the list — one lead line and a pointer instead.
- **Live-artifact embed**: a slide may iframe a live page (fixed height, radius, elevation, scrollable). Single-source rule: numbers shown elsewhere in the deck must match the embedded artifact — refresh the artifact, never fork the numbers.

## Fixed-stage deck register (1920×1080)

There are two deck architectures. Choose deliberately.

| | **Viewport register** (the slide register above) | **Fixed-stage register** |
|---|---|---|
| Sizing | `vh`/`vw` + `clamp()`, reflows per screen | one 1920×1080 canvas, scaled as a whole |
| Wins | adapts to odd windows, long text breathes | pixel-exact fidelity: what you author is what projects |
| Costs | line counts shift between laptop and projector | overflow is yours to solve, no reflow rescue |
| Use for | reading decks, briefs, artifacts opened in a browser | anything projected or exported to PDF |

Prefer fixed-stage when the deck will be **presented or exported**; keep the viewport register for read-in-a-tab artifacts.

**The invariants (all mandatory in this register):**
- A viewport wrapper fills the window; the stage is `width:1920px;height:1080px;transform-origin:0 0`, scaled by `Math.min(innerWidth/1920, innerHeight/1080)` and centred with a translate. Letterbox/pillarbox is correct; re-layout is not.
- Author every internal measurement at the 1920×1080 design size. **No responsive breakpoints rearranging slide content**, including on phones.
- ⚠️ **Toggle slides with `visibility` + `opacity` + `pointer-events`, NEVER `display:none`/`block`.** A later layout rule such as `.slide-content{display:flex}` overrides the toggle and every slide renders at once. Silent and total.
- ⚠️ **Never negate a CSS function** — `-clamp()`, `-min()`, `-max()` are silently ignored. Write `calc(-1 * clamp(...))`.
- `clamp()` belongs only to chrome *outside* the stage, never to slide content.
- Print block: slides become `position:relative` with `break-after:page`.

Static-edition note: the single permitted script is the resize handler that sets the scale factor. That is layout, not motion — state changes stay instant and nothing animates.

## Corporate brand register (working inside someone else's design system)

When the artifact ships under a client's or employer's brand, their system outranks this one. Do not approximate it from memory.

**Extract it live.** Open the brand's own site and read computed styles for: body and heading font stacks, heading weight and letter-spacing, true ink color, accent fill vs accent link (often two different values), card radius, card shadow, and section background colors. Ten minutes of measurement beats an afternoon of guessing, and it produces numbers you can defend.

**What usually separates a corporate system from this house style:**
- Heading weight is often **700 with normal letter-spacing**, not 600 with negative tracking. Negative tracking on a bold corporate headline is the single loudest tell that you styled it from habit.
- Ink is frequently **true black**, not a warm near-black.
- Radius is small (**8px or flat 0**), not 18px, and shadows are tighter and cooler.
- The palette is usually **white canvas with a pale tint for information surfaces**, plus one deep panel for a single emphasis band per page.

**Rules that keep it authentic:**
- **White canvas everywhere, covers and closings included.** A full-accent cover is the tell of a generic template.
- Category labels small, uppercase, tracked, in the brand accent. Titles large, bold, left-aligned.
- **Flat rectangles and pale information surfaces** beat rounded UI cards. Pale hierarchy, never saturated-dark blocks.
- Vary composition by narrative role. Repeating one card grid down the whole deck is the failure mode.
- Icons small and functional; screenshots are **evidence, not decoration**.
- Avoid: persistent header/footer furniture, dashboard density on a narrative page, decorative gradients and abstract blobs, tiny text used to force content into the wrong layout.

**Font doctrine conflict, resolved:** general "never use system fonts, never Inter or Arial" advice does not apply inside a brand system where those faces *are* the authentic voice. Reach for distinctive display faces only on surfaces that belong to neither a corporate system nor this house style.

## Deck density and change-safety contract

**Pick a density mode before authoring, and state which you picked:**

| Mode | For | Behaviour |
|---|---|---|
| **Speaker-led (low)** | live talks, a room you are presenting to | one idea per slide, large type, 1-3 bullets, generous space, more slides if needed |
| **Reading-first (high)** | handouts, async circulation, documents people scroll alone | self-contained slides, structured grids and tables, 4-8 bullets or 4-6 cards, tighter but still deliberate |

Mixed signals resolve to the nearer mode, never a mushy middle: live persuasion → speaker-led; circulated afterwards → reading-first. **If content exceeds the mode, split into more slides. Never shrink type to fit.**

**Before modifying an existing deck**, count what is already on the slide against the density limit. Adding an image to a full slide means moving content out or splitting the slide, not squeezing.

**After ANY change, verify by rendering — not by reading the diff.** Check that no text overflows its container, no panels overlap (grid children can visually cover each other while `scrollHeight` still reports clean), titles do not wrap unexpectedly, and the stage is still 16:9. Reorganise proactively and say that you did; do not wait to be asked.

**Authenticity is non-negotiable.** No fabricated product screenshots, no `<div>`-built fake UI, no invented or pseudo-official marks. Real capture, real asset, or leave the slot empty and say so.

## Portability: inline every asset before a file leaves the machine

A page that references `src="assets/logo.png"` renders perfectly on the machine that authored it, because the folder sits next door, and shows a broken-image icon the moment the file is shared on its own. **Relative asset paths are a local convenience and a shipping defect.**

**The rule.** If an artifact will ever be sent — email, chat, a shared drive, an upload, a handover — it ships as ONE self-contained `.html` with every image, icon and font embedded as a `data:` URI. Keep the loose assets folder as the working source; inline as the last step before sending.

```python
import base64, os, re
p = "Deck.html"; s = open(p).read()
for r in sorted(set(re.findall(r'src="((?!data:)[^"]+)"', s))):
    assert os.path.exists(r), "missing asset: " + r
    ext  = os.path.splitext(r)[1].lstrip(".").lower()
    mime = {"png":"image/png","jpg":"image/jpeg","jpeg":"image/jpeg","svg":"image/svg+xml",
            "gif":"image/gif","webp":"image/webp"}.get(ext, "image/" + ext)
    s = s.replace('src="%s"' % r, 'src="data:%s;base64,%s"'
                  % (mime, base64.b64encode(open(r, "rb").read()).decode()))
open(p, "w").write(s)
print("remaining external:", re.findall(r'src="(?!data:)([^"]+)"', s))   # must be []
```

**Verification is a copy test, never a local eyeball.** "It renders fine here" proves nothing while the folder is still next door. Copy the file ALONE into an empty directory and render THAT.

**Size guidance.** Base64 costs ~33% over raw bytes. Logos and icons are free; full-page screenshots are not. Under ~2 MB inline without thinking; 2–10 MB inline but downscale first (JPEG for photographic captures, PNG where UI text must stay crisp); over ~10 MB, stop and ask — zipping the folder or hosting the images may serve the recipient better than a file their mail gateway will bounce.

Some publishing targets enforce a strict content-security policy that blocks every external host, so the same inlining is mandatory there for a different reason.

## Artifact families + screenshot sanitization

When one artifact must serve multiple audiences, never let a single file quietly serve them all. **Fork explicitly**, same folder, bracketed suffixes — `[Private]` (full detail, operator's copy), `[Public]` (external eyes: names, deal terms, live actions removed), `[Internal]` (method visible, sensitive specifics withheld — and the withholding itself is not announced on the page). All versions share one assets folder; numbers must stay identical across versions (single-source rule).

**Blur-sanitizing a dashboard screenshot** (beats cropping): take the FULL-page 2× screenshot so structure and depth stay visible, then Gaussian-blur exactly the sensitive regions (names, terms, action lists) while aggregates, funnels and headers stay sharp. Pre-swap any identifying string embedded in a sharp region via a temp copy of the HTML before shooting. Present the result in a fixed-height scrollable container — the blurred zones read as "real operations, withheld," which is more credible than absence. Caption: max two clauses (what's blurred · where the numbers come from).

## Annotation system + honest-claims harness

**Asterisk annotations**: any stat, claim, or headline word needing qualification gets a trailing `*` (muted, not accent). ALL asterisk notes collect into ONE block: bottom-left, caption size, `line-height:2`, each note on its own line prefixed `*`, ordered by where their markers appear. The block's left edge aligns with the CONTENT BODY's visible left edge (e.g. the first big stat numeral), not the page margin — and stays clearly separated from both content and footer. Annotations stay out of the body (the body stays the hero) but remain findable in one place.

**Honest-claims harness** (what makes numbers defensible in front of a tough audience):
- **Measure, don't estimate.** If a number can be computed from logs/records, compute it and be ready to show the method.
- **Pair hero metrics with a reference class.** A conversion or performance number is meaningless alone; add a benchmark annotation line (`*Benchmark: industry range X–Y% …`) so the reader can place it.
- **Keep the zero visible.** An honest "0 so far" out-converts hype with any experienced audience.
- **Claim language must match the system.** If humans gate the sends, say "autonomous-first, human-gated" — an absolute like "100% auto" contradicts the harness and invites the attack.
- **Derived numbers must chain.** If phase targets ladder up (4 units × ~$X + channel ~$Y = headline), make each phase's math derive the next phase's inputs — reviewers check the joints, not the totals.

## Common mistakes (the generic-AI-page tells)

- Purple/blue gradient hero → delete; whitespace + big type is the hero
- 6+ font sizes, weights 300/500/700/900 → collapse to the scale
- Cards with borders AND shadows AND radius → pick radius + bg tint only
- Emoji as icons in headings → remove
- Centered long paragraphs → center only ≤2-line text; prose is left-aligned
- Cramped 60–80px sections → 160px; scrolling is free, clutter is not
- Entrance animations to add "polish" → this edition ships static; polish is spacing
