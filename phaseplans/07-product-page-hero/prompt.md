# Product Page — Hero (Split Layout)

**Design ref:** `idiom website update/10.png`  
**File to edit:** `sections/product.liquid`  
**Depends on:** `00-shared-css`

---

## What this section looks like

Two-column split layout, full viewport height on desktop. Left half: a full-bleed lifestyle collage image (pre-baked single asset from graphic designer, e.g. girl + lamb + mountain scene). A rotated pill badge "grab 10% off" is pinned to the far left edge. Right half: cream background with all product info — title, scent descriptor, star rating, description, size selector, add to bag button, first impressions thumbnails, and accordion rows.

---

## Task

Update the main product hero layout in `sections/product.liquid`.

### Overall layout
- Two columns, `50vw` each, `min-height: 100vh` on desktop
- `display: flex`, `align-items: stretch`

### Left column — collage image
- Source from product metafield `custom.hero_collage_image` (file_reference, image type)
- Fallback: `product.featured_image`
- `object-fit: cover`, `width: 100%`, `height: 100%`
- `position: relative`, `overflow: hidden`

**"grab 10% off" badge:**
- `position: absolute`, `left: -36px`, `top: 50%`, `transform: translateY(-50%) rotate(-90deg)`
- Background: `var(--idiom-olive)`, white text, pill shape (`border-radius: 999px`)
- `padding: 6px 16px`, `font-size: 12px`, `white-space: nowrap`
- This is a popup/discount trigger — wrap in `<button>` or `<a>` linking to discount section

### Right column — product info
Background: `var(--idiom-cream)`, `padding: 48px 40px`

Render in this order:
1. `product.title` — bold, ~36px, all-caps or as-is per brand style
2. `product.metafields.custom.scent_descriptor` — uppercase, letter-spaced, ~13px, muted
3. Star rating row — render from `product.metafields.reviews.rating` if available, or use static stars as placeholder. Show `"35 reviews"` link beside stars.
4. Description paragraph — `product.description` (first paragraph only, truncated; full description moves to accordion)
5. `product.metafields.custom.wear_solo_note` — label `"Wear Solo:"` bold, value in normal weight, ~13px
6. `product.metafields.custom.layer_note` — label `"Layer:"` bold, value normal weight, ~13px
7. **Size variant selector** — pill toggle buttons (not a dropdown):
   - Loop `product.variants`, render each as `<button>` with class `idiom-size-btn`
   - Selected state: dark bg + white text. Unselected: outline style.
   - On click: update selected variant via JS (keep existing variant selection JS if present)
8. **Add to bag button** — full width, `.idiom-btn`, dark olive, white text
   - Label: `"add to bag | {{ selected_variant.price | money }}"` 
9. **"FIRST IMPRESSIONS:" row** — label + 4 circular thumbnail images
   - Source from product metafield `custom.first_impression_images` (list of file_reference)
   - Render as `<img>` circles, `width: 48px`, `height: 48px`, `border-radius: 50%`, `object-fit: cover`
   - If metafield is empty, hide this row entirely
10. **Accordions** — three expandable rows using existing `snippets/accordions.liquid` if it exists:
    - "full description" — content: `product.description`
    - "key notes" — content: `product.metafields.custom.key_notes`
    - "how to wear" — content: `product.metafields.custom.how_to_wear`

### Metafields required
- `custom.hero_collage_image` — file_reference (image)
- `custom.scent_descriptor` — single_line_text
- `custom.wear_solo_note` — single_line_text
- `custom.layer_note` — single_line_text
- `custom.first_impression_images` — list.file_reference
- `custom.key_notes` — multi_line_text
- `custom.how_to_wear` — multi_line_text

### Responsive
- On mobile (≤768px): stack to single column. Left image becomes full-width, `height: 60vw`. Right column full width below.
- Hide "grab 10% off" badge on mobile or reposition to top of left image.
