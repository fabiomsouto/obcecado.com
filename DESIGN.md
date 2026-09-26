---
name: obcecado
description: A quiet sheet around one lit object, the receiver's display.
colors:
  deep-teal: "#0a7064"
  deep-teal-dark: "#34b3a4"
  deep-teal-ink: "#ffffff"
  deep-teal-ink-dark: "#03201c"
  cool-ground: "#eef1f0"
  cool-ground-dark: "#0a0d0e"
  sheet: "#f8faf9"
  sheet-dark: "#111617"
  ink: "#0f1516"
  ink-dark: "#e3eae8"
  muted: "#4d5957"
  muted-dark: "#97a5a2"
  hairline: "#d3dad8"
  hairline-dark: "#232d2e"
  glass: "#060808"
  glass-dark: "#030404"
  glass-edge: "#1c2527"
  glass-edge-dark: "#2c393b"
  bezel: "#c9d1cf"
  bezel-dark: "#1a2224"
  vfd-phosphor: "#72f2e2"
  vfd-dim: "#4a8f87"
  vfd-off: "#1d3634"
  vfd-ghost: "#0f1e1d"
typography:
  display:
    fontFamily: "Saira, system-ui, sans-serif"
    fontSize: "clamp(3.25rem, 11vw, 5.75rem)"
    fontWeight: 600
    lineHeight: 0.95
    letterSpacing: "-0.025em"
  headline:
    fontFamily: "Saira, system-ui, sans-serif"
    fontSize: "clamp(1.1875rem, 2.2vw, 1.4375rem)"
    fontWeight: 400
    lineHeight: 1.35
    letterSpacing: "-0.01em"
  title:
    fontFamily: "Saira, system-ui, sans-serif"
    fontSize: "1.375rem"
    fontWeight: 600
    lineHeight: 1.25
    letterSpacing: "-0.01em"
  body:
    fontFamily: "Saira, system-ui, sans-serif"
    fontSize: "1.0625rem"
    fontWeight: 400
    lineHeight: 1.6
  label:
    fontFamily: "Saira, system-ui, sans-serif"
    fontSize: "0.875rem"
    fontWeight: 400
    lineHeight: 1.3
  vfd-readout:
    fontFamily: "DotGothic16, ui-monospace, monospace"
    fontSize: "clamp(2.25rem, 9vw, 4.5rem)"
    fontWeight: 400
    lineHeight: 1.15
    letterSpacing: "0.08em"
  vfd-legend:
    fontFamily: "DotGothic16, ui-monospace, monospace"
    fontSize: "clamp(0.75rem, 2.4vw, 1rem)"
    fontWeight: 400
    letterSpacing: "0.08em"
rounded:
  focus: "2px"
  segment: "4px"
  control: "6px"
  box: "8px"
  object: "10px"
spacing:
  gutter: "clamp(1rem, 4vw, 3rem)"
  wide: "72rem"
  measure: "40rem"
  xs: "0.25rem"
  sm: "0.5rem"
  md: "1rem"
  lg: "1.5rem"
  xl: "3rem"
components:
  button-primary:
    backgroundColor: "{colors.deep-teal}"
    textColor: "{colors.deep-teal-ink}"
    typography: "{typography.body}"
    rounded: "{rounded.control}"
    padding: "0.75rem 1.25rem"
  theme-toggle:
    textColor: "{colors.muted}"
    rounded: "{rounded.control}"
    size: "2.5rem"
  theme-toggle-hover:
    backgroundColor: "{colors.sheet}"
    textColor: "{colors.ink}"
  vfd-display:
    backgroundColor: "{colors.glass}"
    textColor: "{colors.vfd-phosphor}"
    typography: "{typography.vfd-readout}"
    rounded: "{rounded.object}"
    padding: "clamp(0.9rem, 2.5vw, 1.4rem) clamp(1rem, 3.5vw, 2.25rem)"
  vfd-input:
    textColor: "{colors.vfd-dim}"
    typography: "{typography.vfd-legend}"
    rounded: "{rounded.segment}"
    padding: "0.5rem 0.25rem 0.65rem"
  vfd-input-selected:
    textColor: "{colors.vfd-phosphor}"
  hookup-node:
    backgroundColor: "{colors.sheet}"
    textColor: "{colors.ink}"
    rounded: "{rounded.box}"
    padding: "0.7rem 0.95rem"
  hookup-node-board:
    backgroundColor: "{colors.glass}"
    textColor: "{colors.vfd-phosphor}"
    rounded: "{rounded.box}"
    padding: "0.7rem 0.95rem"
  kit-card:
    backgroundColor: "{colors.sheet}"
    textColor: "{colors.ink}"
    rounded: "{rounded.box}"
    padding: "1.25rem 1.25rem 0.5rem"
  kit-card-unavailable:
    textColor: "{colors.muted}"
    rounded: "{rounded.box}"
    padding: "1.25rem 1.25rem 0.5rem"
  project-card:
    backgroundColor: "{colors.sheet}"
    textColor: "{colors.ink}"
    rounded: "{rounded.object}"
    padding: "clamp(1.25rem, 3vw, 2rem)"
---

# Design System: obcecado

## Overview

**Creative North Star: "The Lit Display on a Quiet Sheet"**

The site is a pale, cool, almost silent sheet with one object on it that glows: a receiver's front-panel VFD, black glass with a teal dot-matrix readout. Everything outside the display is typographic and flat: Saira, a squared grotesque in the spirit of hi-fi faceplate lettering, on a cool grey ground, hairline rules between sections, one deep teal accent. The display is the only thing that emits light, and it is the same dark glass in both themes, so it reads as a physical object laid on the page rather than a themed panel.

Status is expressed the way the hardware expresses it, as lit or unlit indicators: a legend where a few words glow and the rest sit drawn but dark, an underline segment that lights under the selected input, a lamp that is either filled and glowing or an empty ring. Density is calm and reading-led: a single measured text column, section headings hung in a left rail on wide screens, generous vertical gaps.

The world replaced a brushed-metal hi-fi faceplate. The sheet carries no material texture; the only texture in the system is the display's own dot grid and glass sheen, which belong to the object.

**Key Characteristics:**
- Light theme by default; dark follows `prefers-color-scheme` unless `data-theme` on `<html>` overrides it (header toggle, persisted in localStorage).
- One lit object: the VFD display, dark glass in both themes.
- DotGothic16 appears only on display content; everything else is Saira.
- Status as lit versus unlit, never as coloured badges.
- Flat sheet, hairline rules, a single deep teal accent.

## Colors

A near-neutral cool grey-green sheet, one deep teal accent, and a separate phosphor palette that lives only inside the display glass.

### Primary
- **Deep Teal** (`deep-teal`; dark theme `deep-teal-dark`): the only accent on the sheet. Primary buttons, link hover, focus rings, text selection, the lit compatibility lamp, ordered-list numerals, the project card's hover border. Text on it uses **Deep Teal Ink** (`deep-teal-ink`, white in light; `deep-teal-ink-dark`, near-black teal in dark).

### Secondary
- **VFD Phosphor** (`vfd-phosphor`): lit characters and segments inside the display, with a soft glow of the same hue. Also the text of the one hookup node that represents the board. Never used on the sheet itself.
- **VFD Dim** (`vfd-dim`): unselected input legends and the standby readout; present but not lit.
- **VFD Off** (`vfd-off`): indicator legends drawn unlit (MUTE, SLEEP); intentionally near-invisible, decorative and `aria-hidden`.
- **VFD Ghost** (`vfd-ghost`): the 5px grid of unlit dots behind readout characters.

### Neutral
- **Cool Ground** (`cool-ground` / `cool-ground-dark`): page background; mirrored in the `theme-color` meta.
- **Sheet** (`sheet` / `sheet-dark`): one step lighter (or lighter-than-ground in dark) for boxes that sit on the page: hookup nodes, kit cards, project cards, toggle hover.
- **Ink** (`ink` / `ink-dark`): body text, headings, cable lines in the hookup diagram, the available kit's solid border.
- **Muted** (`muted` / `muted-dark`): secondary text: notes, captions, nav links, table headers, unordered-list markers, unlit lamps.
- **Hairline** (`hairline` / `hairline-dark`): 1px section rules, table rows, node borders, the colophon rule.
- **Glass** (`glass` / `glass-dark`), **Glass Edge** (`glass-edge` / `glass-edge-dark`), **Bezel** (`bezel` / `bezel-dark`): the display body, its inner edge and divider, and the 5px ring that seats it on either sheet.

### Named Rules
**The One Lit Object Rule.** Only the display (and the board node that stands for it) emits light. Glow (`text-shadow`/`box-shadow` in phosphor) never appears on sheet elements; the single exception is the lit compatibility lamp, which glows in deep teal because it is itself an indicator.

**The Same Glass Rule.** The display keeps its dark glass and phosphor palette in both themes. Only its glass, edge and bezel shade shift slightly to seat it on the dark sheet; the phosphor values never change.

**The Lit Not Coloured Rule.** Status is lit or unlit: filled glowing lamp versus empty ring, bright legend versus drawn-dark legend. No red/green badges, pills or status colours.

## Typography

**Display Font:** Saira (with system-ui, sans-serif), self-hosted variable, weight 100–900 and width 50–125%. Headings run slightly wide (`font-stretch` 108–110%); body stays at 100%. Don't push headings wider: the old, very wide heading style was rejected.
**Body Font:** Saira
**Label/Mono Font:** DotGothic16 (with ui-monospace, monospace), self-hosted, `font-display: block`, display content only

**Character:** A tight, confident grotesque for everything a person reads, and a dot-matrix face that only ever appears as something the receiver would show. The contrast between the two is the world.

### Hierarchy
- **Display** (600, 110% width, `clamp(3.25rem, 11vw, 5.75rem)`, 0.95, -0.025em): the page's name (Phonkyo, obcecado). One per page. Project names on the home cards use a smaller tier of the same treatment (600, 110% width, `clamp(2rem, 6vw, 3.25rem)`, 1, -0.025em).
- **Headline** (400, `clamp(1.1875rem, 2.2vw, 1.4375rem)`, 1.35, -0.01em): the lede under the display, max 28ch, `text-wrap: pretty`. The home intro prose uses the same range capped at 1.375rem.
- **Title** (600, 108% width, 1.375rem, 1.25, -0.01em, balanced): section headings, hung in the left rail on wide screens. Subheads (kit names) are 600 at body size.
- **Body** (400, 1.0625rem, 1.6): running text inside a 40rem measure.
- **Label** (400, 0.875rem, 1.3): figure captions, hookup notes and cable labels, muted. Table headers go to 0.8125rem/500; cta notes and colophon 0.9375rem.
- **VFD Readout** (DotGothic16, `clamp(2.25rem, 9vw, 4.5rem)`, 0.08em): the big display word; the source field beside it is `clamp(1rem, 3.2vw, 1.75rem)`, 0.1em, right-aligned.
- **VFD Legend** (DotGothic16, `clamp(0.75rem, 2.4vw, 1rem)`, 0.08em, uppercase): input selectors; the indicator legend runs 0.75rem at 0.12em.

### Named Rules
**The Display Face Rule.** DotGothic16 is reserved for display content: the readout and source field, the display's link row, the indicator legend, and ordered-list numerals (which are counted steps, read like a display). Never for headings, buttons, body or site navigation outside the display.

**The Weight Ceiling Rule.** Saira runs at 400 for reading, 500 for quiet labels, 600 for emphasis and headings, 700 only on the wordmark.

## Layout

A single centred container (`wide`, 72rem) with a fluid side gutter (`gutter`). Reading text is held to `measure` (40rem).

The first viewport is a two-column hero from 60rem up (copy 5fr, board render 6fr, the render bleeding into the right gutter), with the display spanning full width below both. Below 60rem it stacks: name, lede, button, render, display.

Content below the hero is a sequence of **blocks**, each separated by a hairline top rule with 3rem above and 2rem below. From 56rem up each block becomes a two-column row: a 14rem heading rail on the left and the measured text column on the right, column gap `clamp(2rem, 5vw, 5rem)`. Below that, headings sit above their content.

Spacing steps are rem-based and reused: 0.25, 0.5, 0.75, 1, 1.25, 1.5, 2, 3rem, with `clamp()` for hero and intro padding. Breakpoints in use: 40rem (compat table and display caption), 48rem (hookup horizontal, project card two-column), 56rem (block rail), 60rem (hero two-column).

## Elevation & Depth

The sheet is flat: depth comes from the ground/sheet tonal step and hairline borders, not shadows. Only two things cast shadows, and both are objects rather than UI: the display, which is built as a glass panel seated in a bezel ring, and the board render, which floats on a soft drop shadow.

### Shadow Vocabulary
- **Display seat** (`box-shadow: inset 0 0 0 1px var(--glass-edge), inset 0 2px 10px rgb(0 0 0 / 0.8), 0 0 0 5px var(--bezel), 0 14px 30px -18px rgb(0 0 0 / 0.55)`): glass edge, inner darkness, bezel ring, then a tight under-shadow. Display only.
- **Glass sheen** (`linear-gradient(180deg, rgb(255 255 255 / 0.05), transparent 45%)` over glass): the faint top reflection on the display.
- **Render float** (`filter: drop-shadow(0 24px 28px rgb(0 0 0 / 0.18))`): the hero board render only.
- **Render stage** (dark theme only): the board has black solder mask, so both board renders sit on `--stage`, a faint cool radial pool of light, and carry `--rim`, a 0.5px pale edge. Both tokens are `none` or transparent in the light theme, where the black board already stands out on the grey sheet.
- **Phosphor glow** (`text-shadow: 0 0 8px–14px rgb(114 242 226 / 0.45–0.5)`; selected segment `box-shadow: 0 0 8px rgb(114 242 226 / 0.7)`): lit display elements.
- **Lamp glow** (`box-shadow: 0 0 6px color-mix(in srgb, var(--accent) 60%, transparent)`): the lit compatibility lamp.

### Named Rules
**The Flat Sheet Rule.** Cards, nodes, buttons and navigation never carry shadows. If something needs separation, use the sheet tone or a hairline.

## Shapes

Gently rounded, never pill-shaped, and the radius grows with the size of the thing: 2px for focus rings, 4px for display input segments, 6px for buttons and the toggle, 8px for boxes (hookup nodes, kit cards), 10px for the large objects (the display, project cards). Lamps are the only circles.

Line carries meaning in the hookup diagram, drawn like cables: a 2px solid ink line is a wire, dashed is wireless, a 6px double line is two cables side by side. The same logic marks availability: an available kit has a solid 1px ink border, an unavailable one a dashed muted border with no fill.

## Components

### Buttons
Solid, compact, one colour.
- **Shape:** gently rounded (6px).
- **Primary:** deep teal fill, deep teal ink text, 600 weight, `0.75rem 1.25rem` padding, line-height 1.2, no underline. Used for the order actions only.
- **Hover / Focus:** `filter: brightness(1.12)` over 0.2s ease-out; focus is the global 2px deep teal outline at 3px offset.
- There is no secondary button; secondary actions are plain underlined links (1px underline at 40% current colour, full colour and accent on hover).

### Theme Toggle
A 2.5rem square icon button in the masthead: no fill, muted stroke icon (1.6 stroke SVG sun/moon, showing the theme you would switch to); on hover, sheet background and ink stroke. Label updates to "Switch to light/dark theme".

### Cards / Containers
- **Kit card:** 8px, sheet fill, 1px solid ink border, `1.25rem 1.25rem 0.5rem`, price in 600 tabular numerals. Unavailable: dashed muted border, no fill, muted text.
- **Project card (home):** 10px, sheet fill, 1px hairline border, fluid padding; hover turns the border deep teal over 0.2s. Render and text side by side from 48rem.
- **Hookup node:** 8px, sheet fill, hairline border, 600 name over a muted 0.875rem note.

### Navigation
The masthead is a single row: wordmark (Saira 700, `.com` in muted 500) pushed left, project links in muted with the current page in ink, then the theme toggle. No underlines, no background. The colophon mirrors it at the foot: hairline top rule, muted 0.9375rem text.

### VFD Display (signature)
Black glass panel with a phosphor readout. From top: the indicator legend (lit words glow, the rest drawn in `vfd-off`), the large readout over a ghost-dot grid, a right-aligned source field, then a hairline in glass-edge and a row of links styled as input legends (`nav`, "On this page": How it works, Board, Receivers, Order) that jump to page sections with smooth scrolling. Links sit in `vfd-dim` with their 3px segment at 35% opacity; hover or focus lights the label and segment in phosphor with a glow. The readout always shows DOCK and the source field shows RI LINK. On load it steps STANDBY, POWER ON, DOCK once (standby readout in `vfd-dim` without glow); reduced motion shows the end state. A fixed muted caption below the glass summarises what the board does.

### Hookup Diagram
A chain of nodes joined by cable lines, vertical on phones and horizontal from 48rem with labels above and below each cable so lines meet boxes at their middle. The node that represents the board is drawn as a piece of the display: glass fill, glass-edge border, phosphor text.

### Compatibility Lamps
Table rows with a lamp per feature: lit is a filled deep teal dot with a soft glow and ink text; unlit is an empty 1.5px ring at 60% in muted text. Below 40rem each receiver collapses into a feature-per-line list with the lamp on the right.

## Do's and Don'ts

### Do:
- **Do** keep the display dark glass with phosphor text in both themes, seated in its bezel ring.
- **Do** express status as lit versus unlit (glowing fill or legend versus empty ring or dark legend).
- **Do** keep DotGothic16 on display content only: readout, source field, the display's link row, indicator legend, ordered-list numerals.
- **Do** separate sections with 1px hairline rules and hang section headings in a 14rem left rail from 56rem up.
- **Do** use deep teal as the only accent on the sheet, and white or near-black teal ink on it depending on theme.
- **Do** draw connections as lines: solid for a wire, dashed for wireless, double for a pair.
- **Do** honour reduced motion: transitions off, the display shows its end state.

### Don't:
- **Don't** put brushed metal, grain or faceplate texture on the sheet; the only textures are the display's own dot grid and glass sheen.
- **Don't** give cards, nodes or buttons shadows; only the display and product renders are objects with depth.
- **Don't** use phosphor colour or glow outside the display and the board node.
- **Don't** use coloured status badges or pills; use lamps.
- **Don't** set headings, buttons, navigation or body copy in DotGothic16.
