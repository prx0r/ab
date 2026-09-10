# GOOGLE SETUP — APIs for the EvSpark lead→onboard→stack loop

*Date: 2026-09-10. Verified live where noted. Secrets stay in
`agent-vault --vault oracle`; this doc records STATUS, never values.*

## The loop these APIs serve

```text
PLACES (supply map) ──▶ pick postcode cluster (low density + high parking)
ADS (demand capture) ──▶ landing page → qualified lead (kernel intake)
   ──▶ "we have a lead for you" ──▶ tradie delivers, we observe
   ──▶ onboard: site + agent on their number + invoices + WhatsApp
   ──▶ retainer + per-job spread. Repeat per cluster.
```

## Status board (verified 2026-09-10)

| API | Vault | Live? | Blocker | Workflow use |
|-----|-------|-------|---------|--------------|
| Places API (New) | `GOOGLE_MAPS_API_KEY` ✅ | ❌ 403 | **billing off** | supply map: installers/postcode, ratings, phones, sites |
| Geocoding | same key ✅ | ❌ same | billing | postcode → lat/lng for the map |
| Routes / Distance Matrix | same key ✅ | ❌ same | billing | dispatch drive-time feasibility |
| Address Validation | same key ✅ | ❌ same | billing | job-intake address QA |
| Google Ads API | dev token ✅ + customer ID ✅ | ⚠️ test mode | **Standard access + refresh token missing** | Keyword Planner volume/CPC, campaign mgmt |
| Merchant Center | `MERCHANT_CENTER_ID` ✅ | n/a | — | NOT NEEDED (services track, no product feed) |
| Search Console API | site URL ❌ | ❌ | needs evspark.co.uk live + verified | organic tracking post-launch |
| Gmail API | address ✅ + OAuth ✅ | ✅ | — | tradie outreach mail-merge |
| Calendar API | OAuth ✅ | ✅ | per-user consent at onboard | booking adapter (alt: Cal.com) |
| Business Profile API | OAuth ✅ | ✅ | per-business OAuth at onboard | manage GBP for us + onboarded tradies |
| SerpApi | `SERPAPI_API_KEY` ✅ | ✅ | — | competition/pricing intel (1,047 credits, see `drop/docs/SERPAPI_GUIDE.md`) |
| Apify | `APIFY_TOKEN` ✅ | ✅ | — | `compass/crawler-google-places` bulk supply scrape; actors per APIFYALPHA |
| BigQuery | OAuth ✅ | ✅ | — | evidence lake (unchanged) |

**Root cause for all Maps failures:** `REQUEST_DENIED — You must enable Billing
on the Google Cloud Project.` One human action unlocks the entire left column:
console.cloud.google.com → Billing → link card (free tier + $200/mo Maps credit
covers our volumes many times over).

## Per-API setup (human vs agent)

### 1. Enable billing (HUMAN, 5 min, unlocks everything)
GCP console → Billing → enable on `project-ff2366d2-8fda-4fcb-9ba`. Then
APIs & Services → enable: Places API (New), Geocoding, Routes, Address
Validation. Restrict the key to those APIs + HTTP-referrer/IP locks after.

### 2. Places supply map (AGENT, ~$20–50 one-off per sweep)
`searchText`: `"EV charger installation {town}"` × 10 candidate towns →
name, rating, review count, phone, website, hours. Rank clusters by:
few installers + low ratings + high off-street housing. Store place_ids only
(ToS: cache IDs + your own notes, not reviews/photos). FieldMask minimal —
each SKU bills separately; displayName+address+rating+phone is the cheap set
(~$32/1k text searches; 10 towns × 20 results ≈ $7).

### 3. Bulk fallback that works TODAY (AGENT, no billing)
Apify `compass/crawler-google-places` (595k users): same towns, CSV out,
compute-cost only. Use for the first sweep now; switch to native Places when
billing lands (fresher data, ToS-clean).

### 4. Demand check (AGENT, SerpApi credits — do NOT burn on this yet)
SerpApi is for *product* competition, weak for local-services CPC. Instead:
HUMAN exports Keyword Planner manually (Tools → Planner → "ev charger
installation [town]" → volume + low/high bid) per `STATE_OF_BIGQUERY.md`
standing instruction. Costs £0, takes 10 min, unblocks the CAC sheet.

### 5. Ads API Standard access (HUMAN, 1–2 week wait)
Apply: Google Ads → Tools → API Center → Standard access (needs MCC history +
compliance). Then OAuth refresh token → vault (`GOOGLE_ADS_REFRESH_TOKEN`).
Until then: manual UI for campaigns + Planner; API for reporting later.

### 6. Tradie outreach (AGENT, live now)
Gmail API + Places/Apify phone+site list → personalised "we have leads in
{town}" sequence. Template + send-log in `businesses/ab-001/receipts/`.
Stay inside PECR: B2B outreach to published business addresses is fine;
track opt-outs from reply one.

### 7. Onboard-time APIs (per tradie, at Phase 3+)
Business Profile OAuth (manage their listing/reviews), Calendar OAuth
(availability feed for dispatch), WhatsApp Business API (**Meta, not Google**
— separate application via BSP; note as dependency for the WhatsApp manager).

## Lead economics (sanity check, verify in S6)

- Google Search CPC (home services, local exact): £2–5.
- Landing CVR (photo-survey form): 10–15% → **£15–40/qualified lead**.
- Installer close rate (exclusive warm transfer): 20–30%.
- Job contribution: ~£250 (grant) / ~£180 (non-grant).
- Lead value to installer at 25% close × £220 CM ≈ **£55** → charge £35–45
  or take 15–20% of job. Spread exists IF qualification is real — which is
  exactly what the kernel intake (photos, parking, grant pre-check) is for.
- Checkatrade anchor: £15–30/shared lead of dubious quality. We win on
  exclusivity + pre-qualification, not price.

## Compliance notes (UK)

- Call recording: announce + log consent (GDPR/PECR); retention 90d (kernel default).
- Lead selling: no licence needed; contracts define exclusivity + refund-on-duff-lead.
- Reviews: never gate/incentivise (CMA + GBP policy); ask every customer, same way.
- OZEV data reporting stays with the authorised installer of record (us or partner).

## Sequencing (no billing → billing)

1. NOW: Apify places sweep (10 towns) + manual Planner export + outreach list.
2. HUMAN: billing on → enable 4 Maps APIs → confirm with one searchText call.
3. AGENT: native Places re-sweep, cluster pick, landing copy per cluster.
4. HUMAN: £10/day exact-match test + Standard-access application.
5. Phase 3: first "we have a lead" calls with 3 real leads in hand.
