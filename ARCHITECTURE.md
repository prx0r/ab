# ab — ARCHITECTURE

## The kernel model

A business is a **compiled artifact**. The kernel compiles it from intelligence:

```text
INTELLIGENCE (drop)
  campaign + evidence snapshot + rubric version + mechanisms + theses
        │
        ▼
┌─────────────────────────────────────────────────┐
│                    ab kernel                     │
│                                                  │
│  L1 IDENTITY   L2 RUNTIME   L3 SHIELD   L4 LEDGER │
│   (cmail)     (voiceagent)  (csec)    (breadup)   │
│                                                  │
│  gated state machine: IDEA → … → LIVE → OPERATING│
└─────────────────────────────────────────────────┘
        │
        ▼
RUNNING BUSINESS (domain + inbox + phone + agent + P&L)
```

## Layer contracts

### L0 — Intelligence (read-only)

Source: `/root/drop` (campaigns, docs, corpus, BigQuery via agent-vault creds).

`ab` consumes, never writes:
- `campaign_version_id` — hash of the campaign hypothesis JSON
- `evidence_snapshot_id` — hash of evidence IDs used
- `rubric_version_id` — hash of rubric config + gate code
- mechanism edges relevant to the vertical (e.g. `WARRANTY_EXPIRY_CHANNEL_FLIP`)
- thesis constraints (e.g. `CUSTOMER_PURCHASABLE_SHARE`, self-service ratio)

These three IDs are pinned on every Business (drop's launch rule) so any
business can be traced back to the exact intelligence that justified it.

### L1 — Identity (`cmail`, Cloudflare Worker)

Endpoint: `https://cmail.tradesprior.workers.dev/mcp` — 23 tools, all working.

| Step | Tool | Cost | Gate |
|------|------|------|------|
| name generation | agent + `name.search` | $0 | — |
| availability | `name.search` (15 TLDs × 4 registrars) | $0 | — |
| handles | `name.social` (13 platforms) | $0–$0.04 | — |
| purchase | `name.cf_purchase` | ~$10/yr | **`confirmed:true`** |
| email | `name.wire_email` (catch-all → worker) | $0 | **`confirmed:true`** |
| phone | `name.phone_search` / purchase (Telnyx) | ~$2/mo | **`confirmed:true`** (needs `TELNYX_API_KEY`) |
| inbox ops | `email.*` (inbox, search, read, draft) | $0 | send needs **`confirmed:true`** |

Output: owned domain, live `hello@`/`support@`, provisioned number, handle map.
Stored on the Business as `identity` with receipts (registrar response, zone id).

### L2 — Runtime (`voiceagent`, FastAPI + YAML graph)

Source: `/root/voiceagent`. The graph is authoritative; the LLM is not.

`ab` generates a business kernel YAML from the Business spec:
- `business:` block (name, locale, phone, hours) ← from `identity`
- `agent.system_prompt` ← from vertical playbook + thesis constraints
- `nodes:` (services, policies, faqs, escalations) ← from drop compatibility/
  service graph + regulatory requirements of the country
- `tradie:` block (autonomy, price book, service area) ← from economics
- `voice:` block (locale voice) ← from country

Upgrade path (voiceagent ARCHITECTURE.md): Day 1 web chat + Edge TTS → Day 2
LiveKit SIP / Retell / Vapi for real phone → Day 3 Neo4j + hybrid retrieval →
Day 4 real tools (calendar, CRM/FSM, payments).

`ab` does not fork voiceagent. One kernel YAML per business, loaded via
`BUSINESS_CONFIG`. (Long-term: drop HANDOVER directive — voiceagent evolves
into the Drop Resolver Runtime; `ab` rides that, doesn't duplicate it.)

### L3 — Shield (`csec`, Python CLI)

Source: `/root/csec`. 14 probes (9 chat + 5 intake), UK-shaped.

Gate rule: **all applicable probes HELD, evidence JSONL digest-pinned, exit 0 —
or the business does not advance past `KERNELLED`.**

```bash
BASE=http://127.0.0.1:8080 python3 -m csec.runner
# → evidence/run_*.jsonl, exit 1 on any BREACH
```

New verticals extend packs (plumbing next per csec roadmap; EV-install
additions: OZEV-grant guarantee, DNO-misrouting, Part-P DIY lure — see
`businesses/evspark/KERNEL.md`). Waivers are explicit, per-probe, with reason.

### L4 — Ledger (`breadup` formulas + `drop` decision events)

- Opportunity scoring: breadup `evaluate()` (EV, ROIC, confidence) at `SCORED`.
- Track records: breadup SQS-style calibration as runs accumulate.
- Money: three ledgers, never merged (fiat / credits / external).
- Every controller action → `drop`-style DecisionEvent (what, why, evidence).
- Terminal reward: matured CM2 (drop Rule 8).

## The state machine

```text
IDEA ──score──▶ SCORED ──brand──▶ BRANDED ──provision──▶ PROVISIONED
  │                │                 │                       │
  kill           kill              kill                    kill
                                                    (domain/email/phone live)

PROVISIONED ──kernel──▶ KERNELLED ──redteam──▶ SHIELDED ──stage──▶ STAGED
                                                                │
                                                     human go-live│confirmed:true
                                                                ▼
                                              LIVE ──operate──▶ OPERATING
```

Stage → evidence required:

| Stage | Required evidence |
|-------|-------------------|
| `SCORED` | campaign refs pinned (3 IDs), EV/ROIC worksheet, kill-check vs drop gates |
| `BRANDED` | `name.search` + `name.social` receipts, human brand pick |
| `PROVISIONED` | registrar receipt, zone id + catch-all proof, phone receipt, inbox live check |
| `KERNELLED` | kernel YAML committed, `/health` + `/chat` smoke pass on staging port |
| `SHIELDED` | csec run JSONL, all applicable HELD, waivers (if any) documented |
| `STAGED` | end-to-end dry run (email in → agent draft → csec-clean), unit economics sheet |
| `LIVE` | human `confirmed:true`, launch checklist signed |
| `OPERATING` | weekly P&L + decision log; every £1 in/out recorded |

Any stage may transition to `KILLED` with a reason. Killed businesses are kept.

## Data flow (evspark example)

```text
drop: uk-ev-charger campaign + WARRANTY_EXPIRY_CHANNEL_FLIP + THESIS_REFINED
  → ab SCORED: services track (technician procurement ⇒ orchestration, not D2C)
  → cmail: evspark.co.uk + hello@evspark.co.uk + Telnyx number
  → voiceagent: sparky v2 kernel (install + grant + fault triage)
  → csec: 14/14 HELD (+ EV-install probes)
  → LIVE: OZEV-authorised installer funnel + Checkatrade bridge + organic
  → ledger: revenue, CM2, warranty-flip observations flow back to drop
```

## What ab is NOT (v1)

- Not a new agent runtime (voiceagent is).
- Not a new inbox (cmail is).
- Not a new security tool (csec is).
- Not a new scoring system (breadup + drop rubric are).
- Not autonomous with money. The controller is autonomous with *information*;
  every money or public-surface action has a human gate.
