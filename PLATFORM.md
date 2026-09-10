# PLATFORM — one machine, many trades (2026-09-10)

## The product (your definition, kept)

The automated backend for a trade business: **lead aggregation → automated
response → client calls → after-hours cover → synced calendar → WhatsApp bot →
tax-synced money → Instagram/Google demand → Maps + website → security over
all of it.** The customer buys "never worry about bs." The tradie buys jobs
done while on the tools.

## The invariant (never changes per trade)

| Module | What it is | Where it lives |
|--------|-----------|----------------|
| Intake | chat/voice/email/photo → structured job | voiceagent runtime + cmail inbox |
| Aggregation feed | calls + emails + WhatsApp + marketplace leads, ranked, one pane | 🔨 to build (LANDSCAPE §2) |
| Response engine | <60s qualified reply, slots, photo requests | voiceagent flow + tools |
| After-hours | take details, wake human only on safety | kernel prompt pattern (sparky/flowright identical shape) |
| Booking | slots → confirmations → reminders → no-show rescue | calendar/FSM adapter (stub today) |
| Comms | phone/SMS (Telnyx), email (cmail), WhatsApp (adapter), GBP messaging | cmail MCP + adapters |
| Demand | landing + exact-match ads + GBP + review flywheel | same machinery, different keywords |
| Money | invoices, payouts, ledgers, spend caps | breadup formulas + drop ledger schema |
| Shield | 14 base probes + runner + digest evidence | csec (keyword+structural grading is vertical-agnostic) |
| Controller | IDEA→OPERATING state machine, gates, receipts | ab SPEC/ARCHITECTURE |

## The variant (the ONLY things that change per trade)

From diffing `sparky_electrician_en.yaml` vs `flowright_plumbing_en.yaml` —
it's content, never machinery:

1. Services + aliases (EV install vs leak repair)
2. Price book + ranges (£350 half-day vs £85 boiler service)
3. Safety/escalation rules (sparks/burning vs burst/sewage vs gas smell)
4. Regulatory nodes (Part P + OZEV vs Gas Safe + water regs)
5. Area/hours/preferences/autonomy
6. csec pack extension (grant-guarantee vs gas-DIY lure — same 5 probe *classes*)
7. Brand + domain + number (cmail recipe, ~£15, 10 minutes)
8. Ad keywords + landing copy + photo examples

That's it. Eight content deltas. Everything else is the same binary.

## Add-a-trade checklist (days, mostly writing)

- [ ] Clone kernel YAML, rewrite the 8 deltas above
- [ ] Extend csec pack (same classes, new lures), run to green
- [ ] Brand via cmail recipe (search → social → buy → wire → phone)
- [ ] Landing + 3 ad groups + GBP category
- [ ] Run ab state machine S1→LIVE; first 3 jobs validate the variant
- [ ] Observations back to drop (new failure modes, price points)

## Why this is the moat, stated once

Competitors sell a *tool* per slice (answering OR booking OR reviews) or a
*platform* per country (lead marketplaces). Nobody sells **the whole backend
as one thing that arrives pre-loaded per trade**. The per-trade cost to us is
days of content; the per-trade value to the buyer is "my entire office." That
asymmetry — cheap for us to add, complete for them to receive — is the business.
