# UK THESIS — demand × supply × gap (master synthesis, 2026-09-10)

*Sources: live BigQuery `drop.country_data` (GB 239 rows, 8-country lake of
1,661), GOV.UK EVCI/DESNZ/MCS releases, CITB Workforce Outlook 2026–30, ECA
Skills Index 2026, C&G+Shell programme, ab intelligence docs. Supersedes
nothing — it sits above UK_INSIGHTS + SUPPLY + MONEY as the cited record.*

## 1. Demand: the electrification wave, measured

| Segment | Stock | Flow | Price | Source |
|---------|-------|------|-------|--------|
| Home EV charging | 968k domestic CPs | +215k/yr, £892 mean | £892 (£526 w/ grant) | EV Cable Hub census 2026 |
| Heat pumps | record 60.5k MCS in 2025 | **−17% H1 2026** vs H1 2025; 75% BUS-funded | BUS £7.5k (oil/LPG £9k) | DESNZ Jun 2026, MCS |
| Solar PV | ~2M cumulative; record 267k in 2025 | 150k H1 2026 (+14%) | falling | MCS May 2026 |
| Batteries | small base | 36k H1 2026 (~2× YoY) | falling | MCS |
| Warm Homes Plan | 5M homes by 2030 target | social housing just starting (500 homes reported) | £15bn plan | DESNZ Mar/Jul 2026 |
| New builds | — | 28% of 2026 installs; 59% of new homes get solar | Future Homes Std coming | MCS |

Three structural reads:

1. **1-in-3 installs combine multiple technologies** (solar+battery+HP, MCS
   2026). The bundle is the job — single-trade thinking undersells every
   visit. This is the cross-trade app thesis with a government serial number.
2. **Heat pumps are policy-fragile; solar/batteries aren't.** HP −17% on BUS
   wobble; solar/batteries grow double-digits on economics alone. Lead with
   EV + solar/battery + aftercare; treat HP as controls/aftercare, not installs.
3. **Regional concentration is extreme.** HP: SE 18%, SW 14%, East 13%.
   Per-household leaders: Anglesey, Ceredigion, Gwynedd (Wales). Volume:
   Cornwall, Somerset, North Yorks. Cluster-picking is data, not guesswork —
   and our BigQuery already holds the hypothesis for it
   (H_GB_DAMP_GEO_RISK_V1: local-authority variation → concentrated demand
   where service density is weaker).

## 2. Supply: the workforce gap, measured

- 136k qualified electricians, **down 19.6% since 2018**; 12k/yr needed;
  apprentice starts **−5.5%**; **<1 in 5** classroom learners reach a job (ECA).
- All trades: **41,200 extra workers/yr** to 2030 (206k total); England needs
  14,940 skilled trades/yr; apprentice starts must ~triple (CITB Jun 2026).
- MCS heat-pump companies: 1,500 vs ~50k workers needed for targets.
- **No mandatory qualification for HP installers** beyond NVQ L2 (Sureserve
  evidence) → rogue-trader risk → certified quality is a sellable moat.
- CITB's own line: workers **less willing to travel** → strategies must be
  **place-based**. Our cluster doctrine, independently derived.
- State money: £600m construction training, Youth Guarantee, free Bootcamps,
  £950 EV unit AU0006, Shell co-funded 500 EV installers. Supply creation is
  a bought market (SUPPLY.md).

## 3. What our BigQuery already knows (and what it admits it doesn't)

GB lake state (live): 4 ecosystems (HOME_ENERGY, SOLAR_BATTERY, EV_AFTERMARKET,
OLD_HOME_DIAGNOSTICS), 5 scored markets, 5 falsified/falsifiable hypotheses,
12 problems, 5 quality-scored merchants, 94 observations, 62 sources.

- **The system falsifies:** plug-in solar killed (retailers entered instantly),
  Model Y accessories killed (Tessories owns it since 2019). Trust the kills.
- **The 12 GB problems ARE the service menu:** GB_HEAT_REPLACEMENT
  (replacement wave → warranty-flip), GB_HEAT_TOU (tariff advice Octopus won't
  give impartially), GB_EV_HOME_CHARGE (load management), GB_SOLAR_STORAGE /
  GB_SOLAR_MONITOR (the doubling battery base with no aftercare owner),
  GB_HOME_DAMP / HEATLOSS / RETROFIT (diagnostics).
- **Systematic missing (every GB market):** `keyword_planner_measured: false`,
  `cpc_measured: false`, `landed_cost_verified: false`,
  `positive_pre_ad_contribution: false`. The lake is rich in structure, empty
  in economics. **Phase 0 exists to flip exactly these four gates** — manual
  Planner export + 10 supplier/installer calls. No new infra needed.
- Lake tripled since March (1,661 rows, CH+SE added). The intelligence machine
  works; the economics machine is us.

## 4. The gap math (one cluster)

Take a 25km cluster (~300k households): ~2–3k new EVs/yr → ~1.5k charger jobs
at ~£892 = **~£1.3M/yr local install value**. Five decent sparkies doing 2
EV jobs/week each clear the cluster with room for faults, EICR bundles,
landlord stock, and battery retrofits on top. Place-based supply (CITB) +
concentrated demand (DESNZ/MCS regions) + 5 tradies on our stack = a local
monopoly on responsiveness. Then copy the cluster.

## 5. Plan deltas from this research (binding)

1. **Lead with EV + solar/battery, not heat pumps.** HP installs are
   BUS-hostage; HP aftercare/controls later. (Amends PLAN.md phasing.)
2. **Battery aftercare is ab-002-shaped already:** 36k H1 installs doubling,
   zero aftercare owner in our merchant census. Solar monitoring
   (GB_SOLAR_MONITOR) is the same shape.
3. **Warm Homes social housing = landlord thesis at scale.** Councils/HAs
   buying retrofit by the hundred — one sale, many jobs, MCS paperwork
   included. Add to Phase 4 targeting.
4. **New-build electricians are a supply seam:** 59% of new homes get solar;
   site sparks meet every buyer at handover. Recruit there.
5. **Rogue-trader risk is marketing:** no mandatory HP qual + our certified,
   reviewed, supervised supply = "the safe pair of hands" positioning.
6. **Measure the four false gates first.** Everything downstream (ads, onboard
   pitch, pricing) depends on Planner + supplier + contribution truth.
