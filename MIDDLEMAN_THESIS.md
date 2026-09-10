# THE MIDDLEMAN THESIS

> We sit between the person with the problem and the person with the van.
> We own intake, diagnosis-routing, booking, after-hours, and money movement.
> Tradies do regulated work; we do everything else — and take the spread.

## The five roles (drop's decisive split)

`drop/rubric/RUBRIC_A_BINARY_GATE.md:30-35` splits every transaction into
`problem_noticer / diagnoser / sku_selector / payer / installer`. The middleman
owns every role **except** the regulated one:

| Role | Owner | Notes |
|------|-------|-------|
| noticer | customer | finds us via grant-shaped search, marketplace, landlord deal |
| diagnoser | **us (kernel)** | photo survey + remote triage + grant pre-check |
| sku_selector | **us + tradie** | we scope, tradie confirms on site |
| payer | customer / landlord / grant body | we route, never guarantee (`policy.ozev`) |
| installer | **onboarded tradie** | the only role we never touch |

Track-router rule (`drop/rubric/TRACK_ROUTER.md:40-47`): when the professional
is the chooser, storefronts are not the surface — **orchestration is the
business**. `BUYER_SELECTION_GATE.md` Cases C/D are our hunting ground; the
anti-cheat rule ("a public cart button proves only retail availability") is
why competitors misread these markets as D2C.

## The stack, layer by layer

### 1. Demand intake (BUILT)

- `voiceagent/app/main.py` — `/chat`, `/graph/search`, `/health`; session kernel.
- `voiceagent/knowledge/sparky_electrician_en.yaml` — Sparky tenant (EV, consumer
  unit, fault; price book; `semi_auto`; after-hours prompt).
- `voiceagent/knowledge/flowright_plumbing_en.yaml` — **second tenant; proves
  per-tradie affinity feeds** (`plumber affinities ≠ sparky affinities`).
- `voiceagent/app/flow.py` — BOOK intent + EN/NO/SV templates.
- `voiceagent/app/tools.py` — ticket / callback / booking-request (SQLite-backed).

### 2. Identity + comms (BUILT)

- `cmail` 23 MCP tools: domain search/purchase, catch-all email wiring, Telnyx
  phone/SMS, 13-platform handle checks. Recipe: `/root/cmail/RECIPE.md`.
- `stevejobless/NORTHSTAR.md` — the name→domain→email→number→business loop with
  explicit machine/human division of labor. This is our provisioning runbook.

### 3. Shield (BUILT)

- `csec/packs/chat_uk.py` + `intake_uk.py` — 14 probes mapping 1:1 onto
  middleman failure modes (grant guarantees, DNO misrouting, DIY lure,
  price-book pumping, PII fishing, urgency spoofing).
- Gate: exit 0 + committed JSONL before any customer contact (`ab/SPEC.md` S5).

### 4. Dispatch — tradie matching (SPEC'D, NOT BUILT)

- `voiceagent/docs/REPO_COMPILATION.md:93-97` states the architecture outright:
  **Timefold constraint solver; hard feasibility first, assignment second,
  travel/cost/fairness last; never ask an LLM to pick technicians directly.**
- `voiceagent/tools/calendar.py` — 3-line stub (Google Cal / Cal.com /
  ServiceTitan / Jobber boundary). This is the highest-value unbuilt piece.
- Today's `tradie:` block is single-tenant config (area, price book, affinity).
  The multi-tradie form is: N tradie blocks + job → ranked offer (FlowRight
  already proves the ranking input exists).

### 5. Tradie onboarding (MISSING — closest: zera)

- `zera/README.md` (CallStaff): scrape website → generate receptionist config →
  demo number → connect real number. **This funnel shape is our onboarding
  template**: scrape tradie (Checkatrade/NICEIC register) → generate kernel +
  price book → demo inbox/number → connect their real number → jobs flow.
- Nothing in `ab`/voiceagent implements this yet. M-roadmap item.

### 6. Money — ledgers, payouts, spend policy (PRIMITIVES EXIST, NOT WIRED)

- `breadup/docs/05-payments-bread.md` — three ledgers never merged (fiat /
  credits / external); creator-payout formula
  (`gross − platform_fee − refunds − settlement = payable`) — read "creator"
  as "tradie"; agent spending policies (caps, allowlists, human-above-threshold,
  idempotency keys).
- `drop/AGENTS.md` Rule 6 — every action → DecisionEvent, every cost →
  CostLedger; `drop/bigquery/economic_ledger_ddl.sql` is the table shape.
- `voiceagent/docs/REPO_COMPILATION.md:63-65` — finance as **typed tools with
  narrow scopes** (paypal/agent-toolkit, stripe/ai); Temporal for durable
  booking/refund/payment workflows (`:82-87`).
- Explicit gap (`drop/docs/STATE_OF_BIGQUERY.md:128-133`): **no job table for
  the service model** — the service-model data layer is unbuilt. That table
  (job → visits → invoices → payouts) is the fintech core.

### 7. Services evidence (THIN — D2C templates dominate)

- `drop/docs/HCC_V2.md:137-143` lists the services track (radon 83, lead-pipe
  77) but `campaigns/active/*.md` are all D2C templates carrying
  `Negative: installation, service` ad copy — the services track has **no
  campaign template yet**. `ab-001` (EvSpark PLAN) is its first instance.
- Supplier-side script exists for parts (`drop/rubric/SUPPLIER_VALIDATION_SCRIPT.md`,
  esp. Q17 licensed-installer restriction, Q18 structured RFQs) — needs a
  **tradie-side twin** (day-rate, certs, area, insurance, availability feed,
  payout details).

## Endgame (the app sparkies join)

```text
customer job in (chat/voice/email/photo)
  → kernel scopes + prices (ranges) + grant-routes
  → dispatch ranks onboarded tradies (feasibility → cost → fairness)
  → tradie confirms in app (or auto for routine at full_auto)
  → job executed, cert uploaded, customer pays us
  → ledger splits: tradie payout − platform spread − grant applied
  → after-hours + reviews + recall + aftercare stay with us
```

Tradie value prop (why they join instead of Checkatrade): after-hours phone
answered, diary filled, grant paperwork done, no chasing invoices, payouts on
schedule. Our moat is the intake + data + review graph, not the van.

## Build order (middleman deltas to ab/ROADMAP.md)

1. **Job ledger schema** (jobs, visits, invoices, payouts) — fills the
   STATE_OF_BIGQUERY gap; design-only, mirrors `economic_ledger_ddl.sql`.
2. **Tradie validation script** — twin of SUPPLIER_VALIDATION_SCRIPT for
   sparkies (certs, insurance, area, rates, availability, payout rails).
3. **Dispatch v0** — deterministic ranker over N tradie blocks (no solver yet);
   Timefold when volume justifies it. LLM never picks.
4. **Calendar/FSM adapter** — implement `tools/calendar.py` (Cal.com first,
   cheapest; Jobber/ServiceTitan when tradies demand it).
5. **Onboarding funnel** — zera-shaped: scrape → kernel → demo → connect.
6. **Payout rail** — Stripe Connect style; breadup payout formula; typed finance
   tools; human-above-threshold forever.
