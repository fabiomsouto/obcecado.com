---
version: 1
slug: "layouts-product-html"
primary_target: "layouts/product.html"
related_targets: ["content/phonkyo/index.md"]
---

# Phonkyo product page

Scope: `layouts/product.html` with `content/phonkyo/index.md`; the home, 404 and page layouts share its world. Visitor mode: Persuade.

Audience and job: a receiver owner (Onkyo or other RI receiver), technical or not, deciding whether Phonkyo works with their receiver and ordering by email. Proof on hand: KiCad board renders, the TX-8020 compatibility row, the board's specs. Constraints: light and dark mode (system default plus a remembered header toggle); phones first-class; keep the hookup diagram and a reworked input dial (now the display's link row); no brushed metal or skeuomorphic texture.

## Direction contract

THESIS: The page is built around the receiver's front display switching to DOCK. It refuses the generic product-page stack of hero, feature cards and spec grid, and it refuses the old brushed-metal faceplate.

OWN-WORLD: Black glass display strip with a teal VFD dot-matrix readout (DotGothic16) and ghosted unlit indicators, the same dark object in both themes. Around it, a quiet sheet: near-black in dark mode, pale cool grey in light, set in Geist, hairline rules, deep teal as the only accent. Status reads as lit or unlit indicators, never as coloured badges.

STORY: The visitor sees the display go from STANDBY to DOCK, understands "my receiver turns itself on and switches over", checks the hookup, the board and their receiver in the table, and emails an order.

FIRST VIEWPORT: Left: Phonkyo name, one-line promise, "Order for €30" button with shipping note. Right: iso board render. Full width below them: the display strip, with a large readout and a row of input-style links to page sections (How it works, Board, Receivers, Order), changed at the user's request from the clickable source switcher. On phones: name, promise, order button, then the board, then the display.

FORM: Receiver front-panel VFD display, my ranked candidate 1 (IMPECCABLE'S PICK over the assigned assembly drawing), seed key e5690730. Code-led. Signature interaction: on load the readout goes STANDBY, POWER ON, DOCK once; the link row below the readout lights on hover or focus and jumps to page sections. Reduced motion shows the end state.

FINISH: unreviewed and undocumented is unfinished; this build ends with the finish review, the verdict, DESIGN.md, and every shipping raster carrying its provenance
