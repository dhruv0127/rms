# Shared CSS — idiom Theme Variables & Components

**Design refs:** idiom website update/2.png – 12.png  
**File to create:** `assets/idiom-theme.css`  
**File to edit:** `layout/theme.liquid`

---

## Task

Create a shared CSS file `assets/idiom-theme.css` with the brand tokens and reusable component styles that every section will depend on.

Then import it globally in `layout/theme.liquid` just before the closing `</head>` tag:
```liquid
{{ 'idiom-theme.css' | asset_url | stylesheet_tag }}
```

---

## CSS to include

### 1. Custom properties (brand tokens)
```css
:root {
  --idiom-cream: #faf6f0;
  --idiom-olive: #5a5a1e;
  --idiom-olive-dark: #3d3d1a;
  --idiom-black: #1a1a1a;
  --idiom-white: #ffffff;
}
```
> Confirm exact hex values with the brand kit — these are approximated from the design images.

### 2. Marquee / ticker strip
Infinite left-scrolling text ticker used in hero section and after nav.
```css
.idiom-marquee-track { /* wraps two copies of the content for seamless loop */ }
/* Keyframe: translateX(0) → translateX(-50%), 30s linear infinite */
```

### 3. Product card base (`.idiom-product-card`)
Used on homepage product grid AND collection page grid.
- `position: relative`, `border-radius: 16px`, `overflow: visible`
- Card background image: `object-fit: cover`, covers the card box
- Bottle image: `position: absolute`, `bottom: 0`, centered horizontally, `z-index: 2`, overflows card bottom by ~20px

### 4. Personality tag badge (`.idiom-tag`)
- `position: absolute`, `top: 12px`, `left: 12px`
- `background: var(--idiom-cream)`, `border-radius: 999px`
- `padding: 4px 12px`, `font-size: 12px`
- `transform: rotate(-3deg)` — slight tilt for handmade feel

### 5. CTA button (`.idiom-btn`)
- Base: dark olive bg, white text, `border-radius: 999px`, `padding: 10px 24px`
- Variant `.idiom-btn--outline`: transparent bg, dark olive border, dark text

### 6. Section heading pair (`.idiom-section-heading`)
- Heading: bold, ~36–40px
- Subtext: lighter weight, ~14px, muted color, `margin-top: 6px`
