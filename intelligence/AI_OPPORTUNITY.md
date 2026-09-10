# AI OPPORTUNITY — what to build, what to never touch (2026-09-10)

*Stack audit for sparkagent: cmail (Worker + Workers AI), voiceagent
(FastAPI + OpenAI-compat LLM + Edge TTS + YAML graphs), csec (keyword packs),
breadup (scoring/ledger formulas), drop/BigQuery (evidence lake).*

## DO — ranked by leverage

### 1. Brilliant-for-sparkies (the insight this session: own upskilling content)
Nobody teaches tradespeople interactively, and nobody teaches them the
agent-homelab stack at all. Training providers sell £9.4k classroom bundles;
the US has NEC apps (Sparky AI, SPARK NEC); **the UK has no BS 7671-native,
scenario-driven, phone-first learning product.** Build order inside it:
- **Regs tutor (RAG over BS 7671 + IET guidance):** cite-the-article answers,
  exam-style drills for 2382/2391/2921. LLMs must NEVER freestyle regs —
  retrieval + citation or fail-closed (aithesis §16: observe > ask).
- **Scenario sims:** consumer-unit photo → "what's wrong here, what would you
  test first"; 2391 result-interpretation drills; EV-fault error-code triage.
- **Homelab-with-agents course (the differentiator):** HA + MCP + n8n taught
  to sparkies, by sparkies. Creates the techy-sparky identity, the community,
  and the talent pool for agentic-energy retainers. Zero competition.
- **Business skills:** quoting, pricing psychology, review capture, MTD/tax
  basics — the rest of the job nobody teaches.
- **On-site assistant:** "ask the regs" from the van (photo → cited check).
Why it compounds: freemium learning → CPD accreditation (B2B sale to
employers/providers) → recruitment funnel (best learners → supervised hours →
stack) → **misconception analytics** (which regs sparkies fail = proprietary
safety/knowledge data; negative-data moat, aithesis §23). Learning is the top
of the supply funnel AND a product AND a dataset. Breadup's badge/SQS
machinery was born for exactly this (streaks, calibration, track records).

### 2. Quote-from-photo (multimodal intake)
Consumer-unit / damage / meter photos → scope + price range + parts list +
grant route. Already the kernel's intake; push it to customer-facing ("snap
three photos, get a firm-ish price in minutes"). Octopus does remote surveys
with humans — ours is instant and grant-aware.

### 3. Energy telemetry (HA MCP, read-only)
Battery SoC, solar yield, EV load, grid import → tariff advice, fault
detection ("battery idle 3 days"), pre-fault alerts. Octopus owns tariff
data; we own device truth. Funds the £9–19/mo "we watch your electrons"
retainer. Reads only until trust + revenue justify writes.

### 4. Back-office killers (in priority order)
EIC/cert auto-fill from job data (most-hated paperwork first) → OZEV form
pre-fill → quote follow-up sequences (proven converter per competitor
testimonials) → review request/response drafts → invoice chase tone-ladder →
MTD receipt categorisation + quarterly nudges.

### 5. Matching with explanations
Timefold-style deterministic ranker picks the sparky (never the LLM);
**the LLM explains the pick** to customer and tradie. Transparency is the
feature — tradies accept machine dispatch they can audit.

### 6. Multilingual sites (cheap, ignored by all 8 UK competitors)
voiceagent/language.py already detects 7 languages. Polish/Romanian-speaking
customers + Eastern-European crews are a huge UK-sites reality nobody serves.
Low build, real differentiation.

## NEVER — load-bearing prohibitions

1. **No safety-critical autonomy.** No DIY electrical guidance, no auto-signed
   certs, no HA control writes without human confirm, emergencies always wake
   a human. csec-gated, no waivers (SPEC S5).
2. **No replacing the QS.** AI tutors; humans certify. ECA's bootcamp critique
   is the warning label. Liability boundary explicit in every product.
3. **No building models/infra day 1.** Rent LLM/STT/TTS (ARCHITECTURE.md
   upgrade path). Fine-tune only when the misconception/failure dataset
   justifies it.
4. **No auto-send/auto-book/auto-spend.** Drafts + proposes; human confirms
   (ab rule 1). Idempotency keys on every side effect (hearthline scar).
5. **No hoarding PII/telemetry.** 90-day retention, purpose-limited, GDPR.
   Never train on customer data without consent. Trust is the product.
6. **No generic FSM rebuild.** Density + depth beat features vs US giants.
7. **No tokens, no crypto mechanics.** (breadup + agentic-inference rules.)
8. **No LLM-as-evidence.** Graph/RAG authoritative; unknowns fail closed
   (drop Rule: UNKNOWN fails closed; THESIS_REFINED).
9. **No grant decisions.** Pre-check only; OZEV decides (KERNEL.md policy).
10. **No classrooms prematurely.** Content/software now; premises only on
    revenue (SPARKAGENT_THESIS §11).
