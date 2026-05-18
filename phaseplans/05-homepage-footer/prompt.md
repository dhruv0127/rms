# Homepage — Footer

**Design ref:** `idiom website update/6.png`  
**File to edit:** `sections/footer.liquid`  
**Depends on:** `00-shared-css`

---

## What this section looks like

Dark olive/army green footer. Three text columns on the left/center. A large decorative collage image (flamingo, girl with lamb, foliage — one baked asset from the graphic designer) positioned on the right side, bleeding toward the edges. Across the bottom of the footer, a very large "idiom®" logotype text spans almost the full width.

---

## Task

Update `sections/footer.liquid` to match the design. Do not remove existing schema settings — update the rendered HTML/CSS structure only, and add any new settings needed.

### Background & overall
- Background: `var(--idiom-olive-dark)` (`#3d3d1a` approx)
- `position: relative`, `overflow: hidden` (so large logotype can be clipped cleanly)
- `padding: 60px 48px 0`

### Three text columns (upper area)
Use a 3-column flex or grid layout:

**Column 1 — "smell like no one else"**
- Heading: `"smell like no one else"` — white, bold, ~18px
- Body: brand tagline paragraph — white, ~13px, muted opacity
- Two pagination dots below (decorative only — `<span>` circles)

**Column 2 — "the boring stuff"**
- Heading: `"the boring stuff"` — white, bold, ~16px
- Links (white, ~13px, hover underline): delivery · returns · accounts · faqs · contact · terms & conditions · privacy policy
- Source these from the existing footer menu if it exists in the schema, otherwise hardcode

**Column 3 — "shop by type"**
- Heading: `"shop by type"` — white, bold, ~16px
- Links: full size · mini-oms · kits and gifts

### Decorative collage image (right side)
- Source from schema setting `collage_image` (image_picker)
- `position: absolute`, `right: 0`, `top: 0`, `height: 100%`, `width: ~45%`
- `object-fit: cover`, `object-position: left center`
- `z-index: 0` — behind the text columns (`z-index: 1`)
- Graphic designer supplies this as a single flat asset — do not attempt to layer elements

### Large logotype (bottom)
- Text: `"idiom®"` — white, very large (~120–140px), bold or heavy weight
- `position: relative`, `z-index: 2`, centered or left-aligned spanning full width
- `margin-top: 40px`, `line-height: 0.85` so it sits tight to the bottom
- Bottom of the text should align with or slightly overflow the footer bottom edge (`overflow: hidden` on footer clips cleanly)

### Schema settings to add
```json
{ "type": "image_picker", "id": "collage_image", "label": "Right decorative collage" },
{ "type": "text", "id": "tagline", "label": "Tagline paragraph" }
```
