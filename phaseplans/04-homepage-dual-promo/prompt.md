# Homepage — Dual Promo Banners

**Design ref:** `idiom website update/5.png`  
**File to create:** `sections/idiom-dual-promo.liquid`  
**Depends on:** `00-shared-css`

---

## What this section looks like

Two side-by-side full-bleed panels, each roughly half the viewport width. Left panel has a peach/fruit background with a dark perfume bottle and headline "the perfect saffron". Right panel has a green apple background with a light perfume bottle and headline "citrusy + fresh af". Both panels have a text overlay at the bottom-left and a "shop now | £17" CTA.

The background images are pre-baked single assets from the graphic designer — do NOT attempt to composite fruit + bottle in CSS. The bottle is part of the baked image.

---

## Task

Create `sections/idiom-dual-promo.liquid`.

### Layout
- Flexbox row, two equal panels (`flex: 1 1 50%`)
- Full viewport width, height `50vh` minimum
- No gap between panels

### Each panel
- Background image: `object-fit: cover`, `width: 100%`, `height: 100%` — rendered as `<img>` or CSS background
- Semi-transparent dark overlay: `::after` pseudo-element, `rgba(0,0,0,0.2)`, covers full panel
- Text block: `position: absolute`, `bottom: 28px`, `left: 28px`, `z-index: 2`
  - Heading: white, bold, ~32px — schema setting per panel
  - Subtext: white, ~13px — schema setting per panel
  - CTA: white text, small, underline on hover — schema setting per panel (label + url)

### Schema — use blocks (one block = one panel, max 2 blocks)
```json
"blocks": [
  {
    "type": "panel",
    "name": "Promo panel",
    "settings": [
      { "type": "image_picker", "id": "bg_image", "label": "Background image" },
      { "type": "text", "id": "heading", "label": "Heading" },
      { "type": "text", "id": "subtext", "label": "Subtext" },
      { "type": "text", "id": "cta_label", "label": "CTA label", "default": "shop now | £17" },
      { "type": "url", "id": "cta_url", "label": "CTA link" }
    ]
  }
],
"max_blocks": 2
```

### Responsive
- On mobile (≤600px): stack panels vertically, each `height: 50vw` minimum
