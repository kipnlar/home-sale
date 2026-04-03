# Moving Sale Project — Claude Notes

## Folder Structure
- `index.html` — "Available Now" sale page (served via GitHub Pages at repo root)
- `tbd.html` — "TBD" items page (linked from index.html; items available just before move)
- `photos/` — all item photos, referenced from both HTML files as `photos/filename`

## Page Structure (index.html and tbd.html)

### Document Head
- Google Fonts CDN: Playfair Display (700, 900) + DM Sans (300, 400, 500)
- All CSS is inline in a `<style>` block — no external stylesheet

### CSS Color Variables
```css
--cream: #FAF7F2        /* page background */
--warm-white: #FFFDF9   /* item card background */
--ink: #1A1612          /* dark text, hero bg, section icons */
--brown: #6B4F3A        /* TBD pill, item price, some text */
--rust: #C05A2A         /* links, alert borders */
--gold: #D4A843         /* hero accents, Now borders, section icon color */
--sage: #7A8C6E         /* Now pill, Now card top border */
--light-brown: #E8DDD4  /* section divider lines, instruction bg */
--sold-bg: #F0EDE8      /* (defined but card uses opacity instead) */
```

### Hero Section
```html
<div class="hero">
  <div class="hero-eyebrow">Larry &amp; Kip's Moving Sale</div>
  <h1>Moving Sale – <span>Everything Must Go!</span></h1>
  <p class="hero-sub">...</p>
  <p class="hero-updated">Last updated: Month DD, YYYY</p>  <!-- UPDATE THIS -->
  <div class="hero-badges">...</div>
</div>
```
- `<h1 span>` renders in gold
- `hero-updated` is the "Last updated" line — **always update to today's date when items change**

### Instructions Blocks (between hero and container)
- Gold-left-border block explaining how the sale works; links to tbd.html
- Sage-left-border block with contact info (kipnlar@gmail.com, Zelle/Cash)

### Sections (inside `<div class="container">`)
Current sections in order, each with icon and title:
1. 🍳 Appliances
2. 🛋️ Furniture
3. 🖼️ Accessories & Décor
4. 🔧 Miscellaneous
5. 🎄 Holiday Décor

Section HTML pattern:
```html
<div class="section">
  <div class="section-header">
    <div class="section-icon">🍳</div>
    <h2 class="section-title">Appliances</h2>
    <div class="section-line"></div>
  </div>
  <div class="items-grid">
    <!-- item cards go here -->
  </div>
</div>
```

### Item Card Anatomy
Full example with all optional elements:
```html
<div class="item-card">                          <!-- add "sold" class if sold -->
  <!-- Option A: single photo -->
  <div class="item-photo">
    <img src="photos/photo_2.jpeg" data-large-src="photos/photo_1.jpeg" alt="" style="cursor:zoom-in"/>
  </div>
  <!-- Option B: multi-photo (2-column grid) -->
  <div class="item-photo multi">
    <img src="photos/photo_17.jpeg" data-large-src="photos/photo_17.jpeg" alt="" style="cursor:zoom-in"/>
    <img src="photos/photo_18.jpeg" data-large-src="photos/photo_18.jpeg" alt="" style="cursor:zoom-in"/>
  </div>
  <!-- Option C: no photo yet -->
  <div class="item-photo-placeholder">Photo coming soon</div>

  <div class="item-body">
    <!-- Name: plain text or wrapped in <a> for external link -->
    <div class="item-name">Item Name Here</div>
    <div class="item-name"><a href="https://..." target="_blank">Item with Link</a></div>

    <!-- Optional note (italic, smaller, gray) -->
    <div class="item-note">Originally $1,199</div>

    <div class="item-footer">
      <div class="item-price">$500</div>
      <!-- OR for TBD price: -->
      <div class="item-price tbd-price">Price TBD</div>

      <span class="when-pill when-now">Now</span>
      <!-- OR: -->
      <span class="when-pill when-tbd">TBD</span>
    </div>
  </div>
</div>
```

### Sold Items
```html
<!-- Basic sold -->
<div class="item-card sold">

<!-- Sold with buyer initials shown in badge -->
<div class="item-card sold" data-sold-to="MB">
```
- Sold cards get reduced opacity (0.55), pointer-events: none, and a gray "SOLD" pill (top-right)
- `data-sold-to` appends " · {initials}" to the SOLD badge via CSS `attr()`
- Card top-border: sage (Now items), gold (TBD items) — controlled by CSS `:has()`

### Photo Conventions
- **Single-photo items**: two separate files — a smaller thumbnail (`src`) and a larger full-size (`data-large-src`). Extracted photos use sequential numbering where odd = full-size, even = thumbnail (e.g., photo_1 = large, photo_2 = thumb). This is just how they ended up — new photos can use any filename.
- **Multi-photo items**: same file used for both `src` and `data-large-src` (one file per angle, no separate thumbnail)
- Named photos (from knowledge/photos/): `steamcleaner.jpg`, `PlasticGlasses1.jpeg`, `PlasticGlasses2.jpeg`, `IMG_1171.jpeg`, etc. — these are used directly by descriptive name
- Auto-extracted photos: `photo_1.jpeg` through `photo_89.jpeg`
- New photos added manually: use descriptive names (e.g., `PatioRug1.jpeg`)

### Lightbox
- Clicking any `.item-photo img[data-large-src]` opens a full-screen overlay
- Opens `data-large-src` value as the full-size image
- Closes via: Escape key, clicking overlay, clicking image, or ✕ button
- JavaScript is inline at the bottom of `<body>`, no changes needed when adding items

### Contact Footer
```html
<div class="contact-strip">
  <h2>Interested in Something?</h2>
  <p>...</p>
  <p>📧 <a href="mailto:kipnlar@gmail.com">kipnlar@gmail.com</a></p>
  <p>Payment via Zelle or Cash · Buyer pickup at our home</p>
</div>
```

## Key Conventions
- Prices: `$75`, `$1,400` (dollar sign, commas for thousands)
- "Now" items: `when-now` pill (sage green)
- "TBD" items: `when-tbd` pill (brown), `tbd-price` class on price div if price unknown
- Multi-photo: `class="item-photo multi"` — 2-column grid, imgs 140px tall
- Single-photo: `class="item-photo"` — full width, imgs 200px tall

## Workflow for Adding New Items
1. Add photo files to `photos/` at the repo root
2. In the appropriate section in `index.html` (or `tbd.html`), add an item card following the anatomy above
3. Reference photos as `src="photos/filename.jpeg"` and `data-large-src="photos/filename.jpeg"`
4. Update the "Last updated" date in the hero section to today's date

## Important: Last Updated Date
Always update this line in the hero section when any item is added, removed, or changed:
```
Last updated: Month DD, YYYY
```

## Git
- Always commit to the main branch
