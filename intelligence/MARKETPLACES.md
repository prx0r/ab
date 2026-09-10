# MARKETPLACES — the stack plugs in, not competes (2026-09-10)

## The reframing

Tradies already pay Checkatrade/MyBuilder/Rated People. Don't ask them to quit.
**Be the business-side box their marketplace leads flow into** — instant
response, qualification, booking, invoice, review — with our own exclusive
EvSpark leads as the sweetener, not the pitch. We tax existing distribution
instead of building it.

## Why this wins shared leads: speed-to-lead

Every platform sells the same enquiry to 3–20 tradies. The data on shared
leads is unambiguous in direction (exact multiples vary by study): contact
rates collapse after minutes, and the first responder wins the large majority
of jobs. Tradies lose shared leads because they're on the tools — eight hours
where they can't answer anything.

Our kernel answers in <60 seconds, every time, with a qualified response
(photos requested, parking/tenure captured, slot offered). On a shared lead,
that alone flips win-rate. **Speed-to-lead is the feature; everything else is
retention.**

## How leads arrive (per source)

| Source | Lead arrives as | Our ingestion |
|--------|-----------------|---------------|
| Checkatrade | email + SMS + app alert | cmail inbox parse → classify → draft response |
| MyBuilder | email + app (shortlist ping) | same; shortlist = high-intent trigger |
| Rated People | email + app | same; credit-spent signal = intent |
| Bark | email + app | same |
| Google Business Profile | message / call | GBP messaging adapter (build); call-forward to kernel voice (zera shape) |
| EvSpark direct (ads/organic) | form → email | native; richest data (photo survey + grant pre-check) |
| Landlord/EICR partners | email/phone | manual onboard, then same pipeline |

The marketplace email formats are stable and parseable (subject lines carry
trade + postcode + job type). One parser per platform in cmail's classify
layer; quarantine rules already exist for injection in inbound mail.

## What exists vs what plugs in

- ✅ cmail: receive → classify → store → search → draft (never auto-sends
  without confirm; Phase-3 posture keeps human on send, kernel drafts in seconds).
- ✅ voiceagent: BOOK intent, callback tickets, after-hours prompts.
- ✅ csec: lead-notification phishing/probe classes extend naturally.
- 🔨 marketplace parsers (4 small format maps — days, not weeks).
- 🔨 GBP messaging adapter + call-forward number per tradie.
- 🔨 WhatsApp Business adapter (Meta BSP application; same intake pipe).
- 🔨 response-time dashboard (proof of the core claim: "we answer in 47s").

## The offer stack (order of sale)

1. **"Never miss a lead"** — plug into what you already pay for. Cheapest,
   instant value, zero behaviour change. (Entry.)
2. **"Win more of them"** — instant qualified response + review machine.
   (Retention, measurable win-rate delta.)
3. **"Here's more"** — exclusive EvSpark leads in your postcode. (Expansion,
   only we can give this.)
4. **"Run it all here"** — diary, invoices, payouts, aftercare. (Full stack,
   retainer + spread.)

Each step is purchasable alone; each makes the next obvious. No rip-and-replace
pitch at any point.

## What this changes in the plan

- Phase 1 (installer) unchanged — it generates the proof + reviews + data.
- Phase 2 wedge gets easier: "keep your Checkatrade, plug us behind it" beats
  "leave your leads and trust us." First-year tradie revenue can be pure SaaS
  (£99–249/mo) before any per-job spread.
- MIDDLEMAN_THESIS dispatch (§4) stays, but demand-side pressure drops: the
  machine fills from 6 sources on day one, not from our ads alone.
- COMPETITION.md positioning holds — every clause is still a platform
  complaint inverted — but the sale is now *augment*, not *replace*.
