# ab — SPEC (generation pipeline v1)

## Inputs

A generation run takes:

```json
{
  "business_id": "ab-001",
  "idea": "UK EV charger installation + aftercare",
  "country": "GB",
  "track": "services",
  "intelligence": {
    "campaign_version_id": "sha256:… (drop campaigns/active/uk-ev-charger.md)",
    "evidence_snapshot_id": "sha256:…",
    "rubric_version_id": "sha256:… (HCC_V2)"
  }
}
```

Full field contract: `schemas/business.schema.v1.json`.
Run record contract: `schemas/generation-run.schema.v1.json`.

## Tracks

| Track | Shape | Example | Primary gate |
|-------|-------|---------|--------------|
| `d2c_parts` | specialist parts store (drop HCC A/B) | Allaway vacuums (FI) | HCC_V2 + 12 hard gates, G4 buyer autonomy |
| `services` | install / repair orchestration (drop HCC variant C) | **EvSpark (GB)** | demand proof + permission path + unit economics |
| `hybrid` | services now, parts later (or reverse) | EvSpark + PCB aftercare | both, staged |

**Track selection rule** (from THESIS_REFINED): if `CUSTOMER_PURCHASABLE_SHARE`
is low — technician procurement, regulated work, Part P / gas / DNO — the
business is `services`, not `d2c_parts`. EV charger replacement is the canonical
case: whole-unit replacement is near-zero self-service, so the kernel generates
an orchestration business with a parts-aftercare wedge, never a parts store.

## Stage procedures

### S1 — SCORE

1. Load campaign + evidence snapshot + rubric version (pin 3 IDs).
2. Run kill-check first (drop kill conditions; THESIS kill list).
3. Select track via `CUSTOMER_PURCHASABLE_SHARE` + self-service ratio table.
4. Breadup `evaluate()`: EV, ROIC, hold/ops cost, confidence tier.
5. Write `SCORED` worksheet or `KILLED` with reason.

Kill triggers: incumbent owns identity+compatibility+stock+checkout; Amazon/OEM
solves the decision; single fragile supply source; returns/support destroy CM;
required permission unobtainable (e.g. can't become OZEV-authorised and grants
are the demand engine).

### S2 — BRAND

1. Seed generation (industry keywords × shortness).
2. `name.search` batch (≥30 candidates, .com + .co.uk for GB).
3. `name.social` for shortlist (13 platforms; note the 5 manual-only).
4. Human picks brand. Record alternatives + why rejected.

### S3 — PROVISION (money gates)

1. `name.cf_purchase` with `confirmed:true` → registrar receipt.
2. `name.wire_email` with `confirmed:true` → zone id, catch-all proof.
3. Telnyx search + purchase with `confirmed:true` → number receipt.
4. Verify: inbox live (`email.inbox`), stats endpoint, test email round-trip.
5. Register free handles where automation exists (GitHub, npm, Bluesky…);
   queue manual ones with links (Instagram, Facebook, Reddit…).

### S4 — KERNEL

Generate `businesses/<id>/kernel.yaml` (voiceagent `BUSINESS_CONFIG` shape):

- `business/agent/voice` from identity + country locale.
- `nodes.services` from the job/failure taxonomy of the vertical.
- `nodes.policy` from regulatory requirements (grants, safety, certs).
- `nodes.escalation` from safety cases (sparks/burning/shock → wake human).
- `tradie` block: autonomy (start `semi_auto`, sends always need confirm),
  price book (published ranges only), service area, retention (GDPR).
- Smoke test: `/health` node count, `/chat` retrieval-only pass, TTS file.

### S5 — SHIELD

1. Run full csec pack against the staging kernel.
2. Required: exit 0, JSONL evidence committed to the business dir.
3. Any BREACH → fix kernel/prompt/policy → re-run. No waivers for
   safety/PII/impersonation classes. Waivers (explicit, reasoned) only for
   provably inapplicable probes.
4. Vertical extras: add probes for the vertical's specific lies (for EV-install:
   OZEV-grant guarantee, DNO misrouting, Part-P DIY lure, price-book pumping).

### S6 — STAGE

Dry run, no public surface:
1. Test email into the domain → classification → draft reply (never auto-send).
2. Test chat sessions (happy path + 3 edge cases from csec classes).
3. Unit economics sheet: CAC assumption, AOV, labour/parts, CM per job,
   break-even jobs/month.
4. Launch checklist: permissions (OZEV etc.), insurance, certs, phone, hours.

### S7 — LIVE (human gate)

`confirmed:true` + signed checklist → DNS/number go public, listings live.
Day-1 posture: `semi_auto`, capped ad/test budget, daily P&L review.

### S8 — OPERATE

Weekly: revenue, jobs, CM2, CAC, csec re-run on any kernel change, observation
log back to drop (new mechanisms, price points, failure modes). Monthly:
calibration review (predicted vs realised, Brier-style).

## Evidence rules

- Every stage output is a file under `businesses/<id>/`, referenced by digest
  in the run record.
- Money receipts (registrar, Telnyx, ad invoices) are stored verbatim.
- csec JSONL is committed, never summarised away.
- Killed runs keep everything plus `KILLED.md` (reason + what would un-kill).
