# ab — ROADMAP (build order for the controller itself)

## M0 — Spec (this repo, done 2026-09-10)

README, ARCHITECTURE, SPEC, AGENTS, schemas v1, UK_INSIGHTS, ab-001
(EvSpark PLAN + KERNEL + BUSINESS.json @ IDEA). No code, no infra.

## M1 — Read-only orchestrator (next, ~1 session)

A single CLI (`ab/run.py`, stdlib only) that:
- loads `businesses/*/BUSINESS.json`, validates against schemas (jsonschema or
  vendored check),
- prints stage status + next actions + exact commands (cmail curls, voiceagent
  run, csec run) for the operator to execute,
- writes run records (`schemas/generation-run.schema.v1.json`) from operator
  confirmations + pasted receipts.

No automation of money. No new services. The operator remains the actuator;
`ab` becomes the checklist with memory. Exit: ab-001 reaches SCORED with real
worksheets, or KILLED with cause.

## M2 — State store + receipts (after M1 proves the loop)

SQLite (`ab/state.db`, gitignored): runs, stage transitions, receipt digests.
`STATE` files remain the human-readable mirror. Adds `ab status` and
`ab next <id>` commands. Still operator-actuated.

## M3 — Ledger wiring (with first revenue)

Breadup `evaluate()` runs the S1 worksheet; weekly P&L appends to
`ECONOMICS.md`; observations sync to drop as dated notes. Calibration review
(predicted vs realised) monthly. Exit: one full quarter of ab-001 OPERATING
data or a documented KILL.

## M4 — Semi-autonomy (only after M3 + sustained csec green)

Pre-staged proposals (brand shortlists, kernel diffs, draft replies) generated
by the controller, executed by operator confirm. Money gates stay human
forever (README rule 1). Scheduler for freshness checks (grant-deadline watch,
price drift, csec re-runs on kernel change).

## Non-goals (all milestones)

Forking voiceagent, cmail, csec, or drop. A web dashboard before M3. Any token,
any fundraise mechanic, any multi-business parallelism before ab-001 resolves
(LIVE or KILLED) — one business wins first.
