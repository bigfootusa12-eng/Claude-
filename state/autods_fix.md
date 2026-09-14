# AutoDS — finding the cancellation reason and fixing it

## Why you have to fetch this, not me

Shopify does not store a reason. I checked every field that could hold one on order #1007:

| Checked | Result |
|---|---|
| `fulfillmentOrder.merchantRequests` (where a fulfillment service writes its rejection message) | empty |
| Order metafields | none |
| Order tags / note / custom attributes | all empty |
| Full order event log | only the generic line "AutoDS canceled the fulfillment request of 1 item." |
| Shop-level fulfillment orders | #1007's is not even listed — AutoDS owns it, and this token cannot read another app's fulfillment orders |

The reason exists only inside AutoDS. There is no AutoDS connector, MCP server or API key in
this session, so I cannot open it.

---

## Step 1 — Get the reason (2 minutes)

1. Go to **app.autods.com** and sign in.
2. Left sidebar → **Orders**.
3. Switch to the **Canceled** (or **All**) tab — a cancelled order will not be under "Open".
4. Find the order dated **14 Sep 2026**, total **$49.99**, one Bracken Lower Back Support Belt,
   size **M**. Shopify reference **#1007**.
5. Open it. The reason is in one of these places — copy whichever you see, word for word:
   - a red banner or status chip at the top of the order
   - a **Cancellation reason** / **Error** field in the order detail
   - the **Order log** / **History** tab at the bottom

Also grab, from **Orders → Settings** or the top-right account menu:
- your current **plan name**
- whether **Automatic Orders** shows as On or Off

Paste those back to me and I will tell you exactly what to change.

---

## Step 2 — While you are in there, check these four

Ordered by how often each one causes an instant accept-then-cancel. The cancellation came
**one second** after acceptance, which is a machine rejecting on a precondition, not a
supplier problem.

### 1. Buyer account + payment method  ← most likely
**AutoDS → Settings → Buyer Accounts** (sometimes "Buyer Accounts & Payment")

AutoDS has to actually buy the item from the supplier with a real account and a real card.
If no buyer account is connected, or the card on it is missing/expired/declined, AutoDS accepts
the Shopify request and then instantly cancels because it has no way to place the purchase.

**Fix:** connect the supplier buyer account and attach a valid payment method.

### 2. The product has no supplier source mapped
**AutoDS → Products →** find "Bracken Lower Back Support Belt"

Confirm it shows a live **supplier URL / source**, and that the **M** variant is mapped to a
real supplier variant. A product imported as a draft, or one whose supplier listing was
removed, has nothing to order against.

**Fix:** re-attach the supplier source and map every size variant, not just the product.

### 3. Automatic Orders is off, or not on your plan
**AutoDS → Settings → Automatic Orders** (sometimes under Orders → Automation)

Auto-ordering is a paid-tier feature on AutoDS. On a plan without it, fulfillment requests are
accepted then dropped.

**Fix:** enable it, or switch to manual fulfillment (see the fallback below).

### 4. Supplier-side stock is actually zero
Shopify showed **8 available** for the M variant at the AutoDS location, but AutoDS syncs stock
on a delay, so Shopify can be stale.

**Fix:** check live stock on the supplier listing inside AutoDS.

---

## Fallback while AutoDS is broken

Do not restart ads until an order reaches a supplier. If you want to trade in the meantime,
switch that product to **manual fulfillment**: you place the supplier order yourself and mark
the Shopify order fulfilled with the tracking number. Slower, but it never silently fails, and
it never leaves a customer charged for something that isn't coming.

---

## What would let me do this myself next time

AutoDS publishes a REST API. If you generate a key (**AutoDS → Settings → API**, on the plans
that include it) and add it to this environment, I can read order status and cancellation
reasons directly instead of routing them through you. Same for Judge.me, which is the other
place I'm currently blind — see `review_request_playbook.md`.

---

## Verification, once you have changed something

1. Place one more real order — **the 2-belt bundle this time**, since that path is still
   untested and it is what all three rebuilt ads sell.
2. Tell me the order number.
3. I check: `test: false`, the fulfillment order's `requestStatus`, whether AutoDS accepts and
   **stays** accepted, whether the bundle wrote the Back Stretcher in at $0.00, and what the
   draft Mini Pulse Massager does at add-to-cart.

Green light for ads is: a paid order reaches a supplier and produces a tracking number.
