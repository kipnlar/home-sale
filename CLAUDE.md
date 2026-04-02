# Moving Sale Project — Claude Notes

## Folder Structure
- `knowledge/` — source files and reference material (do not publish)
  - `Moving Sale Items.docx` — original listing (source of truth for items/prices)
  - `Moving Sale Items.pdf` — PDF version of listing
  - `photos/` — photos for new items not yet added to the page
  - `CLAUDE.md` — this file
- `output/` — files ready for web publishing
  - `Index.html` — the live sale page (upload this to host)

## The Sale Page (output/Index.html)
- Single self-contained HTML file; all images are base64-embedded (no external assets needed)
- Design: dark hero, cream background, Playfair Display + DM Sans fonts, warm earth tones
- Items grouped into sections: Appliances, Furniture, Accessories & Décor (+ more TBD)
- Each item card: optional photo, name, optional note, price, Now/TBD pill
- Lightbox: clicking a photo opens a full-size overlay (from docx images where available)
  - Closes on click outside, click image, ✕ button, or Escape key
- Sold items shown with SOLD badge and reduced opacity

## Items With Photos Still to Add (knowledge/photos/)
- Elliptical machine — Eliptical1.jpeg, Eliptical2.jpeg
- Kettle Bell — KettleBell.jpeg
- Luonto Sleeper sofa — LuontoSleeper1.jpeg, LuontoSleeper2.jpeg
- West Elm Chair — WesElmChair1.jpeg, WestElmChair2.jpeg

## Key Conventions
- Prices formatted with $ and commas (e.g. $1,400)
- "Now" items: green pill (when-now class)
- "TBD" items: brown pill (when-tbd class)
- Multi-photo items use class="item-photo multi" (2-column grid, 140px height)
- Single-photo items use class="item-photo" (full width, 200px height)
- Lightbox large images stored as data-large-src attribute on each <img>
- Photo images in item cards need both src (thumbnail) and data-large-src (full size)

## Workflow for Adding New Items
1. Photos go in knowledge/photos/ for reference
2. Embed photos as base64 in HTML for both thumbnail src and data-large-src
3. Save updated HTML to output/Index.html

## Important: Last Updated Date
Whenever an item is added, removed, or updated on the page, always update the "Last updated" date in the hero section to today's date. The string to update looks like:
  Last updated: Month DD, YYYY
