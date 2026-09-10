# APP — one tradie app, per-trade customer brands (decision, 2026-09-10)

## Decision

**One standard tradie app.** Trade is a selector at onboarding (loads kernel
pack + price defaults + playbook), not a separate build. Multi-trade tradies
enable multiple packs in one feed.

**Customer-facing stays per-trade** (EvSpark for EV, separate brand per trade
later): customers buy specialists — drop validated this across all 5 countries
(`STATE_OF_BIGQUERY.md`: "specialist positioning works"). All brands drain
into the same tradie feed.

## Why (five reasons)

1. **Maintenance is survival.** One operator + agents. N apps = N update
   trains, store reviews, push certs, bug triages. One app is a constraint,
   not a preference.
2. **The architecture already decided.** One voiceagent runtime → N kernels.
   One cmail worker → N domains. One csec runner → N packs. The tradie pane
   follows the same pattern or the invariant (PLATFORM.md) breaks.
3. **Tradies multi-trade.** Sparky's affinity already spans EV + consumer unit
   + fault. Per-trade apps would fracture one user's day across logins.
4. **Cross-trade jobs are margin.** EV install + consumer unit; boiler + leak;
   landlord "send whoever." One feed bundles them; separate apps can't.
5. **One data flywheel.** Prices, response times, failure modes, reviews
   compound in one store — per-trade apps split the asset N ways.

## Non-decisions (solved inside one app)

- White-label feel → per-tenant theming (logo, colours, business name). Full
  white-label only if a tradie pays for it.
- Per-trade pricing → plan flags, not binaries.
- Blast radius → tenancy + csec per pack, not separate deployments.
- Discovery ("plumber app" search) → tradies buy via outreach/demo, never app
  search. Non-issue.
