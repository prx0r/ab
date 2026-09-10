# LANDSCAPE — competitors, naming, and why it only looks easy

*Date: 2026-09-10. Web research + voiceagent spec audit.*

## 1. Naming decision

**EvSpark stays — as the consumer installer brand (ab-001), not the platform.**
`EvSpark Electrical / evspark.co.uk` is a good local-installer name: short,
trade-evocative, .co.uk. It was never meant to cover plumbing, and shouldn't.

The stack is the `ab` kernel. Each trade gets its own consumer brand compiled
from the same machine (one kernel YAML + one csec pack + one playbook each —
sparky + flowright already prove multi-tenancy). Platform nameless by design
for now; name it when tradie #5 asks "what is this thing."

## 2. Voiceagent spec audit (what "already specced" really covers)

| Claimed | Reality | File |
|---------|---------|------|
| Retrieval scoring | ✅ BUILT — TF-IDF + alias boost + 28% edge expansion, top-k with evidence | `app/graph.py:62-89` |
| Per-tenant feed ranking | ✅ PROVEN CONCEPT — flowright header: plumber affinities ≠ sparky affinities | `knowledge/flowright_plumbing_en.yaml:1-2` |
| Job affinity / preferences | ✅ BUILT — `job_affinity`, area, price book, autonomy levels | sparky + flowright `tradie:` blocks |
| Dispatch architecture | 📐 SPEC'D — Timefold, feasibility→cost→fairness, LLM never picks | `docs/REPO_COMPILATION.md:93-97` |
| Multi-agent receptionist | 📐 REFERENCED — LiveKit doheny-surf-desk pattern (Intake/Scheduler/Billing + Observer) | `REPO_COMPILATION.md:14-15` |
| Finance as typed tools | 📐 REFERENCED — paypal/agent-toolkit, stripe/ai, Temporal durability | `REPO_COMPILATION.md:63-87` |
| **Unified feed (calls+emails+WhatsApp+leads, ranked)** | ❌ MISSING — the actual "never worry about bs" pane does not exist | — |
| **Scheduling source-of-truth** | ❌ STUB — `tools/calendar.py` is 3 lines | `tools/calendar.py` |
| **Marketplace parsers** | ❌ MISSING — see MARKETPLACES.md | — |

Honest read: the *brain* is specced, the *pane of glass* is not. Nobody has
built the one feed. That's a real build item, not a polish item.

## 3. Competitor map (it's crowded — in one slice)

### UK AI receptionists for trades (the crowded slice)
Callio (£79.99/mo, 8-sec text-back), Onsite Digital (receptionist + booking
page + quote follow-ups + review agent + unified inbox — fullest UK stack),
Answrd (flat rate, photo-request links), Team-Connect (0800 numbers, emergency
routing), AIMEX (invoicing built in), Triple J, Clara (£69/mo), Moneypenny
(human+AI incumbent). Supportive AI is already writing EV-charger + Part P
SEO. **The answering slice is commoditizing toward ~£70/mo.**

### US FSM + AI (funded, not here yet)
Housecall Pro (200k pros, $147M, AI Accelerator), ServiceTitan ($9.5B, Atlas
AI sidekick), Jobber, **Probook ($40M a16z+Sequoia — "AI Operating System for
home services," dispatch-first, 2,542 jobs in month one at a 14-site operator)**,
My AI Front Desk / AgentZap (FSM plug-in recipes for Jobber/HCP/ServiceTitan —
our MARKETPLACES.md idea, already productized in the US), Vapi ($50M Series B).
Probook is the one to watch: dispatch-first + enterprise US. Nobody funded is
doing UK sole-trader EV-install depth.

### Lead platforms (structurally can't follow us here)
Checkatrade/MyBuilder/Rated People monetize *shared* lead volume. Instant
exclusive response cannibalizes their model — they'd have to sell fewer leads
per enquiry. Conflict of interest is a moat.

## 4. Why it looks easy (and where the real difficulty is)

It looks easy because the *demo* is easy: answer a call, book a slot. Eight UK
companies demo that. The difficulty — and the moat — is everything around it:

1. **Demand attached.** Every receptionist player waits for the phone to ring.
   We *make* it ring (ads → exclusive leads → grant-shaped segments). Nobody
   in the UK bundles generation + answering. This is the #1 differentiator.
2. **Money in the loop.** Invoicing exists (AIMEX, Rated People); *holding the
   transaction* (customer pays us → we split → tradie payout + float) barely
   exists at sole-trader level. That's the fintech wedge (§6 MIDDLEMAN_THESIS).
3. **Density, not spread.** Five tradies + 200 reviews in MK9 beats fifty
   tradies scattered nationally. Cluster density compounds (drive-times fall,
   reviews concentrate, word-of-mouth fires). Everyone else sells nationally.
4. **Vertical depth.** OZEV schemes, Part P scope, DNO routing, EICR bundling,
   cross-pavement councils — unsexy, regulated, local. Blog posts about it
   (Supportive AI) ≠ product that encodes it (sparky v2 kernel).
5. **The boring ops.** Onboarding labor, payout reliability, dispute handling,
   review velocity, churn. This is won in vans and inboxes, not demos.

Verdict: receptionist-alone is a race to £69/mo — do not compete there. The
winnable position is **demand + answering + money, dense in one cluster, deep
in one vertical**, then repeat the machine per trade. That's exactly STRATEGY.md;
the landscape confirms it rather than breaking it.
