# Bracken — Running Experiments

## Status: none running. Ad spend is paused pending funnel fixes.

---

## Queued (not yet started)

### EXP-001 — Add real social proof to the product page
- **Hypothesis:** With 0 reviews on a health-adjacent $49.99 wearable, trust is the binding constraint on add-to-cart. Real reviews lift ATC rate materially.
- **Status:** BLOCKED. Judge.me is installed and reporting `data-shop-review-count="0"`. We have 6 lifetime orders, 1 refunded. Reviews must be solicited from those real customers — they will not be fabricated.
- **Judge on:** ATC rate per session (baseline 1 ATC / 98 landing-page views = ~1%).

### EXP-002 — Landing-page LCP / above-the-fold
- **Hypothesis:** Page is 301 KB of HTML with 15 `loading="lazy"` images and 0 `loading="eager"`. If the hero image is lazy-loaded, mobile paid traffic sees a blank hero first — a known ATC killer.
- **Status:** BLOCKED on write access. Shopify MCP refuses theme file writes to the MAIN theme.
- **Judge on:** LCP, and ATC rate per session.

### EXP-003 — Rebuild ad creative without the false claims
- **Hypothesis:** CTR 3.2% and CPC $1.32 say the creative earns the click; the funnel loses it afterwards. Rebuild the winning concept truthfully (60-day guarantee, free tracked shipping, no star rating) and relaunch only once the page converts.
- **Status:** Queued behind EXP-001/EXP-002. Relaunching paid traffic into the current page repeats the same loss.
- **Judge on:** blended ROAS over $60 spend.

---

## External input — ChatGPT website suggestions
None received yet.
