# Collection Page — Product Grid

**Design ref:** `idiom website update/8.png`  
**File to edit:** `sections/collection.liquid`  
**Depends on:** `00-shared-css`, `03-homepage-product-cards` (shared card styles in `idiom-theme.css`)

---

## What this section looks like

Clean full-width collection page. Simple page heading "shop everything" + subtext centered at the top. Below that, the same product card style as the homepage grid — rounded cards with lifestyle background images, bottle overflowing the card bottom, personality tag badge top-left. No sidebar.

---

## Task

Update `sections/collection.liquid` to match the design.

### Page heading block
At the top of the section (above the product grid), render:
- `collection.title` — bold, centered, ~40px, dark (`var(--idiom-black)`)
- `section.settings.subtext` — lighter, centered, ~14px, muted
- `padding-bottom: 32px`

### Product grid
- Remove any existing sidebar or filter panel — layout should be full width, no sidebar
- CSS Grid: 3 columns desktop, 2 columns tablet (≤768px), 1 column mobile (≤480px)
- `gap: 20px`, `padding: 0 24px 60px`
- Use `collection.products` with Shopify pagination (keep any existing `paginate` tag)

### Each product card — reuse `.idiom-product-card` and `.idiom-tag` from `idiom-theme.css`

**Card background image:**
- Source from `product.metafields.custom.card_background_image`
- Fallback: `product.featured_image` (zoomed/blurred via CSS filter if needed as fallback)
- `position: absolute`, `inset: 0`, `object-fit: cover`, `border-radius: 16px`

**Bottle image:**
- `product.featured_image`
- `position: absolute`, `bottom: -20px`, `left: 50%`, `transform: translateX(-50%)`
- `height: 75%`, `object-fit: contain`, `z-index: 2`

**Personality tag — `.idiom-tag`:**
- `product.metafields.custom.personality_tag` — only render if present

**Below card:**
- `product.title` — bold, ~16px
- `product.metafields.custom.scent_descriptor` — uppercase, spaced, ~12px
- `product.price | money` — inline

**Card link:** wrap in `<a href="{{ product.url }}">`

### Schema settings
```json
{ "type": "text", "id": "subtext", "label": "Subtext below collection title", "default": "get to know our crowd-pleasers..." },
{ "type": "range", "id": "products_per_page", "label": "Products per page", "min": 6, "max": 24, "step": 3, "default": 12 }
```
Keep all existing schema settings — only add these new ones.

### Note
The card HTML/CSS structure here must be identical to `sections/idiom-product-cards.liquid` so both pages look consistent. If the card markup is long, consider extracting it to `snippets/idiom-product-card.liquid` and rendering it with `{% render 'idiom-product-card', product: product %}` in both files.
