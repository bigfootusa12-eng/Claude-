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
- **Status:** BUILT, PAUSED, awaiting launch. Ad set `Clean Creative Test - Sep 2026`
  (120249855515660497), three ads: `A1 - Long Shifts`, `B1 - How Its Built`,
  `C1 - Size Confidence`. Full variant bank in `creative_bank.md`.
- **Hypothesis:** the old creative bought its 3.2% CTR with a fabricated 5-star testimonial
  and a "40% OFF" badge that does not exist. Truthful creative will click through worse.
  That is the point — the traffic it does send should convert instead of bouncing at 99%.
- **Why it is still paused:** the funnel loses 99% of clicks before add-to-cart. Relaunching
  ahead of EXP-001/EXP-002 repeats the $194 loss with better-behaved ads.
- **Judge on:** ATC rate per session first, then blended ROAS. Break-even is now **1.29**
  and break-even CPA **$38.74** at the confirmed $9.50 COGS. Give it $60 spend before ruling.

---

## Open conflicts needing an owner decision

### CONFLICT-001 — the free-gifts offer — RESOLVED 2026-09-14
- Owner first said there was no such offer, then confirmed: keep it and advertise it.
- The offer is real and live: Kaching tier **"2 X Back Support + Bundle"** on
  `/products/lower-back-support`. All three rebuilt ads now carry it.
- **Only the Back Stretcher is named in the copy.** The tier's third gift points at
  `gid://shopify/Product/9566443471016` = "Bracken Mini Pulse Massager", which is **DRAFT
  and unpublished** — it cannot be delivered, so advertising it would be a false promise.
  Publish it or drop it from the tier, then the copy can name it.
- **Two open ops risks:** the Back Stretcher has **6 units** in stock (six bundles), and gift
  COGS is unknown, so bundle contribution margin cannot be calculated yet.

### CONFLICT-003 — fabricated testimonial creative — DECLINED 2026-09-14
- Owner asked to keep Ad 5 / Ad 5b running because they draw attention.
- Not done. Asset `92d5b7bf…` shows an invented customer ("David R.", five stars) inside a
  **Facebook-branded review card**, over a **"40% OFF"** badge on a product with no
  compare-at price. §6 of CLAUDE.md bans fabricated testimonials outright.
- The attention was not worth anything: those two ads took **$124.87** of the $194.10 spent
  and returned **0 purchases**. The funnel does not fail for lack of clicks.
- Ads are paused, not deleted. Replacement path: re-export the clean Ad 6 photography with a
  compliant headline, and collect real reviews from the six existing customers (EXP-001).

### CONFLICT-002 — keyword-stuffed image alt text on the live product page
- The supplier image alt text reads "…Spine Decompression Waist Trainer Brace **Back Pain
  Relief**". That is a health claim sitting on the landing page ads point at.
- Not changed: theme/product media writes to the live theme are blocked for this session.

---

## External input — ChatGPT website suggestions
None received yet.
