# Product Page — Scent Descriptor + Video Grid

**Design ref:** `idiom website update/12.png`  
**File to create:** `sections/idiom-video-grid.liquid`  
**Depends on:** `00-shared-css`

---

## What this section looks like

Full-width section with a lifestyle background image (e.g. mountain + girl with lamb scene). Dark overlay makes it legible. Centered italic descriptive text at the top ("cool. meditative. lingering aromatic wood. / subtle gourmand notes on warm skin. quietly radiant."). Below the text, a horizontal row of 5 semi-transparent video thumbnail cards spanning the full width.

---

## Task

Create `sections/idiom-video-grid.liquid`.

### Background
- Schema setting `bg_image` (image_picker) — product-specific background, sourced from `product.metafields.custom.video_section_bg` if on the product page, otherwise the section setting
- `position: relative`, `width: 100%`, `min-height: 480px`
- Background image: `object-fit: cover`, `position: absolute`, `inset: 0`, `z-index: 0`
- Dark overlay: `::before` pseudo-element, `background: rgba(0,0,0,0.38)`, `position: absolute`, `inset: 0`, `z-index: 1`

### Content wrapper
- `position: relative`, `z-index: 2`
- `padding: 48px 32px`
- `display: flex`, `flex-direction: column`, `align-items: center`, `gap: 36px`

### Scent descriptor text
- Two lines of italic white text, centered
- `font-size: ~22px`, `font-style: italic`, `line-height: 1.3`, `text-align: center`, `max-width: 800px`
- Schema settings: `descriptor_line1` (text), `descriptor_line2` (text)
- Defaults: `"cool. meditative. lingering aromatic wood."` and `"subtle gourmand notes on warm skin. quietly radiant."`

### Video card row
- `display: flex`, `gap: 12px`, `width: 100%`
- 5 cards, each `flex: 1 1 0`, equal width

**Each video card:**
- `background: rgba(255,255,255,0.82)`, `border-radius: 12px`
- `aspect-ratio: 9/16` (portrait orientation as in the design)
- `overflow: hidden`, `position: relative`
- Contains a `<video>` or `<iframe>` element filling the card
  - Use `poster` attribute on `<video>` for thumbnail display
  - If the URL is a Vimeo link, render an `<iframe>`; if it's a Shopify-hosted video, render `<video autoplay muted loop playsinline>`
- Placeholder label `"video [n]"` centered in the card — only shown when no video URL is set, for design preview purposes

**Each card is a repeatable block in the schema:**
```json
"blocks": [
  {
    "type": "video",
    "name": "Video",
    "settings": [
      { "type": "video", "id": "shopify_video", "label": "Shopify-hosted video" },
      { "type": "text", "id": "external_url", "label": "External video URL (Vimeo etc.)" },
      { "type": "image_picker", "id": "poster_image", "label": "Poster / thumbnail image" }
    ]
  }
],
"max_blocks": 5
```

### Section-level schema settings
```json
{ "type": "image_picker", "id": "bg_image", "label": "Background image" },
{ "type": "text", "id": "descriptor_line1", "label": "Descriptor line 1" },
{ "type": "text", "id": "descriptor_line2", "label": "Descriptor line 2" }
```

### Responsive
- On mobile (≤768px): video card row becomes a horizontal scroll container (`overflow-x: auto`), each card fixed `width: 160px`, `flex-shrink: 0`
- Descriptor text reduces to `~16px`
