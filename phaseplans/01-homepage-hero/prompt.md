# Homepage — Hero Collage Banner

**Design ref:** `idiom website update/2.png`  
**File to edit:** `sections/section-banner-image.liquid`  
**Depends on:** `00-shared-css` (idiom-theme.css must exist first)

---

## What this section looks like

Full-width hero with a pre-baked collage image as the background (multiple photos of flamingos, discovery kit, girl with lamb etc — graphic designer supplies this as one flat PNG/JPG). Over the image sits a text overlay + CTA button at the bottom-left. Directly below the image is a scrolling olive marquee ticker strip.

---

## Task

Update `sections/section-banner-image.liquid` to match the design.

### Hero image area
- Full-width, min-height `70vh`
- Background image from Shopify section schema setting `hero_image` (image_picker)
- `object-fit: cover`, centered

### Text overlay (position: bottom-left of image, ~40px from edges)
- Heading: bold, white, ~48px — schema setting `heading` (default: `"127 unique fragrances. 1 kit."`)
- Subtext: white, ~14px — schema setting `subtext` (default: `"discover your Flanker fragrance combinations with our 7-piece discovery kit."`)
- CTA button: uses `.idiom-btn--outline` class — schema settings `cta_label` (default: `"shop now | £17"`) and `cta_url`

### Marquee ticker strip (directly below the hero, NOT inside the image)
- Olive green background (`var(--idiom-olive)`)
- White text, repeating: `"smell like no one else™"` · `"find your fragrance freedom"` · `"layer, or wear solo"`
- Use `.idiom-marquee-track` from shared CSS for the infinite scroll animation
- Schema setting `marquee_text` (textarea) — each line becomes one ticker item

### Schema settings to add
```json
{ "type": "image_picker", "id": "hero_image", "label": "Hero image" },
{ "type": "text", "id": "heading", "label": "Heading", "default": "127 unique fragrances. 1 kit." },
{ "type": "text", "id": "subtext", "label": "Subtext" },
{ "type": "text", "id": "cta_label", "label": "CTA label", "default": "shop now | £17" },
{ "type": "url", "id": "cta_url", "label": "CTA link" },
{ "type": "textarea", "id": "marquee_text", "label": "Marquee items (one per line)" }
```

Do not remove or break any existing schema settings already in the file — append new ones only.
