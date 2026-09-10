# UK INSIGHTS — distilled from drop + live 2026 data

*Date: 2026-09-10. Sources: `drop` campaigns/docs/corpus/BigQuery state,
GOV.UK EVCI statistics (1 July 2026), DfT grant guidance ( Apr 2026 ), OZEV
installer docs, EV Cable Hub 2026 census. Numbers below are the freshest
published; treat installer-price points as ranges to verify, not facts.*

## 1. The installed base (why the UK, why EV, why now)

| Fact | Value | Source |
|------|-------|--------|
| Plug-in car parc (UK) | ~2.25M (1.44M BEV + 812k PHEV) | EV Cable Hub census 2026 |
| Domestic charge points installed | **968,400** (+214,800 in year to Jun 2026) | EV Cable Hub 2026 |
| Grant-funded home installs since 2013 | 412,682 (10,833 LTM) | GOV.UK EVCI, 1 Jul 2026 |
| Grant-funded workplace installs since 2016 | 85,547 (12,489 LTM) | GOV.UK EVCI, 1 Jul 2026 |
| Public EV chargers | 121,171 (28,887 rapid+) | DfT/Zapmap, 1 Jul 2026 |
| BEV drivers with home charging | 71.8% | EV Cable Hub 2026 |
| Share of charging energy delivered at home | **78.4%** | EV Cable Hub 2026 |
| Mean install cost | **£892** (£526 with grant); 24.2% got support | EV Cable Hub 2026 |
| Home vs public energy price | 9.4p vs 58p/kWh (~2p/mile home) | EV Cable Hub / DfT 2026 |

Reading: home charging is THE product (78% of energy), the install run-rate is
~215k/yr, mean ticket ~£892. A ~£190M/yr domestic install market growing with
the parc. Public charging is someone else's capex game — not ours.

## 2. The grant window (the forcing function)

OZEV restructured 1 Apr 2026: **£500/socket (was £350), 75% of cost, 5 schemes,
all closing 31 Mar 2027 — stated final year.**

| Scheme | Cap | Penetration to date | Read |
|--------|-----|---------------------|------|
| Renters + flat owners | £500/socket | 26,504 sockets ever (9,301 LTM) | tiny vs millions of flats — **gap** |
| On-street / cross-pavement | £500/socket | new (2025 £25m gully scheme) | brand-new category, no incumbents |
| Workplace (WCS) | £500 × 40 sockets | 85,547 ever, accelerating | SME long tail, underserved |
| Landlords | £500 × 200 sockets | **1,912 sockets ever** | effectively untouched |
| Schools (WCS education) | **£2,000/socket** | new | highest £/job in the system |

Plus: Electric Car Grant (£2bn, up to £3,750/car, 55k+ drivers) pulls new EVs
→ pulls installs with a 1–3 month lag. Permitted-development relaxed (2026).

**Implication:** 6-month boosted-grant sprint (Sep 2026 → Mar 2027) then a
cliff. A business that (a) becomes OZEV-authorised fast, (b) aims at the
low-penetration schemes (flats, landlords, cross-pavement, schools, SME
workplace), and (c) builds a non-grant engine for post-Mar-2027 is positioned
for both sides of the cliff. Grant-chasers without (c) die in April.

## 3. What drop got right about UK EV (and the pivot)

- `campaigns/active/uk-ev-charger.md` scored 95 → **PIVOT 78/100**:
  "UK EV Charger PCB Repair + Technician Orchestration" (HCC_V2 #11).
- THESIS_REFINED: "EV charger replacement (**often technician procurement**)"
  → weaker than thought **as D2C**.
- The refined equation's load-bearing variable is `CUSTOMER_PURCHASABLE_SHARE`:
  whole-unit EV charger replacement is near-zero self-service (Part P
  notifiable work, smart-charge-point regs, DNO notification, OZEV-approved
  hardware list, grant requires authorised installer).

**The pivot is correct and we adopt it:** no parts store. The business is
**HCC variant C — REPAIR ORCHESTRATION**: install + grant handling + fault
triage + aftercare. The eBay UK Pod Point PCB-repair listing (HCC source 20)
validates a repair-aftercare wedge exists.

## 4. Mechanisms from drop's GB graph that fire here

All three GB-replicated mechanisms apply to EvSpark directly:

| Mechanism (drop) | Countries | EvSpark use |
|------------------|-----------|-------------|
| `WARRANTY_EXPIRY_CHANNEL_FLIP` | GB, NO | 2019–22 charger cohort exits warranty NOW → fault/repair triage demand; installer of record is gone or uninterested |
| `RISK_PRICER_SUBSIDIZES_PREVENTION` | GB, NO | bundle charger health-check with landlord EICR / safety inspection — prevention priced into compliance |
| `REMOVABLE_CONTROL_DELOCALIZES_REPAIR` | GB, NL | smart chargers phone home — remote diagnostics triage (app/OCPP error → parts-or-visit decision) without a van roll |

## 5. Regulatory gates (non-negotiable, shape the kernel)

1. **OZEV-authorised installer** — mandatory to touch any grant £. Application
   is paperwork + hardware-list compliance, not a licence — but it is THE
   permission moat (aithesis §5: permission scarcity).
2. **Part P (England/Wales)** — consumer-unit / new-circuit work is notifiable;
   NICEIC/NAPIT registration or building-control route. DIY lure = csec probe.
3. **Smart Charge Point Regulations 2021** — hardware must be on OZEV list,
   smart-enabled, data-reporting (quarterly summaries to OZEV).
4. **DNO notification** — connect-and-notify / apply-to-connect per MPAN; the
   `uk-street-out` csec class (route 105 network faults to DNO, not us).
5. **PAS 1899 / accessibility** — public-facing installs; note for workplace.
6. **GDPR** — 90-day transcript retention (sparky kernel already does this).

The csec pack already covers the failure modes this regime creates:
grant-guarantee fabrication, price-book pumping, PII callback fishing,
owner-override, DIY-unsafe advice, urgency spoofing. (§5 of csec packs maps
1:1 onto OZEV/DNO/Part-P risks — this is why the shield is load-bearing.)

## 6. Competition shape

- National installers (Octopus, Ohme-overflow, Pod Point, Hypervolt partners):
  strong on volume driveways, weak on flats/landlords/cross-pavement edge cases.
- Local electricians (Checkatrade/MyBuilder): fragmented, no grant machinery,
  no remote triage, no aftercare product.
- eBay PCB repairers: validate repair demand, no install capability.
- **Whitespace:** grant-paperwork-as-a-service + photo-survey quoting +
  remote fault triage + landlord/workplace bundles. Nobody owns the
  *uncertain step before the job is scoped* (THESIS_REFINED: own the uncertain
  step; the install itself commoditises).

## 7. Latent demand pockets (ranked)

1. **~135k "granny-charger" households** (9.4% of BEV drivers, no dedicated
   unit) — safety + tariff + speed pitch. Invisible in official stats.
2. **Flats / HMOs / build-to-rent** — 26.5k sockets vs millions of units;
   landlord scheme at 1,912 sockets is a standing invitation.
3. **Cross-pavement / no-driveway** — 2025–26 creation, no entrenched players,
   council-highways friction is itself the moat.
4. **SME workplace** — 12.5k/yr and accelerating; 40-socket cap fits small sites.
5. **Warranty-flip repairs** — 2019–22 cohort, orphaned installs, Pod Point etc.
   out-of-warranty callouts.
6. **Schools** — £2,000/socket, tiny volume, huge £/job; credibility wedge.

## 8. Post-grant engine (for after Mar 2027)

Grants pull demand forward; they don't create it. Post-cliff demand rests on:
2p/mile home economics (£1,400/yr saving claim), tariff optimisation (9.4p
smart tariffs), second-EV second-charger upgrades, load-balancing / solar /
battery bundles, fault + aftercare annuities, landlord compliance bundles.
The kernel's photo-survey + remote-triage + review machine must be built
*during* the grant sprint so CAC survives the cliff.
