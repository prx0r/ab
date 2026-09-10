# COMPETITION + PLAYBOOK — lead platforms & EV nationals

*Date: 2026-09-10. Web research + drop corpus. Prices are reported ranges.*

## 1. Lead platforms (the tradie side competes here)

| Platform | Model | Tradie cost | Vetting | Exclusivity | Scale |
|----------|-------|-------------|---------|-------------|-------|
| **Checkatrade** | subscription + leads | £30+VAT/mo floor (listing only); lead plans £100–500+/mo, 12-mo contract; ~£1–1.5k/yr typical post-Apr-2025-reset | strictest (12 checks) | ❌ shared (reportedly 10–20+ per enquiry) | 48k trades, 72 trades |
| **MyBuilder** | pay-per-shortlist | £2–35/lead, free to join, no subscription | ID + certs + skill checks | ❌ several per job | 228k trades, 2.5M reviews, ~100k jobs/mo |
| **Rated People** | sub + per-lead | monthly fee + lead cost, credit back | medium | ❌ up to 3 per lead | ~1M posts/yr |
| **Bark** | credits | ~£5–40/lead, credits expire in 3 mo (since Nov 2025) | light | ❌ up to 5 per lead | broad |
| **TradeMatch** (new) | pay-on-confirmed-work | commission on won work only | verified reviews, escrow | capped at 5 quotes | challenger |
| **Energy North / NI Trades** | free / flat local | £0–55/mo, no lock-in | local | capped at 3 | niche proof that flat-fair beats lock-in |

Benchmarks that matter: pay-per-lead £5–40 with **~1 job per 5–10 leads**;
Google Ads top-of-page click **£0.90–16.37** across top-10 trades (Local Ladder
Q3 2026 tracker). Subscriptions run £1.2–2k/yr on 12-month lock-in.

**Tradie pain (universal, in their own words):** pay-before-you-earn, fixed fee
in quiet months, renewal jumps (Checkatrade £870→£1,500/yr reports), shared
enquiries where slow reply = paid fee + lost job, shortlist fees owed even when
the job goes elsewhere, credits that expire.

## 2. EV nationals (the customer side competes here)

| Player | Offer | Price anchor | Network | Gap we exploit |
|--------|-------|--------------|---------|----------------|
| **Octopus** | charger + install + tariff + support, remote survey, 3-yr warranty, 7-day support, Electroverse, Fleet (Feb 2026) | bundled (tariff-led) | accredited Octopus installers | standard driveways only; edge cases fall out of remote survey |
| **Ohme** | Home Pro / ePod + install, 3–5 min commissioning, tariff integration | **£949–999 incl. standard install** | approved installers + CPD + marketing collateral | same: standard installs; custom = slow/expensive |
| **Pod Point** | home + fleet + subscription (upfront waived Mar 2026) | subscription-led | own + partners | subscription lock-in; repair-aftercare thin (hence eBay PCB repairers) |

Reading: nationals own the **standard driveway install at ~£950** with tariff
as the hook. Nobody owns flats, HMOs, landlords, cross-pavement, schools, or
post-warranty repair — the segments where the job is *scoping*, not fitting.
That is the whole game (THESIS_REFINED: own the uncertain step).

## 3. How we do it (the playbook)

```text
MAP (Places/Apify) → one cluster: few installers, weak ratings, driveways/flats mix
  → ADS (£10/day exact: "ev charger installer {town}", "ozev installer near me")
  → LANDING (photo-survey form: parking, consumer unit pic, tenure → grant pre-check)
  → QUALIFIED EXCLUSIVE LEAD (£15–40 all-in)
  → deliver via partner spark (subcontract, we hold customer + grant paperwork)
  → "we sent you N jobs this month" → ONBOARD (kernel on their number,
     diary, invoices, reviews, WhatsApp) → retainer £99–249/mo + 15–20%/job
  → cluster 2. Tradie-side CAC → ~£0 (leads are the acquisition).
```

Why the order works: buying demand first means every tradie conversation starts
with proof, not promises. Checkatrade charges before the first job; we arrive
with three. The kernel intake (photos + grant routing) is what makes our lead
worth £35–45 exclusive vs their £5–40 shared — qualification, not volume.

## 4. Positioning

**To tradies:** no 12-month contract, no pay-before-you-earn, exclusive
pre-qualified leads only, phone answered after hours, diary filled, grants
done, invoices chased, payouts on schedule. (Every clause is a Checkatrade
complaint inverted.)

**To customers:** local specialist, grant-maximised quote (£500 applied where
eligible), photo-survey firm pricing (no "from £949*"), 3-yr paperwork trail,
one throat to choke on aftercare. (Every clause is a national-player gap.)

## 5. What to steal from each

- Checkatrade Pay (1.29–1.79%) → our payout rail target rate.
- Rated People in-app invoicing → job-ledger invoice object (MIDDLEMAN_THESIS §6).
- MyBuilder shortlist → our qualification bar (pay only on shortlist ≈ our
  exclusive-handoff; keep the intent-correlation, drop the sharing).
- Octopus remote survey → our photo-survey intake (faster, grant-aware).
- Ohme installer network (training + collateral) → our onboarding kit.
- TradeMatch escrow + pay-on-win → Phase-5 trust product for big jobs.
- Local Ladder tracker → cite in tradie outreach ("the average electrician
  pays £X/job on [platform]; ours is exclusive at £Y").
