# Homepage — Product Cards Grid ("holy s#*%, what are you wearing?")

**Design ref:** `idiom website update/4.png`  
**File to create:** `sections/idiom-product-cards.liquid`  
**Depends on:** `00-shared-css` (`.idiom-product-card`, `.idiom-tag` classes)

---

## What this section looks like

3-column product card grid on a cream background. Each card is a rounded rectangle with:
- A lifestyle/scene photo as the card background (roses, vintage car road, tall grass etc.)
- The product bottle image centred in the foreground, slightly overflowing the card bottom edge
- A small rotated pill badge top-left with a personality descriptor ("floral, but not sweet")
- Product name, scent descriptor, and price printed below the card

---

## Task

Create `sections/idiom-product-cards.liquid`.

### Section heading (optional — skip if brand story section already renders them)
If this section is placed standalone (without brand story above it), render:
- `section.settings.heading` — bold, centered, ~32px
- `section.settings.subtext` — lighter, centered, ~14px
Wrap in a conditional so they only show if the settings are non-empty.

### Grid
- CSS Grid: 3 columns desktop, 2 columns tablet (≤768px), 1 column mobile (≤480px)
- Gap: `20px`
- `padding: 40px 24px`

### Each product card — uses `.idiom-product-card`
Render using Shopify's `section.settings.collection` object, limit by `section.settings.max_products`.

**Card background image:**
- Source from product metafield `custom.card_background_image` (image type)
- Render as `<img>` with `object-fit: cover` inside the card, `position: absolute`, fills card box
- Card box: `position: relative`, `border-radius: 16px`, `overflow: hidden` for the bg, `overflow: visible` on the outer wrapper so the bottle can bleed out

**Bottle image:**
- Source from the product's featured image (`product.featured_image`)
- `position: absolute`, `bottom: -20px`, `left: 50%`, `transform: translateX(-50%)`
- `z-index: 2`, `height: 75%`, `object-fit: contain`

**Personality tag badge — uses `.idiom-tag`:**
- Source from product metafield `custom.personality_tag` (single_line_text)
- Only render if metafield is non-empty

**Below card:**
- Product title — bold, ~16px
- `product.metafields.custom.scent_descriptor` — uppercase, letter-spaced, ~12px, muted
- Price — `product.price | money`, inline with a `|` separator

**Card link:** entire card + below-card area wrapped in `<a href="{{ product.url }}">` 

### Schema settings
```json
{ "type": "collection", "id": "collection", "label": "Product collection" },
{ "type": "range", "id": "max_products", "label": "Max products", "min": 3, "max": 12, "step": 3, "default": 3 },
{ "type": "text", "id": "heading", "label": "Section heading" },
{ "type": "text", "id": "subtext", "label": "Section subtext" }
```

### Metafields required (register in Shopify admin before this section will display correctly)
- `custom.card_background_image` — type: file_reference (image)
- `custom.personality_tag` — type: single_line_text
- `custom.scent_descriptor` — type: single_line_text

### Responsive
- On mobile: single column, card height fixed `320px`, bottle image scales down proportionally
