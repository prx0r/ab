# ab — Autonomous Business Kernel

> **One sentence:** `ab` turns market intelligence into running businesses.

`ab` is the higher-level controller. It does not replace any existing repo — it
orchestrates them. Given a scored opportunity (from `drop`), `ab` generates a
complete business: brand + domain + email + phone (via `cmail`), a customer-facing
runtime (via `voiceagent` kernels), a security gate (via `csec`), and an economic
ledger (via `breadup` formulas + `drop` decision events).

```text
drop (intelligence) ──┐
                      ▼
              ┌──────────────┐
              │      ab      │  ◄── you are here
              │  controller  │
              └──────┬───────┘
        ┌───────────┼────────────┐
        ▼           ▼            ▼
     cmail      voiceagent      csec
   (identity)   (runtime)     (shield)
        └───────────┼────────────┘
                    ▼
              breadup/drop
               (ledger)
```

## The thesis

Every repo we built is one organ of the same animal:

| Repo | Organ | Job |
|------|-------|-----|
| `drop` | eyes | finds WHERE the opportunity is (country × asset × trigger) |
| `cmail` | hands | acquires identity (domain, email, phone, handles) |
| `voiceagent` | mouth | runs the customer surface (chat, voice, intake) |
| `csec` | immune system | red-teams every surface before it touches money |
| `breadup` | metabolism | scores opportunities, tracks P&L, pays out |
| **`ab`** | **nervous system** | **decides, sequences, gates, remembers** |

No new commerce-agent repo. No new voice repo. No new security repo.
`ab` is sequencing + state + gates over systems that already work.

## Business instances

| ID | Business | Country | Track | State |
|----|----------|---------|-------|-------|
| `ab-001` | EvSpark Electrical (evspark.co.uk) | GB | services | `IDEA` → see `businesses/evspark/PLAN.md` |

## Repo layout

```text
ab/
├── README.md                  this file
├── AGENTS.md                  operating manual for agents working in ab
├── ARCHITECTURE.md            kernel layers, repo contracts, data flow
├── SPEC.md                    generation pipeline: stages, gates, evidence
├── ROADMAP.md                 build order for ab itself
├── schemas/
│   ├── business.schema.v1.json        the Business entity
│   └── generation-run.schema.v1.json  one kernel run, stage by stage
├── intelligence/
│   └── UK_INSIGHTS.md         distilled UK + EV intelligence (drop + live 2026 data)
└── businesses/
    └── evspark/
        ├── PLAN.md            working plan for EvSpark Electrical
        └── KERNEL.md          sparky v2 kernel outline
```

## Rules

1. **ab never touches money without a human `confirmed:true`.** Domain purchase,
   email send, phone purchase, ad spend, go-live — all require explicit
   confirmation. The controller proposes; the human disposes.
2. **Every stage transition requires evidence.** No evidence, no advance.
   Evidence is a file, a digest, a receipt — never a claim.
3. **csec must be green before STAGED.** No business reaches a customer without
   14/14 HELD (or documented waivers for inapplicable probes).
4. **Intelligence is read-only input.** `ab` reads `drop` campaigns, BigQuery,
   theses. It never edits them. Findings flow back as new observations, not
   rewrites.
5. **Kill fast, preserve everything.** Killed businesses stay in the repo with
   the reason. Rejected paths are training data (drop Rule 10).
