You are the master orchestrator for implementing the idiom Shopify theme redesign.
Your job is NOT to implement sections yourself. Your job is to spawn parallel sub-agents
using `claude -p` and coordinate their work, then validate results.

## Project context
- Theme directory: `/Users/dhruvparekh/Desktop/RMS/rms`
- Shopify CLI available: `shopify` command
- Claude CLI available: `claude` command (use `claude -p "<prompt>"` for headless sub-agents)
- Playwright available at: `/Users/dhruvparekh/Desktop/BSC`
- All plans are in `phaseplans/<folder>/prompt.md` — each has a `status.md` to track state

---

## Phase execution strategy

### Phase A — Run first (foundation, everything depends on it)
Run this single sub-agent and wait for it to complete before starting Phase B:

```bash
claude -p "$(cat <<'EOF'
Read the implementation plan at /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/00-shared-css/prompt.md
and implement it exactly. Working directory is /Users/dhruvparekh/Desktop/RMS/rms.
When done, write "status: done" to /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/00-shared-css/status.md
EOF
)" --allowedTools "Read,Edit,Write,Bash"
```

---

### Phase B — Run all homepage sections in parallel (after Phase A is done)
Spawn these 5 sub-agents simultaneously using background jobs:

```bash
# Agent 1 — Hero
claude -p "$(cat /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/01-homepage-hero/prompt.md)

Working directory: /Users/dhruvparekh/Desktop/RMS/rms
When done update /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/01-homepage-hero/status.md to: status: done
If blocked, write: status: blocked — <reason>" \
  --allowedTools "Read,Edit,Write,Bash" &

# Agent 2 — Brand story
claude -p "$(cat /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/02-homepage-brand-story/prompt.md)

Working directory: /Users/dhruvparekh/Desktop/RMS/rms
When done update /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/02-homepage-brand-story/status.md to: status: done
If blocked, write: status: blocked — <reason>" \
  --allowedTools "Read,Edit,Write,Bash" &

# Agent 3 — Product cards
claude -p "$(cat /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/03-homepage-product-cards/prompt.md)

Working directory: /Users/dhruvparekh/Desktop/RMS/rms
When done update /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/03-homepage-product-cards/status.md to: status: done
If blocked, write: status: blocked — <reason>" \
  --allowedTools "Read,Edit,Write,Bash" &

# Agent 4 — Dual promo
claude -p "$(cat /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/04-homepage-dual-promo/prompt.md)

Working directory: /Users/dhruvparekh/Desktop/RMS/rms
When done update /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/04-homepage-dual-promo/status.md to: status: done
If blocked, write: status: blocked — <reason>" \
  --allowedTools "Read,Edit,Write,Bash" &

# Agent 5 — Footer
claude -p "$(cat /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/05-homepage-footer/prompt.md)

Working directory: /Users/dhruvparekh/Desktop/RMS/rms
When done update /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/05-homepage-footer/status.md to: status: done
If blocked, write: status: blocked — <reason>" \
  --allowedTools "Read,Edit,Write,Bash" &

wait  # wait for all 5 to finish
```

---

### Phase C — Collection page (after Phase B agent 3 done — depends on card snippet)

```bash
claude -p "$(cat /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/06-collection-page/prompt.md)

Working directory: /Users/dhruvparekh/Desktop/RMS/rms
When done update /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/06-collection-page/status.md to: status: done
If blocked, write: status: blocked — <reason>" \
  --allowedTools "Read,Edit,Write,Bash"
```

---

### Phase D — Product page sections in parallel (independent of each other)

```bash
# Agent 7 — Product hero
claude -p "$(cat /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/07-product-page-hero/prompt.md)

Working directory: /Users/dhruvparekh/Desktop/RMS/rms
When done update /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/07-product-page-hero/status.md to: status: done
If blocked, write: status: blocked — <reason>" \
  --allowedTools "Read,Edit,Write,Bash" &

# Agent 8 — Layering row
claude -p "$(cat /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/08-product-page-layering/prompt.md)

Working directory: /Users/dhruvparekh/Desktop/RMS/rms
When done update /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/08-product-page-layering/status.md to: status: done
If blocked, write: status: blocked — <reason>" \
  --allowedTools "Read,Edit,Write,Bash" &

# Agent 9 — Video grid
claude -p "$(cat /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/09-product-page-video-grid/prompt.md)

Working directory: /Users/dhruvparekh/Desktop/RMS/rms
When done update /Users/dhruvparekh/Desktop/RMS/rms/phaseplans/09-product-page-video-grid/status.md to: status: done
If blocked, write: status: blocked — <reason>" \
  --allowedTools "Read,Edit,Write,Bash" &

wait  # wait for all 3
```

---

## Mobile design rules — enforce across ALL sub-agents
Each prompt.md already has section-specific mobile rules. Additionally enforce these globally:

**Breakpoints:** desktop > 768px | tablet 481–768px | mobile ≤ 480px
**Typography:** body 14px · small/meta 12px · section headings 24px · hero headings 32px · line-height 1.4
**Spacing:** section padding `40px 16px` mobile vs `60px 48px` desktop
**Touch targets:** all buttons min-height 44px · CTA buttons full-width on mobile
**Images:** hero height `56vw` min on mobile · `object-fit: cover`
**Grids:** all multi-column → single column on mobile unless plan says otherwise
**Cards:** height 280px on mobile · bottle overflow reduce to 10px

Section-specific mobile overrides:
- `01-homepage-hero`: marquee 13px · hero heading 32px · subtext 13px
- `02-homepage-brand-story`: hide left collage · text block full width centered
- `03-homepage-product-cards`: 1 column · card height 300px
- `04-homepage-dual-promo`: stack panels vertically · each 50vw height
- `05-homepage-footer`: stack 3 columns vertically · logotype 64px
- `06-collection-page`: 2 columns on mobile
- `07-product-page-hero`: stack image top (60vw) + info below · hide "grab 10% off" badge
- `08-product-page-layering`: stack vertically · product row horizontal scroll 200px cards
- `09-product-page-video-grid`: video cards horizontal scroll · 160px fixed width each

---

## Playwright visual verification — run AFTER all phases complete

Start the Shopify dev server:
```bash
cd /Users/dhruvparekh/Desktop/RMS/rms
shopify theme dev --store <your-store>.myshopify.com &
# wait ~10s for it to boot, preview runs at http://127.0.0.1:9292
```

Take desktop + mobile screenshots for each page:
```bash
cd /Users/dhruvparekh/Desktop/BSC
mkdir -p screenshots/idiom

# Homepage
npx playwright screenshot --browser chromium "http://127.0.0.1:9292" screenshots/idiom/homepage-desktop.png
npx playwright screenshot --browser chromium --viewport-size "390,844" "http://127.0.0.1:9292" screenshots/idiom/homepage-mobile.png

# Collection page
npx playwright screenshot --browser chromium "http://127.0.0.1:9292/collections/all" screenshots/idiom/collection-desktop.png
npx playwright screenshot --browser chromium --viewport-size "390,844" "http://127.0.0.1:9292/collections/all" screenshots/idiom/collection-mobile.png

# Product page — replace <product-handle> with a real handle from the store
npx playwright screenshot --browser chromium "http://127.0.0.1:9292/products/<product-handle>" screenshots/idiom/product-desktop.png
npx playwright screenshot --browser chromium --viewport-size "390,844" "http://127.0.0.1:9292/products/<product-handle>" screenshots/idiom/product-mobile.png
```

Read each screenshot and verify:
- No broken layout or clipped text
- No horizontal overflow on mobile
- Touch targets look large enough
- Images load or show graceful fallback
- Sections appear in the correct order

If anything looks broken: identify the section file, fix it, re-screenshot, then continue.

---

## Final output
When all phases are done and screenshots verified, read each `phaseplans/<folder>/status.md`
and print this summary table:

| Section | Status | Blocker |
|---------|--------|---------|
| 00-shared-css | | |
| 01-homepage-hero | | |
| 02-homepage-brand-story | | |
| 03-homepage-product-cards | | |
| 04-homepage-dual-promo | | |
| 05-homepage-footer | | |
| 06-collection-page | | |
| 07-product-page-hero | | |
| 08-product-page-layering | | |
| 09-product-page-video-grid | | |
