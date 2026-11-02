---
version: 1
slug: "document-review"
primary_target: "document-review"
related_targets: []
---

## Direction contract

THESIS: Redline doesn't just flag risk — it locates it, showing exactly where danger sits in the terrain of your own document, refusing the generic "AI legal chatbot" card-list default that treats every flag as an identical badge.

OWN-WORLD: Topographic trail-map system. Ground: warm parchment neutral (#F3EEE2) with fine ink-brown contour-style rules (#3B362C); one hazard red (#C0202B) as the sole accent, reserved for Critical danger zones and the severity legend. Type: Overpass (highway/trail-sign grotesque heritage) for headings, labels, and the legend; system-ui stack for body prose (quoted sentences, counter-offers) — a workhorse Operate face, not a designed one; JetBrains Mono for coordinates, clause numbers, and tallies. Components read as map elements: a legend key, contour-shaded risk zones, a "you are here" marker tied to scroll position.

STORY: A freelancer opens an uploaded document and sees it rendered as terrain — safe ground in neutral ink, danger zones shaded in red intensity by tier, a legend translating Critical/Moderate/Worth-noting the way a trail map translates easy/moderate/black-diamond. They understand instantly: this document has been surveyed, here's where the hazards are, and here's the route (counter-offer) around each one.

FIRST VIEWPORT: A single scrollable document pane on the left rendered as parchment terrain, its full text visible with risk zones contour-shaded in graduated red intensity by severity tier directly over the source sentences; a fixed right-hand legend/rail lists every flag as a hazard-map key entry (icon, severity word, one-line label), synced to a "you are here" marker that tracks scroll position in the left pane; the plain-English summary sits above both as a short "trailhead briefing." Deliberate adaptation: the in-text risk zones render as flat graduated-opacity red tints, not literal drawn contour-lines within the zone itself — a real hairline-contour rendering competed with the quoted legal text for attention and lost, so the flat tint was chosen to keep the source sentence legible while still reading as "shaded terrain" through color alone; the legend and background retain the literal contour-line treatment.

FORM: Hazard map / topographic direction — my top-ranked grounded candidate (position 1 of 7), presented as IMPECCABLE'S PICK against assigned index 7 (union grievance-sheet) and winning challenger 6 (festival lineup poster, size-as-severity); user-locked over both. Seed key: 1838a319.

FINISH: unreviewed and undocumented is unfinished; this build ends with the finish review, the verdict, DESIGN.md, and every shipping raster carrying its provenance.

## Scope

Mode: Operate. Surface: Document Review workspace — the core screen where a signed-in user reviews an already-uploaded document's plain-English summary, severity-ranked risk flags with source-sentence citations, and per-flag counter-offers.

Audience/job/task: A freelancer who just uploaded a contract, reviewing what Redline found before deciding what to push back on. Primary task: scan flags by severity, read each one's exact source sentence, read its counter-offer, and locate it in the actual document.

Content/constraints: Fully synthetic demo content this round (a plausible freelance-contract excerpt; 3-5 flags spanning Critical/Moderate/Worth noting, invented but grounded in the seven real red-line clause types from PRD.md; a drafted counter-offer per flag) — no real user data, no wired backend. Every flag's quoted sentence must actually appear verbatim in the demo document text (the citation guarantee holds even in the prototype). No hedging language anywhere. This is a static front-end prototype, not the ticketed engineering build (tickets 01-08 remain unbuilt).

Unresolved decisions: Q&A box and red-lines editor are separate tickets/surfaces, not built here. Dark mode not addressed this round (paper/topo-map world is inherently a light-ground artifact; revisit if requested).

## Fix round (post finish-review)

Finish-review disposition: fix. Screenshot evidence for both viewports is in `.impeccable/review/` (captured via Playwright's bundled Chromium after the project's own headless Chrome/Edge CLI proved unable to honor a specified viewport width in this environment — confirmed broken on trivial test HTML, not specific to this build).

Material fixes applied: (1) enforced the OWN-WORLD two-voice type system in code — `--body-font` (system-ui stack) now applies to all document prose, counter-offer/field-note text, the trailhead summary, legend copy, and rail flag labels; Overpass is reserved for the brand mark, headings, and tracked micro-labels. (2) Risk-flag zones are keyboard-operable (`tabindex`, `role="button"`, Enter/Space handler). (3) `aria-expanded`/`aria-controls` link every zone and rail trigger to its field-note; collapsed notes carry `aria-hidden="true"`, toggled in sync with the open state. (4) "Trailhead briefing" is a real `h1`, the document subtitle a real `h3`. (5) The rail's and page's native scrollbars are themed from the palette. (6) The "Worth noting" tier's color was unified to one value (`--worth`) via a shared CSS custom property, matching `--moderate` and `--hazard`. (7) The flat-tint zone treatment is now named above as a deliberate legibility adaptation rather than an undecided gap.
