# Review Request Playbook — ready to switch on

**Status: NOT SENT. There is nobody to send it to yet.**

Every order in the store (#1001–#1006) is flagged `test: true` in Shopify. #1001–#1004 belong
to a single customer id, #1005 and #1006 are ids with zero completed orders, three of the six
are cancelled, and the other three were fulfillment-declined and never delivered. No product
has reached a real buyer, so there is no honest review to ask for.

Seeding Judge.me from those orders would manufacture the same fake social proof that got the
Ad 5 creative retired — and it would be traceable, because the reviewer would be the store
owner's own test account.

Everything below is ready to run the day a real, delivered order exists.

---

## Eligibility — who gets asked

Send only when **all** of these are true:

- `test` is `false`
- order is not cancelled and not refunded
- fulfillment status is `SUCCESS` **and** `deliveredAt` is set
- at least **10 days** past `deliveredAt` — a back support belt needs a few shifts of wear
  before anyone has a real opinion
- the customer has not already been asked about this order

Never send to a test order, a cancelled order, or an address matching the store owner's.

---

## Timing

| Step | When | Purpose |
|---|---|---|
| Request | delivered + 10 days | First ask |
| Reminder | request + 7 days, only if no review | Roughly doubles response rate |
| Stop | after the reminder | One reminder, then leave them alone |

## Where to turn it on

Judge.me's automation lives in the Judge.me dashboard, not in Shopify Admin, and this session
has no Judge.me API token — `judge.me/api/v1` returns "Failed to authenticate". Enable it at
**judge.me → Settings → Review Requests**: set the trigger to *Fulfilled/Delivered*, the delay
to 10 days, enable one reminder at 7 days, and turn **on** photo and video uploads. Photo
reviews are the asset that matters for this product.

---

## Request email

**Subject:** How's the belt holding up?

> Hi {{first_name}},
>
> You picked up a Bracken lower back support belt about a week and a half ago, so you've
> probably had it through a few full days by now.
>
> Would you tell us how it's going? A couple of honest sentences is plenty — how it fits, how
> it wears over a long shift, whether you'd pick the same size again. If it isn't working for
> you, we'd rather hear that too; the 60-day money-back guarantee is there for exactly that.
>
> {{review_button}}
>
> If you can add a photo of it on, that helps the next person more than anything we could
> write ourselves.
>
> — The Bracken team
>
> We make one thing well. Reply to this email and a person reads it.

**Reminder subject:** One question about your Bracken belt

> Hi {{first_name}},
>
> Just the one nudge, then we'll leave you to it — how has the belt been?
>
> {{review_button}}
>
> Two sentences is genuinely enough.
>
> — The Bracken team

---

## Rules for the copy

- Never offer a discount, entry, credit or gift in exchange for a review. A paid-for review is
  not usable as social proof and, in the US, an incentivised review presented as organic is an
  FTC problem.
- Never ask for a *positive* review, or route unhappy customers away from the public form.
- Ask for the photo every time. Photo reviews on a worn product outperform text.
- Do not ask about the Lumbar Back Stretcher or Mini Pulse Massager until those have actually
  shipped to someone.

## What this unlocks

Once real reviews land, they can legitimately appear in:
- the product page widget (currently `data-shop-review-count="0"`)
- a new ad concept D built on genuine quotes — the replacement for the retired Ad 5
- the ad `link_description`, where the fabricated "(4.8)" used to sit

Until then, every Bracken ad runs with **no rating, no review count and no testimonial**.
