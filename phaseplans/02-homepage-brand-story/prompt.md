# Homepage — Brand Story Section

**Design ref:** `idiom website update/3.png`  
**File to create:** `sections/idiom-brand-story.liquid`  
**Depends on:** `00-shared-css`

---

## What this section looks like

Cream background section. Left side has a decorative collage (moon, smoke/mist, butterfly) — this is ONE pre-baked image asset from the graphic designer, positioned absolutely on the left edge. Right/center has a text block with heading, body copy, and a "learn more" CTA. At the very bottom of this section, the transition heading for the product grid appears.

---

## Task

Create `sections/idiom-brand-story.liquid` from scratch.

### Layout
- Full-width, cream background (`var(--idiom-cream)`)
- Two visual zones:
  1. **Left decorative image** — `position: absolute`, left edge, vertically centered, `width: ~40%`, `object-fit: contain`. This is schema setting `collage_image` (image_picker). Do NOT attempt to layer multiple images — the designer provides this as a single flat asset.
  2. **Text block** — centered on page (with enough left padding to clear the collage on desktop), max-width ~520px

### Text block content
- Heading: `"sick of smelling like everyone else?"` — bold, ~36px, dark
- Subline: `"yeah, us too."` — italic, smaller, below the heading
- Body copy paragraph — schema setting `body` (richtext or textarea)  
  Default text: *"idiom was born by 3 good friends who shared a passion for fragrance with the belief that individuality is everything and fragrance could be done better, high-quality, long lasting capsule eau du parfums ready to layer and always priced to be affordable."*
- CTA button: `.idiom-btn` — schema settings `cta_label` (default: `"learn more"`) and `cta_url`

### Grid transition (bottom of section)
Below the text block, separated by generous whitespace:
- Sub-heading: `"holy s#*%, what are you wearing?"` — bold, centered, ~32px
- Subtext: `"get to know our crowd-pleasers..."` — lighter weight, centered, ~14px

These bottom headings are also schema settings (`grid_heading`, `grid_subtext`) so they can be edited from the Shopify customizer.

### Schema settings
```json
{ "type": "image_picker", "id": "collage_image", "label": "Left decorative collage image" },
{ "type": "text", "id": "heading", "label": "Heading", "default": "sick of smelling like everyone else?" },
{ "type": "text", "id": "subline", "label": "Subline", "default": "yeah, us too." },
{ "type": "textarea", "id": "body", "label": "Body copy" },
{ "type": "text", "id": "cta_label", "label": "CTA label", "default": "learn more" },
{ "type": "url", "id": "cta_url", "label": "CTA link" },
{ "type": "text", "id": "grid_heading", "label": "Grid transition heading", "default": "holy s#*%, what are you wearing?" },
{ "type": "text", "id": "grid_subtext", "label": "Grid transition subtext", "default": "get to know our crowd-pleasers..." }
```

### Responsive
- On mobile: hide the left collage image (or stack it above the text block at full width, `position: static`)
- Text block becomes full width, centered padding
