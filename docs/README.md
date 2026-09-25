# FORTREX — Project Knowledge Base

> **Any agent working on this repo must read this file first.** It explains every page, every system, every decision, and where the full documentation lives. Last updated: September 26, 2026.

## 1. What this project is (one paragraph)

FORTREX is a skill-based trading tournament brand. Traders keep their real capital at their own broker (read-only verification); FORTREX is the competition, leaderboard, and reward layer on top — never a broker, never custodial, never advice. The business goal is **the maximum number of members and traders**. Everything — pages, copy, design, automation — is one funnel:

```
SOCIAL POSTS → GENESIS WAITLIST (this site) → PLATFORM (VortexFX) → REVENUE (tickets, premium, broker IB)
```

## 2. Site map (this repo = the public flagship)

| Page | Role in funnel | Key systems |
|---|---|---|
| `index.html` | Capture: hero, live Genesis counter/ticker, doors countdown, three pillars, cap panel + live feed, registration modal, Genesis Pass + referral share | Live backend polling (60s), honeypot + submit-time bot defense, `?ref=` tracking |
| `tournaments.html` | Desire: the three arenas (Genesis Cup, weight-bracket leagues, funded finals), "Three steps to the arena" | Static concept, funnel CTA |
| `leaderboard.html` | Trust: "the board is dark" sealed state + live Genesis standings + verification pledge | Live backend polling, countdown |
| `faq.html` | Objection handling: non-custodial model, honest leaderboards, REX, cap, referrals, legality, launch date | Accordion FAQ |
| `legal.html` | Compliance: Terms, Privacy, Risk Disclosure (disclaimer patterns from legal research) | — |
| `docs/` | **This knowledge base** — all project logic for agents/humans | — |
| `assets/` | `fortrex-crown.png` (320px, ~113KB), `favicon.png` (64px) | — |

## 3. Backend contract (live, working — do not break)

Endpoints (Base44 serverless, owned by the founder's Superagent app `vesper-d5af3674`):

- `POST /functions/fortrexSaveWaitlistEntry` — body: `{ name, phone, email, country, honeypot, formTime, referredByCode }`. Success: `{ success:true, referralCode, position, memberNumber, message }`. Duplicates: `{ success:false, error:'already_registered', memberNumber, referralCode }`. Bot/honeypot submissions silently get fake success.
- `GET /functions/fortrexGetWaitlistCount` — `{ success, count, remaining (cap 10,000), recent:[{name, joinedDate}] }` (5 latest).
- `POST /functions/fortrexGetMemberStatus` — member lookup by referral code/email.

Data entity: `FortrexWaitlist` — fields: email, name, phone, country, referral_code, referred_by, position, invite_count, status ('genesis'), source, signup_date. Every record stores **source** (which page/form) and **referred_by** (whose referral code) for funnel analytics.

**Never point pages at the old arlo endpoints — that app is dead (org integration limit).**

## 4. Design system (the canon — exact values)

- Background: obsidian `#050506` + layered radial-gradient shell (`.fortrex-shell`, ends `#05050a`) + gold grid overlay (`.grid-noise`)
- Text: bone white `#FFF7E6` primary, muted gold `#A99B7A` secondary
- Accent: gold gradient `#F2D18A → #C9973E` for CTAs; `#D8A64D` for data numbers; hairlines `rgba(242,209,138,.16)`
- Type: Space Grotesk display (`.display`, tracking -.055em) · Inter body · JetBrains Mono numbers/labels (letter-spacing .2em+ uppercase)
- Surfaces: `.glass` cards, `.gold-border` emphasis, 1px gold hairlines — never neon, never glassmorphism cliché, one accent only
- Signature terms: "— LAUNCH / 001" eyebrows · "WHERE TRADERS RISE." · "JOIN THE GENESIS LIST" · "DOORS OPEN 11.07" · Genesis Pass FX-00000
- Motion: slow weighted eases (cubic-bezier .23,1,.32,1), respect `prefers-reduced-motion`, mobile-first, fast load

## 5. Brand voice (non-negotiable)

Quiet institutional confidence. Scarcity stated as fact, never begged ("10,000 seats. The gates weld shut at capacity."). Zero hype, zero profit promises, one exclamation maximum per page. Risk disclaimer ships on every money-adjacent surface. Full law: `docs/FORTREX-MASTER-SPEC.md` §1.

## 6. Admin & control (how the founder runs this)

- **Data control**: all waitlist records live in the `FortrexWaitlist` entity, managed via the Superagent (Vesper) entity tools or Base44 — search, edit, delete, segment by source/referrer/country.
- **Automation**: live counters, feeds, countdown run automatically; referral tracking is automatic. Next automation phase (welcome nurture, referral nudges, launch sequences) is mapped in `docs/research/06-automation-and-ops.md`.
- **There is intentionally NO public admin page on a static site** — admin control goes through the authenticated Superagent/Base44 layer. Never add an unauthenticated admin page here.
- **Full platform** (23 pages, trader accounts, tournaments, REX ledger, admin plane) lives in the private `VortexFX` repo and deploys on the founder's `koda` Base44 app once the plan limit clears.

## 7. Critical constraints (from legal research — see docs/research/04)

1. **Never promote offshore forex brokers (XM etc.) to Indian residents** — FEMA/RBI AVOID. India-facing product story = skill tournaments on the user's own account, no broker promotion.
2. REX = non-refundable utility points, no fiat cashout language, never sellable during Genesis.
3. No profit promises, no financial advice, risk disclaimer always. Geo-restrictions acknowledged in FAQ/legal.
4. NEEDS-LAWYER items before paid tickets go live in India (entity, state geo-blocking, TDS).

## 8. Roadmap (priority order)

1. ✅ Flagship redesign + legal + referral tracking + this knowledge base
2. Content engine: Phase II posts (starts Sep 28) — templates in `docs/research/03-visual-direction.md`
3. Domain: buy fortrex.io / fortrex.in, point at this site
4. Plan upgrade → koda/arlo revive → export old waitlist entries → merge
5. VortexFX platform deploy (merged per `docs/research/05-repo-audit-and-features.md` merge matrix)
6. Automation workflows (per `docs/research/06-automation-and-ops.md`)

## 9. Full documentation index

| File | Contents |
|---|---|
| `docs/FORTREX-MASTER-SPEC.md` | The master operating doc: ecosystem map, funnel, design language, backend canon, agent rules |
| `docs/research/01-competitor-teardown.md` | FTMO/TFT/Topstep/TradingView/India apps: hooks, pricing, failures, 10 exploitable gaps |
| `docs/research/02-psychology-and-presentation.md` | Conversion levers for traders, landing wireframe, post-signup flow, trust checklist |
| `docs/research/03-visual-direction.md` | Signature visual moments, motion spec, social post templates, performance rules |
| `docs/research/04-legal-and-business-setup.md` | Risk map (SAFE/GRAY/AVOID), disclaimer patterns, entity + payments, GST, IB compliance |
| `docs/research/05-repo-audit-and-features.md` | Page-by-page repo audit, feature merge matrix, ranked new features, admin console spec |
| `docs/research/06-automation-and-ops.md` | Growth automation map, founder dashboard spec, skills inventory, smart-work sequence to Nov 7 |

Ops/brand/content calendar also lives in the `fortrex-command-center` repo (brand-kit, content-system, launch phases).
