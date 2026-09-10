# PLATFORM BRAND — selection log (evspark process)

*Method (from `cmail/a-logs/EVSPARK_BRAND.md`): seed → batch-check (.com via
`name.search`, .co.uk via `name.verify_domain` RDAP) → web-collision search →
socials (`name.social`, Apify-verified) → score → portfolio. Lesson added this
round: **always Google the name** — domain availability ≠ namespace availability.*

## Scoring (same as evspark)

Short + memorable + industry-relevant + .co.uk available + handles clean +
no live same-space collision. A live same-name UK competitor is an
instant kill regardless of domain status.

## Batch 1 — desk compounds (12)

graftdesk, sitedesk, jobsorted, vanoffice, tradestack, jobcatcher, firstcall,
diaryfull, graftly, siteoffice, everyjob, solidbook.

- `.com` available: **graftdesk, diaryfull** (graftdesk: full 15-TLD sweep).
- Rest taken on .com.

## Batch 2 — graft/office/sorted variants (10)

grafthq, graftos, graftkit, graftline, tooloffice, joboffice, besorted,
sortedit, weanswer, everycall. **0/10 on .com.** .com is gone for dictionary
compounds — .co.uk-first checking adopted from here.

## Batch 3 — coined UK slang (10, .co.uk via RDAP)

graftlane ✅, graftyard ❓, graftshed ✅, jobsdone ❌, dusted ❌, vanplan ❌,
daybook ❌, orderbook ❌, fullbook ❌, properjob ❌.

## Batch 4 — sound/straight/minder/gaffer/yard (10, .co.uk via RDAP)

soundjob ✅, soundtrade ✅, straightjob ✅, gafferdesk ✅, jobbook ❌,
runbook ❌, callminder ❌, jobminder ❌, gaffer ❌, yardbook ❌.

## KILLS (with reasons — do not revisit without new facts)

1. **graftdesk — KILLED 2026-09-10.** Clean .com sweep + near-clean socials
   (all Apify-verified available except Pinterest taken). Killed by collision:
   `graftdesk.co.uk` is LIVE — "GraftDesk Construction AI, AI Paperwork for UK
   Trades, Devon-based, RAMS/quotes/tenders/invoice chasing." Same country,
   same customer, same words. Namespace also crowded: `graft-ai.co.uk`
   (Torbay — "AI sidekick for self-employed tradespeople… admin side of being
   on the tools, handled" — our pitch verbatim) and `trygraft.app` (UK tradie
   jobs/tax/MTD app). Search + word-of-mouth confusion would be fatal in a
   trust business. Method note: this is why step 3 (web search) exists.
2. **graftlane / graftshed — KILLED (namespace).** Both .co.uk-available, both
   .com-taken, socials clean. Killed by the same Graft-cluster finding above:
   three live UK-trade-AI "Graft*" players (two in Devon). A fourth "Graft*"
   tradie brand is un-ownable in search and conversation.
3. **Batch 2/3/4 taken names** — dead on RDAP, no further work.

## DECISION (2026-09-10): sparkagent

**sparkagent.co.uk: AVAILABLE** (RDAP high-confidence, no DNS). sparkagent.com
taken (acceptable per evspark precedent — UK trust domain is .co.uk).

- Collision: PASS. No UK trades company; no .co.uk site. Nearest hits all
  distant: SparkPoint "SparkAgent" (PH crypto tooling), SPARK NEC / Sparky AI /
  SparkyPal / SparkShift (US NEC/IBEW apps), Mr Sparky (US franchise). Crowded
  "spark*" US namespace noted; zero UK collision.
- Socials (Apify-verified): npm/PyPI/crates/Bluesky/Telegram/GitLab/
  SoundCloud/Pinterest available. TAKEN: GitHub, YouTube, TikTok, X, Snapchat.
  MANUAL CHECK PENDING (most tradie-important): Facebook, Instagram
  (+ Reddit/Twitch/Threads). Fallbacks if taken: sparkagentuk, teamsparkagent.
- Name logic: spark (the trade's own word) + agent (what it is — their agent).
  Faces both sides: customers meet "the agent," sparkies get "their agent."
- STATUS: decided, NOT purchased. Buy gate: Facebook manual check
  (Instagram ✅ human-verified free as sparkagent.co.uk, 2026-09-10) +
  Companies House/IPO check + human `confirmed:true`. (~£10/yr + sparkagent.uk
  if free.)

## LIVE SHORTLIST (superseded by decision above — kept for record)

| Name | .co.uk | .com | Angle |
|------|--------|------|-------|
| soundjob | ✅ available | ❌ | "sound job" — solid work, well done |
| soundtrade | ✅ available | ❌ | "sound trader" — trustworthy tradesperson |
| straightjob | ✅ available | ❌ | straight = honest; "a straight job" |
| gafferdesk | ✅ available | ❌ | gaffer = the boss/foreman; office of the boss |

Next per process: web-collision search → socials → score → portfolio
(.co.uk primary + handles + Companies House/UK IPO check before any buy).
No purchase without human `confirmed:true` (ab README rule 1).
