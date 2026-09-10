# SPARKIES — targeting plan (ab-001, Phase 0–3)

*Two asks, one list. Ask 1 (now): do our jobs on day-rate. Ask 2 (later):
join the stack. Never pitch Ask 2 before delivering Ask 1.*

## 1. The four segments (same cluster, different pitch)

| Segment | Find them | Pitch | Value to us |
|---------|-----------|-------|-------------|
| **Busy local spark** (2–5 staff, diary full-ish) | NICEIC/NAPIT find-a-contractor, Checkatrade/MyBuilder profiles, Places 4.5★+ | overflow + after-hours cover + zero admin; "we fill gaps, you never touch paperwork" | delivery capacity + credibility |
| **Newly qualified / 1-man band** (<3 yrs, thin reviews) | training-provider graduates, MyBuilder new profiles, Instagram/TikTok starters | leads + backend + reputation-from-zero; "jobs and 5★s from week one" | loyal supply, grows with us |
| **EICR/landlord spark** (testing + remedial) | landlord agents, EICR-heavy profiles, letting-agent suppliers | EV bolt-on income on visits you're already doing; we scope + grant-handle | property access + volume |
| **Career changer (supervised)** | bootcamp providers, adult-diploma centres | ladder + supervised hours + jobs at the end (SUPPLY.md) | pipeline Monopoly later |

Phase 0–1 needs exactly ONE: prefer a busy-local (competence proven) with
new-spark backup. Quality over quantity until 10 jobs done.

## 2. List build (one cluster, 50 names)

1. Apify Places sweep (GOOGLE_SETUP §3): "electrician {town}" × cluster towns
   → name, rating, review count, phone, website. Sort by: few reviews + decent
   rating (hungry-good) FIRST, then high-volume (capacity), skip <3.5★.
2. Cross-check NICEIC/NAPIT registered (Part P cover) + Checkatrade presence
   (tells you who already buys leads — warmest).
3. Enrich: website → about page (firm size, EV mention?), reviews → recency
   (active?), socials → hiring posts (capacity crunch = our pitch lands).
4. Output: `businesses/ab-001/receipts/sparky_list.csv` — 50 rows, source +
   segment tag each. Evidence, not vibes.

## 3. Outreach sequence (14 days, lead-first)

No cold SaaS pitch exists in this plan. Every touch carries proof or books proof.

- **Day 1–3 (email, all 50):** subject carries the cluster + the goods —
  "3 EV jobs in {town} this month — want the first free?" Body: who we are
  (EvSpark, local, OZEV route), what a qualified lead looks like (photo survey
  + grant pre-check + slot — attach a SAMPLE scope pack), one ask: 10-min call.
  B2B to published business addresses, opt-out honored (PECR legitimate
  interest; screen sole-trader mobiles against TPS before any cold call).
- **Day 4–7 (calls, engaged + Ltd cos):** 10-min script — their capacity,
  day-rate, EV experience, Part P cover, area. Qualify for partner fit, not
  stack interest. Goal: 5 deep conversations.
- **Day 5–10 (ads live in parallel):** first real leads flow → warm-transfer
  the first TWO free to the best-fit spark WITH the full scope pack (photos,
  parking, grant route, customer briefed, slot proposed). Free means free —
  no contract, no catch, one line: "more where that came from."
- **Day 10–14 (close):** partner terms v0 (below) with ONE spark; keep two
  warm backups. Then stop recruiting and deliver — reputation compounds only
  from done jobs.

Funnel math (plan): 50 → 15 replies → 5 calls → 2 trials → 1 partner.
If replies <10: list wrong (re-sweep adjacent town) or subject wrong (A/B once).
If trials won't close free: offer paid day-rate trial, never beg.

## 4. Partner terms v0 (one page, handshake-simple)

- Day-rate £250–300 (verify in calls; sparky book says £350 labour/job all-in
  as the envelope), paid weekly, no chasing (we hold customer money).
- We supply: scoped job pack, customer comms, grant paperwork, slot, review
  capture, cert filing. They supply: van, tools, competence, certs, insurance.
- Sign-off: photos + EIC per job to us same-day; faults triaged by us first.
- Reviews go to EvSpark AND their business (dual capture — their asset too).
- 30-day rolling, either side walks. Migrate to per-job split (15–20% spread)
  once monthly volume >8 jobs — contracted then, not now.

## 5. From partner to platform (Ask 2, Phase 2+)

Only after 10+ joint jobs + their review count visibly moved. The pitch writes
itself from the ledger: "we sent you £X revenue, answered Y calls, chased £Z
invoices — the stack does that for everything, not just our jobs: £149/mo."
Show their own numbers, not a deck. First convert is the reference; film it
(with permission) as the recruitment asset for sparkies 3–5.

## 6. Triggers

- No partner by day 14 → widen cluster OR raise day-rate (price signal, not
  effort signal) OR take EICR-partner route (property access first).
- Partner churns → exit interview logged to OBSERVATIONS.md; backups activated.
- Partner wants exclusivity → yes within cluster, in exchange for capacity
  commitment + stack adoption. Exclusivity is earned by volume, given for lock-in.
