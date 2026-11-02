---
name: Redline
description: A topographic trail-map system for locating risk in your own contract
colors:
  paper: "#F3EEE2"
  paper-deep: "#EAE2D1"
  ink: "#2A271F"
  ink-soft: "#55503F"
  contour: "#B9AF95"
  contour-strong: "#8D836A"
  hazard: "#B31B23"
  hazard-deep: "#7F1219"
  moderate: "#C97A3F"
  worth: "#7C8451"
  rule: "rgba(42,39,31,0.16)"
  focus: "#1C5C8A"
typography:
  display-hero:
    fontFamily: "Overpass, system-ui, -apple-system, 'Segoe UI', sans-serif"
    fontSize: "3.1rem"
    fontWeight: 800
    lineHeight: 1.08
    letterSpacing: "-0.025em"
  display-hero-min:
    fontFamily: "Overpass, system-ui, -apple-system, 'Segoe UI', sans-serif"
    fontSize: "2rem"
    fontWeight: 800
    lineHeight: 1.08
    letterSpacing: "-0.025em"
  display:
    fontFamily: "Overpass, system-ui, -apple-system, 'Segoe UI', sans-serif"
    fontSize: "1.5rem"
    fontWeight: 700
    lineHeight: 1.2
    letterSpacing: "-0.01em"
  display-section:
    fontFamily: "Overpass, system-ui, -apple-system, 'Segoe UI', sans-serif"
    fontSize: "1.32rem"
    fontWeight: 700
    lineHeight: 1.25
    letterSpacing: "-0.015em"
  summary:
    fontFamily: "system-ui, -apple-system, 'Segoe UI', Roboto, Arial, sans-serif"
    fontSize: "1.12rem"
    fontWeight: 400
    lineHeight: 1.55
  brand:
    fontFamily: "Overpass, system-ui, -apple-system, 'Segoe UI', sans-serif"
    fontSize: "1.05rem"
    fontWeight: 800
    lineHeight: 1.2
    letterSpacing: "-0.01em"
  body:
    fontFamily: "system-ui, -apple-system, 'Segoe UI', Roboto, Arial, sans-serif"
    fontSize: "1.02rem"
    fontWeight: 400
    lineHeight: 1.75
  body-small:
    fontFamily: "system-ui, -apple-system, 'Segoe UI', Roboto, Arial, sans-serif"
    fontSize: "0.96rem"
    fontWeight: 400
    lineHeight: 1.6
  body-quote:
    fontFamily: "system-ui, -apple-system, 'Segoe UI', Roboto, Arial, sans-serif"
    fontSize: "0.86rem"
    fontWeight: 400
    lineHeight: 1.5
  cta:
    fontFamily: "'JetBrains Mono', ui-monospace, monospace"
    fontSize: "0.9rem"
    fontWeight: 600
    lineHeight: 1.2
    letterSpacing: "0.14em"
  label:
    fontFamily: "Overpass, system-ui, -apple-system, 'Segoe UI', sans-serif"
    fontSize: "0.8rem"
    fontWeight: 400
    lineHeight: 1.3
    letterSpacing: "0.12em"
  label-small:
    fontFamily: "'JetBrains Mono', ui-monospace, monospace"
    fontSize: "0.72rem"
    fontWeight: 400
    lineHeight: 1.3
    letterSpacing: "0.1em"
  mono:
    fontFamily: "'JetBrains Mono', ui-monospace, monospace"
    fontSize: "0.8rem"
    fontWeight: 400
    lineHeight: 1.3
    letterSpacing: "0.01em"
  mono-data:
    fontFamily: "'JetBrains Mono', ui-monospace, monospace"
    fontSize: "0.82rem"
    fontWeight: 400
    lineHeight: 1.3
    letterSpacing: "0.01em"
  mono-small:
    fontFamily: "'JetBrains Mono', ui-monospace, monospace"
    fontSize: "0.78rem"
    fontWeight: 400
    lineHeight: 1.3
    letterSpacing: "0.01em"
rounded:
  sm: "2px"
  stamp: "3px"
  md: "4px"
  scrollbar: "5px"
spacing:
  xs: "8px"
  sm: "10px"
  md: "18px"
  lg: "22px"
  xl: "40px"
components:
  zone-critical:
    backgroundColor: "rgba(179,27,35,0.16)"
    rounded: "{rounded.sm}"
    padding: "0 0.08em"
  zone-critical-hover:
    backgroundColor: "rgba(179,27,35,0.26)"
  zone-moderate:
    backgroundColor: "rgba(179,27,35,0.09)"
    rounded: "{rounded.sm}"
    padding: "0 0.08em"
  zone-worth:
    backgroundColor: "rgba(179,27,35,0.045)"
    rounded: "{rounded.sm}"
    padding: "0 0.08em"
  rail-item-btn:
    backgroundColor: "transparent"
    textColor: "{colors.ink}"
    rounded: "{rounded.md}"
    padding: "10px 10px 10px 14px"
  rail-item-btn-active:
    backgroundColor: "{colors.paper-deep}"
  field-note-card:
    backgroundColor: "{colors.paper-deep}"
    rounded: "{rounded.md}"
    padding: "18px 20px 20px"
---

# Design System: Redline

## Overview

**Creative North Star: "The Surveyed Document"**

Redline renders a legal document as terrain rather than as a list of chat-bot flags. Danger is a place you can point to, not a badge floating beside a paragraph: risk sits directly over the source sentence that caused it, shaded by severity the way a trail map shades a slope. Safe ground stays neutral ink on parchment; only the hazard-tint zones and the sparing hazard-red accent break the calm. The system is deliberately unglamorous where it needs to be legible — body prose, quoted clauses, and counter-offers run in a plain system-ui workhorse face so the words a user must trust are never stylized — and reserves the designed Overpass grotesque and JetBrains Mono for wayfinding scaffolding (headings, labels, legend, coordinates, tallies) that frames the document without competing with it.

This is a light-only, code-shipped world (no dark mode this round; the parchment ground is treated as structural, not a theme option). It carries no drawn shadows as a device: the one shadow in the build is a 1px ambient hairline under the field-note card, not a hard offset or neobrutalist block shadow — this is not that kind of world.

**Key Characteristics:**
- Parchment ground with hairline ink-brown contour rules; one hazard red reserved for danger and the legend
- Two-voice type system: a designed grotesque (Overpass) for wayfinding scaffolding, a plain system-ui stack for document prose and quoted legal text
- Risk zones as flat graduated-opacity red tints laid directly over source sentences — a deliberate legibility adaptation, not a missing feature
- Map-metaphor components: severity legend, "you are here" scroll marker, field-note expansion cards
- Fully keyboard-operable risk zones with a synced ARIA expand/collapse pattern

## Colors

A warm, low-saturation parchment field with a single reserved hazard-red accent; everything else is ink, ink-soft, and contour-brown.

### Primary
- **Hazard Red** (#B31B23): The sole accent color. Reserved for the Critical severity tier — zone tint, legend swatch, rail icon, "you are here" emphasis — and the brand mark. Never used decoratively elsewhere.
- **Hazard Deep** (#7F1219): Darker step of hazard red, used for the "Trailhead briefing" label and jurisdiction-note emphasis text where full hazard red would be too loud against parchment.

### Secondary
- **Moderate Amber-Brown** (#C97A3F): The Moderate severity tier — zone tint, legend swatch, rail icon.
- **Worth-Noting Olive** (#7C8451): The Worth-noting severity tier — zone tint, legend swatch, rail icon. Unified to a single custom property (`--worth`) so the tier never drifts to a second value across zone, legend, and rail.

### Neutral
- **Parchment** (#F3EEE2): Page ground. The base of the "terrain."
- **Parchment Deep** (#EAE2D1): Recessed surface — field-note cards, active/hovered rail rows — one step down from the page ground, not a bordered panel.
- **Ink** (#2A271F): Primary text color.
- **Ink Soft** (#55503F): Secondary text — doc metadata, mono labels, field-note body copy, legend copy.
- **Contour** (#B9AF95) / **Contour Strong** (#8D836A): The hairline rule vocabulary — background contour-ring texture, clause-number marks, dashed jurisdiction-note divider, themed scrollbar thumb.
- **Rule** (rgba(42,39,31,0.16)): Hairline dividers between header/pane/rail regions and legend rows.
- **Focus** (#1C5C8A): The one non-palette color in the system — a blue reserved exclusively for `:focus-visible` outlines, chosen to be legible against parchment and distinct from every semantic severity color so focus is never mistaken for a severity tint.

### Named Rules
**The One Hazard Rule.** Hazard red is reserved for Critical severity and the brand mark only. Moderate and Worth-noting each carry their own distinct hue (amber-brown, olive) rather than a lighter tint of hazard red — severity tiers are colors apart, not intensities of one color, except within a single zone's own tint ramp.

**The Focus-Is-Not-Severity Rule.** Focus rings use `--focus` (#1C5C8A), a blue found nowhere else in the palette, so keyboard focus is never visually confused with a Moderate or Critical tint.

## Typography

**Display/Label Font:** Overpass (with system-ui, -apple-system, "Segoe UI" fallback)
**Body Font:** system-ui, -apple-system, "Segoe UI", Roboto, Arial, sans-serif
**Label/Mono Font:** JetBrains Mono (with ui-monospace, monospace fallback)

**Character:** A trail-sign grotesque (Overpass) handles wayfinding — brand, headings, tracked micro-labels, legend — while a deliberately undesigned system-ui stack carries every word that must be trusted verbatim: document prose, quoted source sentences, counter-offer text, field-note body copy. JetBrains Mono marks anything coordinate-like: clause numbers, document metadata, tallies, severity labels.

### Hierarchy
- **Display** (700, 1.5rem, 1.2 line-height, -0.01em tracking): Document section headings (`h2`) inside the document pane.
- **Title** (800, 1.05rem, -0.01em tracking): The Redline brand mark/wordmark in the header.
- **Body** (400, 1.02rem body / 0.96rem field-note, 1.75 / 1.6 line-height, max 74ch): Document paragraphs, quoted clauses, counter-offer text, field-note explanations. Always system-ui, never Overpass.
- **Label** (400, 0.8rem, 0.12em tracking, uppercase): "Trailhead briefing," field-note row labels ("Why flagged," "Counter-offer"), rail severity words. Always JetBrains Mono.
- **Mono/Data** (400–600, 0.78–0.82rem): Clause numbers, document metadata line, "you are here" marker, tally counts.

### Named Rules
**The Two-Voice Rule.** Overpass is reserved for wayfinding scaffolding (brand, headings, tracked labels, legend chrome); system-ui carries every word the user must weigh and trust (document text, quotes, counter-offers). No document prose is ever set in Overpass, and no label/legend chrome is ever set in system-ui.

## Layout

Two-column workspace grid: a fluid document pane (`minmax(0,1fr)`) beside a fixed 340px legend rail, collapsing to a single column under 880px (rail moves below the document, sticky positioning drops to static). The document pane and header cap prose width at 74ch regardless of viewport. Horizontal page padding scales with `clamp(20px, 4vw, 56px)`. The rail is `position: sticky; top: 0` with its own themed scrollbar and independent scroll region up to `100vh`. A fixed, full-bleed `.contour-ground` layer sits behind all content at `z-index: -1` as the page's base texture, independent of the scrolling content layers above it.

## Elevation & Depth

Flat by default. The system does not use elevation to separate layers — depth reads through parchment-to-parchment-deep tonal shifts (page ground vs. recessed card) and hairline rule dividers, not shadows. The one shadow in the build is a near-invisible 1px ambient line under the field-note card (`0 1px 0 rgba(42,39,31,.05)`), used to lift it barely off the recessed surface beneath it — not a hard offset, not a neobrutalist block shadow, and not present anywhere else.

### Named Rules
**The Tonal-Not-Lifted Rule.** Depth is conveyed by moving one step down the neutral ramp (parchment → parchment-deep) plus a hairline rule, never by a drop shadow. The single ambient 1px shadow on the field-note card is the sole, deliberately minor exception.

## Shapes

Small, consistent corner radii throughout: 2px on inline risk-zone tints and quote highlights, 4px on cards, legend containers, and rail buttons. No large radii, no fully rounded rectangles except the small tally dots and legend swatches (which are true circles). Borders are hairline (1px, `--rule` or `--contour`) and dividing, never decorative frames; the jurisdiction note uses a 1px dashed `--contour` rule to mark it as an aside distinct from the field-note's solid dividers.

## Components

### Risk Zones (signature component)
Inline `<span>` highlights laid directly over the exact source sentence they flag — not a separate card or badge. Background is a flat graduated-opacity red tint keyed to severity (`--hazard-tint-critical` 0.16/0.26 hover, `--hazard-tint-moderate` 0.09, `--hazard-tint-worth` 0.045), 2px radius, `cursor: pointer`. This flat-tint treatment is a deliberate adaptation from a literal drawn-contour-line treatment: contour lines inside the zone competed with the quoted legal text and lost, so color-only shading was chosen to keep the source sentence legible. The literal contour-line treatment is retained elsewhere (background texture, legend). Every zone is keyboard-operable: `tabindex="0"`, `role="button"`, `aria-expanded`, `aria-controls`, with Enter/Space handlers mirroring the click handler.

### Field Notes
The expand/collapse detail card revealed by a risk zone or its matching rail entry. Built on a `grid-template-rows: 0fr → 1fr` transition (not `max-height`) for a smooth reveal, `cubic-bezier(.16,1,.3,1)`, 0.38s. Background is parchment-deep, 4px radius, containing a "Why flagged" row and a "Counter-offer" row, each with a small inline SVG icon matching the triggering severity color. Collapsed notes carry `aria-hidden="true"`; only one field note is open at a time (opening one closes any other). A non-hedging jurisdiction note (dashed top border) appears only on jurisdiction-sensitive flags (e.g. non-compete).

### Severity Legend
A bordered, 4px-radius list in the rail: one row per tier, each with a distinct SVG glyph shape (triangle = Critical, diamond = Moderate, circle = Worth noting) stroked in the tier's color, plus a one-line plain-English description. Shape, not just color, distinguishes tiers — a deliberate redundant encoding.

### Rail / "You Are Here" Marker
A sticky right-hand rail listing every flag as a legend-style entry (icon, severity label in mono, one-line description). A small triangular marker appears beside the active entry, synced via `IntersectionObserver` to whichever risk zone is centered in the document pane's scroll position; a mono-font "You are here" readout above the flag list mirrors the same state in text.

### Navigation / Header ("Trailhead Briefing")
Brand mark (inline SVG triangle glyph, not an icon font) plus document metadata in mono, a tracked mono micro-label ("Trailhead briefing") introducing a real `h1`, then a system-ui summary paragraph and a row of tally dots (one per severity tier, colored to match).

## Do's and Don'ts

### Do:
- **Do** set all document prose, quoted source sentences, and counter-offer text in the system-ui body stack — never in Overpass.
- **Do** keep risk-zone shading as flat graduated-opacity red tint, not literal contour lines, inside quoted text — legibility of the source sentence wins that conflict by deliberate decision.
- **Do** make every interactive risk zone keyboard-operable (`tabindex`, `role="button"`, Enter/Space) and pair every trigger with `aria-expanded`/`aria-controls` on its target field note.
- **Do** reserve hazard red for the Critical tier and the brand mark; give Moderate and Worth-noting their own distinct hues rather than lighter tints of hazard red.
- **Do** convey depth with a tonal step (parchment → parchment-deep) plus a hairline rule; reserve the single ambient 1px shadow for the field-note card only.

### Don't:
- **Don't** introduce a second shadow style, a hard offset shadow, or any neobrutalist block shadow — this world uses one near-invisible ambient hairline shadow and nothing else.
- **Don't** use an icon font or a generic icon library glyph; icons in this build are hand-drawn inline SVG matched to the map metaphor (triangle/diamond/circle severity shapes, the trailhead brand mark).
- **Don't** style body prose or quoted legal text in Overpass, and don't style labels, legend, or headings in the system-ui body stack — the two-voice split is load-bearing for the map/document distinction.
- **Don't** use the `--focus` blue for anything but `:focus-visible` outlines; it exists specifically to stay distinct from every severity color.
