# Bracken — Running Experiments

## Status: none running. Ad spend is paused pending funnel fixes.

---

## Queued (not yet started)

### EXP-001 — Add real social proof to the product page
- **Hypothesis:** With 0 reviews on a health-adjacent $49.99 wearable, trust is the binding constraint on add-to-cart. Real reviews lift ATC rate materially.
- **Status:** BLOCKED. Judge.me is installed and reporting `data-shop-review-count="0"`. We have 6 lifetime orders, 1 refunded. Reviews must be solicited from those real customers — they will not be fabricated.
- **Judge on:** ATC rate per session (baseline 1 ATC / 98 landing-page views = ~1%).

### EXP-002 — Landing-page LCP / above-the-fold — CLOSED, NOT A REAL ISSUE
- I claimed the hero was lazy-loaded. **That was wrong.** I had counted `loading="lazy"`
  occurrences without checking which images carried them. The hero carries no loading
  attribute and loads eagerly; only the below-fold gallery is lazy, which is correct.
- Weight is fine too — the CDN serves **318 KB of webp** to browsers that accept it. The
  5.1 MB PNG only reaches clients that don't request webp.
- No theme edit is needed. Closed.

### EXP-004 — Compliant hero image *(shipped 2026-09-14)*
- **What was wrong:** the product page's featured image was `Ad_6.png` — the retired ad
  creative whose baked-in headline reads "Back Pain Doesn't Take a Day Off." Affliction
  framing under §3, serving as both the hero and the `og:image` on every shared link.
- **Change:** reordered product media so the worn-product shot leads, cutaway second, size
  chart third, `Ad_6.png` last. Three alt texts rewritten, removing the supplier's
  "…Back Pain Relief" keyword spam.
- **Judge on:** ATC rate per session against the 1-in-98 baseline, once traffic resumes.
- **Revert:** move `MediaImage/41352348696744` back to position 0.

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

### CONFLICT-002 — keyword-stuffed image alt text — RESOLVED 2026-09-14
- Rewritten via `fileUpdate`, which is not blocked (only *theme file* writes to the live theme
  are). The "…Back Pain Relief" alt is gone; all three images now carry factual descriptions.

### CONFLICT-004 — Ad_6.png still sits in the product gallery
- Its health claim is baked into the image pixels, so demoting it to last limits exposure but
  does not remove it. Deleting a brand asset is the owner's call.
- **Options:** delete the media, or re-export the artwork with a compliant headline. The
  photography and brand lockup are genuinely good — only the copy on it is the problem.

---

## External input — ChatGPT website suggestions
None received yet.
