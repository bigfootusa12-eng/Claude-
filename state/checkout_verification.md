# Checkout Verification Run

**Do this one thing first, or the run proves nothing.**

## Shopify Payments test mode is ON

All six orders show `paymentGatewayNames: ["shopify_payments"]` with `test: true`. That is
Shopify Payments **test mode**, not a coincidence of how they were placed. Leave it on and the
seventh order is another `test: true` row: no money moves, no supplier order is triggered, and
the Meta pixel Purchase event is not something you can trust.

**Turn it off:** Shopify admin → Settings → Payments → Shopify Payments → **Manage** →
uncheck **Use test mode** → Save.

Turn it back on afterwards only if you deliberately want more test orders. Nothing else in this
checklist works while it is on.

---

## What to order

Order the **2-belt bundle**, not a single belt. That is the exact path the three new ads sell,
and it is the path with the most that can break.

- Use a **real card** and a **real deliverable address**.
- Use a **fresh email** — not `jonesstone899@gmail.com`. A new email also tests the
  new-customer flow and the confirmation email as a stranger receives it.
- Expected total: **$99.98**, free shipping, Lumbar Back Stretcher added at **$0.00**.

---

## Watch for these, in order

| # | Step | What to check | Known risk |
|---|---|---|---|
| 1 | Product page | Bundle block renders; picking "2 X Back Support + Bundle" adds the Back Stretcher at $0 | **The tier also promises a Mini Pulse Massager, which is a draft product.** Watch what it does — silently drops, errors, or blocks the add to cart |
| 2 | Size picker | Six sizes selectable; the chart is reachable without hunting | Sizing doubt is the top add-to-cart killer on wearables |
| 3 | Cart | $99.98 subtotal, stretcher at $0.00, shipping $0.00 | Bundle discounts sometimes fail to carry into cart |
| 4 | Checkout | "Free Shipping" rate appears; delivery estimate is stated and **is actually true for a dropshipped item** | Rates exist (Free $0.00, Express $4.99) but the stated delivery window has never been tested |
| 5 | Payment | Card is really charged | Only verifiable with test mode off |
| 6 | Confirmation email | Arrives; the guarantee reads **60 days**; sender and reply-to look like a real business | |
| 7 | **Meta pixel** | A **Purchase** event fires. Check Meta Events Manager → Test Events while you check out | **Zero purchases have ever been attributed.** ViewContent and AddToCart do fire, so this is the untested link |
| 8 | Order in admin | `test: false`; order lands and is assigned somewhere sane | |
| 9 | **Fulfillment** | Does a supplier order actually get placed? | See below — this is the weakest link |

---

## Fulfillment is the part most likely to fail

- The store has **one location**: `4605 Jerome Prairie Rd`, Grants Pass, OR — a home address,
  not a warehouse or a fulfillment service.
- **AutoDS is connected** (it owns a delivery profile, "AutoDS Free Shipping"), so dropship
  automation is partly wired.
- But on orders #1002–#1004 the fulfillment orders are `status: CLOSED`,
  `requestStatus: UNSUBMITTED`, assigned to that home address. **No fulfillment request was
  ever submitted to a supplier.** They were closed out without anything being ordered.

So it is unproven that a paid order reaches a supplier at all. The test order settles it.

---

## After it lands

Tell me the order number and I will verify from the Admin API: `test` flag, financial and
fulfillment status, the fulfillment-order request status, what the bundle actually wrote into
the line items, and whether Meta recorded the purchase.

Keep the order — don't refund it immediately. Let it run all the way to delivery. That gives
you:
- a true delivery time to state honestly on the page and in ads
- the packaging and product quality in hand
- **the first real customer who can leave a review** (see `review_request_playbook.md`)

If you want to test the 60-day guarantee path too, refund it only after it has arrived.
