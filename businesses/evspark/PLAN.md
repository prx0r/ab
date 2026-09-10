# EvSpark Electrical — working plan (`ab-001`)

*Brand: EvSpark Electrical · Domain: evspark.co.uk (~£10/yr, available) ·
Country: GB · Track: **services** (HCC variant C — repair orchestration) ·
State: `IDEA`. Full background: `intelligence/UK_INSIGHTS.md`.*

## Why services, not parts (the one-paragraph justification)

Drop scored UK EV aftersales 95 → pivoted to 78 as "PCB Repair + Technician
Orchestration": whole-unit replacement is technician procurement (Part P,
smart regs, DNO, OZEV-authorised-installer requirement for grants), so
`CUSTOMER_PURCHASABLE_SHARE` ≈ 0 for D2C and a parts store fails G4. The
install + grant + triage + aftercare bundle is where the uncertainty — and
the margin — lives. EvSpark is that bundle, with the voiceagent kernel as the
intake surface and csec as the gate.

## Unit economics (verify in S6, targets for OPERATE)

| Line | Value | Basis |
|------|-------|-------|
| Mean domestic install | ~£892 | EV Cable Hub 2026 |
| Labour (Sparky price book) | £350 | `voiceagent/knowledge/sparky_electrician_en.yaml` |
| Hardware (7kW smart unit) | ~£350–450 | OZEV list units; verify with 3 distributors |
| Sundries + cert + DNO | ~£80–120 | RCBO, SWA/m, EIC, notification |
| Grant offset (to Mar 2027) | −£500 (eligible jobs) | OZEV, 75% to £500 cap |
| Target contribution/job | **≥£250** (grant) / **≥£180** (non-grant) | SPEC S6 sheet |
| Break-even | **~8 jobs/mo** at £250 CM vs ~£2k fixed | Solo + subcontract spark |
| CAC ceiling | ≤£60/job (grant sprint) / ≤£90 (post-cliff) | Checkatrade lead £15–30; Google £2–5/click |

## Permissions & compliance (start day 1, all tracked in BUSINESS.json)

1. **OZEV-authorised installer** — application + approved-hardware + data-reporting. THE gate to grant £. Owner: human. Target: applied week 2.
2. **NICEIC/NAPIT (or QS route)** — Part P notifiable work. Subcontract qualified spark initially if registration lags — never operate outside scope.
3. **Insurance** — public liability + professional indemnity, EV-specific.
4. **GDPR** — 90-day transcript retention (kernel default), ICO registration.
5. **Accounts** — separate business bank; three ledgers from day 1 (breadup rule).

## Phases

### Phase 0 — Validate (week 1, £0, no gates passed yet)

- [ ] S1 SCORE: pin campaign/evidence/rubric IDs, EV/ROIC worksheet → `SCORED`
- [ ] 10 installer reality calls (3 distributors, 3 OZEV installers, 2 landlords,
      2 EICR electricians): hardware net pricing, lead times, grant friction,
      subcontract day-rates. Kill-check: if net hardware >£500 or no spark
      available <£250/day in target postcode → HOLD, document.
- [ ] Pick service area: one underserved geography first (drop dev-plan rule:
      one country wins first → one postcode cluster wins first). Candidate:
      commuter belt with high off-street parking + low installer density —
      verify via Google Places actor (`compass/crawler-google-places`).

### Phase 1 — Brand + provision (week 2, ~£15, human gates)

- [ ] S2 BRAND: 30+ seed batch via cmail, `.co.uk` focus, human picks.
      (evspark.co.uk is the standing candidate from `cmail/a-logs/EVSPARK_BRAND.md`.)
- [ ] S3 PROVISION: `cf_purchase` + `wire_email` + Telnyx number (3 × confirmed).
      Receipts → `businesses/ab-001/receipts/`. Verify inbox round-trip.
- [ ] Free handles (GitHub, npm, Bluesky…); queue manual five with links.
- [ ] BUSINESS.json written, STATE → `PROVISIONED`.

### Phase 2 — Kernel + shield (weeks 3–4, £0)

- [ ] S4 KERNEL: sparky v2 per `KERNEL.md` → staging port → smoke pass.
- [ ] S5 SHIELD: full csec run + 3 new EV-install probes (grant-guarantee,
      DNO-misroute, Part-P-DIY). Exit 0, JSONL committed. STATE → `SHIELDED`.
- [ ] S6 STAGE: dry-run email→draft loop, 3 edge-case chats, economics sheet,
      launch checklist (OZEV applied, insurance quoted, spark contracted).

### Phase 3 — Soft launch (weeks 5–8, capped £300 test budget, human gate)

- [ ] S7 LIVE (`confirmed:true`): listings on Checkatrade/MyBuilder (buy
      demand while organic builds), Google Business Profile, 3 landing pages
      (home install / landlords+flats / fault repair).
- [ ] Human handles every job; kernel runs `observe` on live traffic
      (logs + drafts, sends need confirm). Target: 4–8 jobs, CM ≥£180/job,
      5★ reviews, photo library for the graph.
- [ ] OZEV authorisation lands → grant jobs unlock → CM step-change.

### Phase 4 — Grant-cliff sprint (Oct 2026 → Mar 2027)

- [ ] Aim grant-shaped demand: renters/flats, landlords (200-socket cap!),
      SME workplace, schools (£2k/socket), cross-pavement early adopters.
- [ ] £500/socket messaging everywhere; "final year" urgency is factual.
- [ ] Build the post-cliff machine in parallel: reviews, referral loop,
      landlord retainer offers, EICR-bundle pilot (RISK_PRICER mechanism),
      remote-triage product (REMOVABLE_CONTROL mechanism).
- [ ] Target exit: ≥15 jobs/mo, blended CM ≥£220, CAC ≤£60, csec green on
      every kernel change, 40+ reviews.

### Phase 5 — Post-grant (from Apr 2027)

- [ ] Demand engine without grants: 2p/mile economics pages, tariff-switch
      bundle, second-charger upgrades, solar/battery cross-sell,
      warranty-flip repair funnel (2019–22 cohort ageing),
      landlord compliance retainers.
- [ ] Parts-aftercare wedge (the drop pivot's second half): mail-in/swap PCB
      triage for orphaned units — low van time, national catchment.
- [ ] STATE → `OPERATING` with weekly P&L; observations flow back to drop
      (prices, failure modes, mechanism confirmations).

## Demand stack (in order)

1. Grant-shaped search ("OZEV installer near me", "landlord EV charger grant").
2. Marketplaces (Checkatrade/MyBuilder — rented demand, deliberate bridge).
3. Landlord/HMO direct (letters + EICR bundle — highest £/effort).
4. Organic (compatibility-style content: "which charger for [flat / no-driveway /
   3-phase / solar]" — the drop graph habit applied to services).
5. Referral + review flywheel (every job → photos → review → case page).

## Metrics (weekly from LIVE)

Jobs, quoted→booked %, CM/job, CAC/job, review count/score, csec status,
grant-pipeline £, warranty-flip inbound, kill-watch (net hardware, spark
day-rate, CPC drift). Monthly: predicted-vs-realised calibration.

## Kill conditions (write KILLED.md, preserve everything)

- OZEV authorisation refused AND no path (grants were the sprint fuel).
- No qualified spark <£250/day sustained in area (delivery breaks).
- Net hardware + sundries push non-grant CM <£120/job at market prices.
- CAC >£120/job for 4 consecutive weeks post-optimisation.
- Any safety incident → immediate HOLD, csec + kernel review before resume.

## Un-kill conditions (what would revive)

- OZEV path reopens / new scheme announced.
- Cross-pavement category formalised with council standing approvals.
- Distributor net pricing improves ≥15% (volume terms).
