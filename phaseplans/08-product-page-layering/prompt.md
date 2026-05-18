# Product Page — "Wear Solo or Layer Me With" Row

**Design ref:** `idiom website update/11.png`  
**File to create:** `sections/idiom-layering-row.liquid`  
**Depends on:** `00-shared-css`, `03-homepage-product-cards` (card snippet)

---

## What this section looks like

Full-width olive green band. Left side has white text with a large two-line heading ("wear solo, / or layer me with:") and a small italic note. Right side is a horizontally scrollable row of product cards (same card style as the product grid — bottle + name + price). The section sits directly below the product hero on the product page.

---

## Task

Create `sections/idiom-layering-row.liquid`.

### Layout
- Full-width, `background: var(--idiom-olive)` (army green)
- `display: flex`, `align-items: center`, `min-height: 320px`
- `padding: 40px 48px`

### Left text block (~30% width, flex-shrink: 0)
- Line 1: `"wear solo,"` — white, bold, large (~40px), `line-height: 1`
- Line 2: `"or layer me with:"` — white, bold, large (~40px), `line-height: 1`
- Subtext: `"we don't do signature scents..."` — white, italic, ~14px, `margin-top: 12px`
- Fine print: `"* that's your part."` — white, italic, very small (~11px), `margin-top: 4px`

All four lines are schema settings (`heading_solo`, `heading_layer`, `subtext`, `fine_print`).

### Right product row (~70% width)
- `overflow-x: auto`, `scrollbar-width: none` (hide scrollbar)
- `-webkit-overflow-scrolling: touch`
- Flex row, `gap: 16px`, `padding-bottom: 4px` (prevents clipping of card overflow)

**Product source — in priority order:**
1. Product metafield `custom.layer_with_products` (list of product references) — if set, use these specific products
2. Fallback: `section.settings.layering_collection` (collection picker) — show first 6 products from that collection
3. Fallback: same collection as current product

**Each card — use `{% render 'idiom-product-card', product: product %}`** (shared snippet from phase 03/06):
- Fixed width: `~200px`, flex-shrink: 0
- Same card structure: background image, bottle, personality tag, name, price

### Schema settings
```json
{ "type": "text", "id": "heading_solo", "label": "Line 1", "default": "wear solo," },
{ "type": "text", "id": "heading_layer", "label": "Line 2", "default": "or layer me with:" },
{ "type": "text", "id": "subtext", "label": "Subtext", "default": "we don't do signature scents..." },
{ "type": "text", "id": "fine_print", "label": "Fine print", "default": "* that's your part." },
{ "type": "collection", "id": "layering_collection", "label": "Fallback collection" }
```

### Responsive
- On mobile (≤768px): stack vertically. Text block full width on top, product row scrolls horizontally below.
- Card width stays `200px` so scrolling behaviour is preserved on mobile.
