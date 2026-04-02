# Moving Sale Project — Claude Notes

## Folder Structure
- `index.html` — the live sale page (served via GitHub Pages)
- `photos/` — all item photos, referenced by index.html and tbd.html
- `knowledge/` — source files and reference material (not published)
  - `Moving Sale Items.docx` — original listing (source of truth for items/prices)
  - `Moving Sale Items.pdf` — PDF version of listing
  - `photos/` — original source photos (subset of what's in top-level photos/)

## The Sale Page (index.html)
- HTML file with images referenced as `photos/filename.jpeg` (not base64-embedded)
- Hosted on GitHub Pages; index.html must remain at the repo root
- Design: dark hero, cream background, Playfair Display + DM Sans fonts, warm earth tones
- Items grouped into sections: Appliances, Furniture, Accessories & Décor (+ more TBD)
- Each item card: optional photo, name, optional note, price, Now/TBD pill
- Lightbox: clicking a photo opens a full-size overlay
  - Closes on click outside, click image, ✕ button, or Escape key
- Sold items shown with SOLD badge and reduced opacity

## Key Conventions
- Prices formatted with $ and commas (e.g. $1,400)
- "Now" items: green pill (when-now class)
- "TBD" items: brown pill (when-tbd class)
- Multi-photo items use class="item-photo multi" (2-column grid, 140px height)
- Single-photo items use class="item-photo" (full width, 200px height)
- Lightbox large images stored as data-large-src attribute on each <img>
- Photo images in item cards need both src (thumbnail) and data-large-src (full size)

## Workflow for Adding New Items
1. Add photo files to photos/ at the repo root
2. Reference them in index.html as src="photos/filename.jpeg" and data-large-src="photos/filename.jpeg"
3. Update the "Last updated" date in the hero section (see below)

## Important: Last Updated Date
Whenever an item is added, removed, or updated on the page, always update the "Last updated" date in the hero section to today's date. The string to update looks like:
  Last updated: Month DD, YYYY

## Git
- Always commit to the main branch
