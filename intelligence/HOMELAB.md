# HOMELAB — sparkies first, agentic energy later (2026-09-10)

*Research: HA native MCP integration, homelab MCP ecosystem (all ≤5★,
fragmented, nobody owns it), homelab-power pain threads, MCP 2026-07-28
stateless spec. Decision recorded: trades separate, sparkies first.*

## Why sparkies first (three reasons)

1. **Biggest job surface.** EV + solar + battery + consumer units + faults +
   EICR all need sparks. One trade covers the whole electrification wave.
2. **Techy = cheapest onboarding.** They run Home Assistant, self-host, debug
   their own networks. Lowest support cost, fastest kernel feedback, natural
   evangelists. Plumbers later (bigger market, higher support cost).
3. **Permission moat.** Part P + NICEIC + OZEV + MCS keep the cowboys out and
   the willing buyer in. No other trade gates demand this hard.

Separate customer brands per trade (specialist positioning, drop-validated);
one tradie app (APP.md). No change to architecture — this is sequencing.

## Homelab owners are leads (the fishing pond)

The homelab crowd (r/homelab, HA forums, diysolarforum, self-hosted Discord)
constantly needs regulated sparky work they can't DIY:

- dedicated 32A circuits for racks, consumer-unit space + RCD protection
- whole-home UPS wiring / transfer switches (EcoFlow DELTA-class installs)
- solar + battery sized for uptime, earthing, surge protection
- network cabling + PoE (data sparky work, same visit)
- load monitoring (CT clamps, Harvi-style) for the energy dashboard

£500–5k jobs, techy customers who *love* an agent-driven experience
(photo survey, WhatsApp bot, live updates). Fish where the fish buy.

## Homelab MCP: the integration map (all early — good)

| Layer | State | Our play |
|-------|-------|----------|
| Home Assistant native MCP Server | ✅ SHIPPED (control devices from Claude Desktop) | kernel reads: battery SoC, solar yield, EV load, grid import |
| Community HA MCP (ha-mcp, robbrad) | early, fragmented | contribute/fallback, don't depend |
| Infra MCP (Proxmox, TrueNAS, Docker, OPNsense) | tiny (0–5★); TrueNAS official = research preview | tradie-offer later ("we watch your lab"); NOT phase 1 |
| MCP spec 2026-07-28 | stateless, no handshake — trivial to call | our kernel can adopt cheaply when ready |

Rules carried over: read-only defaults (truenas-mcp fail-closed is the
pattern), no control writes without human confirm (ab money-gate rule),
csec classes extend (a prompt-injected HA is a house fire — treat accordingly).

## The agentic-homelab endgame (Phase 5+, not now)

```text
customer HA (via MCP, read-only) ──▶ our kernel sees electron flow
  "battery hasn't charged in 3 days" / "EV pulling 7kW on peak tariff"
  ──▶ triage (remote fix? settings? visit?) ──▶ dispatch sparky
  ──▶ aftercare retainer: "we watch your electrons" £9–19/mo
```

Octopus owns tariff data; we'd own device truth. Fault detection +
dispatch + energy advice on one thread = the REMOVABLE_CONTROL_DELOCALIZES_REPAIR
mechanism as a product. Batteries doubling YoY with no aftercare owner
(UK_THESIS §1) is the wedge that funds it.

## Expansion order (binding)

EV installs → solar/battery → smart panels + load management → homelab
power/network circuits → agentic energy retainer. Each funds the next;
none starts before the previous cash-flows. Homelab *servicing* (managing
their Proxmox etc.) is explicitly out of scope until the energy retainer
lands — same demographic, different business, later.
