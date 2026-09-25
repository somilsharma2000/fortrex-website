# FORTREX MASTER SPEC — The One File That Runs Everything

> **Read this first.** This file is the single source of truth for the FORTREX brand, product ecosystem, growth funnel, and visual design language. Any agent (or human) working on ANY Fortrex repo must read this before building. Last updated: Sep 25, 2026.

---

## 0. North Star

**Goal: the highest possible number of clients and traders.** Everything we build is one funnel:

```
SOCIAL POSTS  →  LANDING (Genesis waitlist)  →  PLATFORM (tournaments, REX, community)  →  REVENUE (broker IB + tickets + premium)
```

Every page, post, and feature must move a person one step deeper. If a design or feature doesn't feed the funnel, it doesn't ship.

---

## 1. Brand Canon (rules that never change)

- **One name in public: FORTREX.** The codebase names FORTEX-FX, VortexFX, Fortrex Arena are internal repo names only. Never show them to users. One brand, everywhere, forever — split branding leaks funnel traffic.
- **Taglines (pick per context):** "Where Traders Rise" (brand) · "Trade Real. Win Real." (product) · "The Gates Are Opening" (stealth).
- **Voice: quiet confidence.** Institutional, minimal, certain. We never shout, never use hype-bro language, never more than one exclamation. Scarcity is stated as fact ("10,000 seats. The gates weld shut at capacity."), never begged.
- **Logo:** the beveled-gold crown (see `brand-kit/fortrex-crown.png` and `brand-kit/fortrex-logo-usage.md`). Obsidian background, gold mark, nothing else.

---

## 2. Ecosystem Map — every repo, what it's for, where it lives

| Repo | Role in funnel | Live link | Backend | Status |
|---|---|---|---|---|
| `landingpage` | **TOFU→MOFU: the Genesis waitlist** (10,000-seat cap, referral links, member portal, scarcity) | somilsharma2000.github.io/landingpage | Vesper Base44 functions (fixed Sep 25, 2026) | ✅ LIVE |
| `fortrex-website` | Older waitlist variant w/ name/phone/country + live signup feed, tournaments/FAQ pages | somilsharma2000.github.io/fortrex-website | Vesper Base44 functions (fixed Sep 25, 2026) | ✅ LIVE |
| `fortrex-landing` | First lead-capture page (Apps Script) — historical only | github.io | superseded | 🗄 Archive |
| `fortrexfxmanusgold` | **Flagship brand site** (obsidian + beveled gold, Genesis registration, profile, leaderboard, AI chat) | fortrexfx-lwqfvhpi.manus.space (full) · github.io mirror (UI-only) | Manus (tRPC + MySQL) | ⚠️ Alive but 3rd-party hosted |
| `VortexFX` (private) | **THE PLATFORM** — 23 pages: dashboard, tournaments, leaderboard, REX currency, daily check-in, invites, journal, community, admin | not deployed publicly | koda Base44 app | 🔴 Backend blocked (org integration limit) |
| `FORTREX` | Tournament showcase (Next.js): arenas, funded accounts, stats, royal gold buttons | not deployed | none (static) | 🧪 Concept |
| `fortrex-arena` | Arena concept: Live Arenas, "Earn Your Rex", Citadel Discord, lot-size calculator, FAQ | somilsharma2000.github.io/fortrex-arena | none (static) | ✅ Live (static) |
| `fortrex-command-center` | **Ops home**: brand kit, content system, launch plan, this file | github.io | none | ✅ Live |
| `fortrex-command-center` socials docs | Launch phases, pillars, hashtags, calendar | see `content-system/` | — | In use |

**Current blockers (fix these):**
1. Base44 org hit monthly integration limit → koda (platform API) + arlo (old waitlist) return "upgrade your plan" errors. Upgrade the Base44 plan or wait for reset.
2. Flagship's real backend lives on Manus hosting — not ours. Migrate when the platform goes live.
3. Old waitlist entries are stuck inside the arlo app until the limit clears — export then.

---

## 3. Feature Audit — what each repo does best (steal these for the master site)

**From `landingpage` (conversion psychology — the strongest):**
- 10,000-seat hard cap with live 7-segment counter and "seats remaining" ticker
- Referral system with per-member codes + share buttons (X / WhatsApp / Telegram)
- Genesis membership number (#00042), "Architect" titles, invite count
- 1.25x REX tier multiplier hook for referrals
- Vault reveal animation after signup (reward moment), confetti, gold particles, candlestick hero background

**From `fortrex-website` (international + social proof):**
- Name / phone / country form → international targeting from day one
- Live feed of recent signups ("Ravi just claimed a spot · Confirmed")
- Cap progress bar, urgency text, FAQ, tournaments + leaderboard pages

**From `VortexFX` (the product core):**
- Full trader platform: register, dashboard, tournaments, leaderboard, daily check-in streaks, REX currency (send/earn/distribute), referrals, journal, offers, tools, community, invites
- Admin plane: ban/verify traders, create + control tournaments, settings, audit
- Entities: Trader, Tournament, Participant, Trade, CheckIn, Referral, TaskClaim, Transaction, PlatformSetting
- 20 deployed function files (register, joinWaitlist, dailyCheckin, sendRex, distributeRex, admin*, getPublic*)

**From `fortrex-arena` + `FORTREX` (product story):**
- "Trade Real. Win Real." — traders keep capital at their own XM broker (MT4/MT5); FORTREX is the competition + reward layer. **No trade execution, no custody = no regulatory quicksand.**
- Live Arenas, weight-bracket tournaments, funded-account prizes, Forts/REX currency, "Three Steps to the Arena" onboarding story
- Lot Size Calculator (genuine trader utility = organic SEO/acquisition)
- "FORTREX Citadel" Discord + Telegram signal channels

**From `fortrex-command-center` (growth engine):**
- 4-phase launch plan (doors open Nov 7, 2026), content pillars, hashtag banks, weekly calendar, benchmarks, platform format templates

**Verdict — the winning formula:** flagship's premium obsidian-gold design + landingpage's scarcity mechanics + fortrex-website's international form and live feed + VortexFX's platform depth + arena's product story and calculators. That combination, consistently branded, is the master site.

---

## 4. The Funnel (stages, metrics, loops)

| Stage | Surface | Conversion event | Metric that matters |
|---|---|---|---|
| 1. Attention | Social posts (IG/X reels, quote cards, countdown markers) | Profile visit / link click | CTR per post |
| 2. Capture | Landing page | Email signup (Genesis list) | Visitor → signup % |
| 3. Activation | Welcome + referral tools | Referral link shared | Invites per member |
| 4. Commitment | Platform launch | Register + daily check-in | Signup → active trader |
| 5. Revenue | Tournaments, premium, broker (XM IB) | Ticket purchase / funded account / IB link | ARPU |

**Loops that compound (build these, protect these):**
- **Referral loop:** member number + architect title + 1.25x REX multiplier → every member becomes a marketer.
- **Scarcity loop:** 10k cap + live counter + "N seats left" → urgency without discounts.
- **Streak loop:** daily check-in with REX rewards → retention (VortexFX already has it).
- **Social-proof loop:** live signup feed + leaderboard screenshots → posts that market themselves.

**Tracking:** every signup stores `source` (which page) + `referred_by` (whose code). Weekly: top sources, top referrers, signup velocity. (Entity: `FortrexWaitlist` on the Vesper app, already populated with source/referred_by.)

---

## 5. The Perfect Website — canonical architecture

One canonical site when the platform launches (until then, the waitlist IS the site — that's the stealth phase working as designed). Merge as follows:

```
/                 Home — flagship hero (obsidian+gold crown), live seat counter,
                  "Three Steps to the Arena", CTA → /genesis
/genesis          Waitlist (landingpage mechanics + intl form + live feed)
/tournaments      Tournament cards, weight brackets, prize pools (arena + VortexFX)
/leaderboard      Public leaderboard (VortexFX getPublicLeaderboard)
/tools            Lot size + risk calculators (arena) — free value, SEO magnets
/community        Citadel Discord + Telegram + journal highlights
/app              The platform itself (VortexFX pages: dashboard, check-in, REX, invites)
/legal            Terms, Privacy, risk disclaimer (MANDATORY for anything trading)
/admin            Admin plane (never linked publicly)
```

**Rules:** mobile-first (70%+ of funnel traffic is phones), skeleton screens not spinners, every page ends in a CTA deeper into the funnel, `< 2s` load, single accent (gold) on near-black — restraint IS the luxury signal.

---

## 6. Visual Design Language (the canon — use for site AND social posts)

### Palette (harmonized from all repos; these exact values)
| Token | Hex | Use |
|---|---|---|
| Obsidian | `#050506` | Page background (near-black, never pure black) |
| Graphite | `#111114` | Elevated cards, panels |
| Bone White | `#FFF7E6` | Primary text (warm white, never #FFF) |
| Muted Gold | `#A99B7A` | Secondary text, captions |
| **Fortrex Gold** | `#D8A64D` | Primary accent, buttons, key numbers |
| Gold Bright | `#F4D28C` | Hover/glow, beveled edge highlight |
| Gold Deep | `#7D541D` | Shadows, pressed states |
| Verdant | `#15846E` | Profit / success ONLY (candles, wins, confirmations) |
| Destructive Red | `#DC2626` | Loss / error ONLY |
| Ice Blue | `#4C9FC1` | Occasional "reflection" accent (flagship detail) — sparing |

**Gold rule:** gold is the ONLY brand accent. Green/red are reserved for market semantics. Never rainbow.

### Typography
| Role | Font | Notes |
|---|---|---|
| Display / headlines | **Space Grotesk** | Tight tracking (-0.055em), bold; the flagship's `display` class |
| Body / UI | **Inter** | Weights 400–800 |
| Numbers / data / labels | **JetBrains Mono** (or ui-monospace) | Letter-spacing +0.2em uppercase for labels |

### Texture & motion
- Obsidian surfaces with faint beveled-gold edges (`1px` borders at ~16-22% gold opacity)
- Gold particles on interactive moments, liquid-gold sheen sweeps, crown material studies
- Candlestick motifs as background texture (landingpage hero)
- Motion: slow, weighted, cinematic. 500-800ms eases. Skeleton screens. Respect `prefers-reduced-motion`.
- Photography: dark environments, single warm key light, gold reflections. No stock-photo traders in suits.

### Social post templates (1080×1350 feed / 1080×1920 story)
1. **Quote card:** obsidian bg, crown small top-center, one line in Space Grotesk, gold underline. ("Discipline is the only edge that compounds.")
2. **Countdown marker:** giant mono numerals (5·4·3·2·1), gold on obsidian, nothing else.
3. **Leaderboard flex:** real screenshot of /leaderboard, gold-framed, "The board is live."
4. **Stat tile:** one number, gold, bone caption ("1,000 seats gone").
5. **Reel frame:** 15s candle animation + one sentence + crown watermark.
- Content pillars, hashtag banks, weekly calendar: see `content-system/*.md` — already written, follow them.

---

## 7. Backend Canon (where data lives today)

- **Live waitlist API (working):** `https://vesper-d5af3674.base44.app/functions/` → `fortrexSaveWaitlistEntry`, `fortrexGetWaitlistCount`, `fortrexGetMemberStatus`. Entity: `FortrexWaitlist` (email, name, phone, country, referral_code, referred_by, position, invite_count, status, source, signup_date). Drop-in shapes match both landing pages.
- **Platform API:** koda app (`koda-a0d26f88.base44.app`) — currently blocked by org integration limit; revives on plan upgrade, zero code changes.
- **Flagship API:** Manus tRPC (me, register, lookup, counter, leaderboard, track) — alive but 3rd-party; treat as disposable.
- **Migration path (post-upgrade):** port the 20 VortexFX functions to the revived koda app, point the master site at them, retire Manus.

---

## 8. For any agent working on Fortrex — operating rules

1. Read this file + `brand-kit/BRAND-KIT.md` before touching pixels or copy.
2. One brand name (FORTREX), this palette, these fonts — no new colors, no new vibes.
3. Every page/post must feed a funnel stage (Section 4). No orphan content.
4. Waitlist endpoints are the ones in Section 7 — never the arlo ones.
5. Anything trading-related ships with the risk disclaimer and legal pages. No profit promises, ever (see `LEGAL_STRATEGY.md` in VortexFX repo).
6. Don't break the stealth phase: until doors open, public posts reveal mechanics never. Mechanics live in the waitlist page only. (Phases: `content-system/launch-countdown.md`.)
7. Commit messages explain the funnel reason, not just the change.

## 9. Priority order right now

1. **Unblock revenue-critical infra:** upgrade Base44 plan → koda + arlo revive → export old waitlist entries → merge into `FortrexWaitlist`.
2. **Master site build** per Section 5 (start: `/genesis` + `/tournaments` + `/leaderboard` static pages on the flagship design system, backed by the live waitlist API).
3. **Content engine live:** Phase II "The Feeling" posts start Sep 28 per launch plan.
4. **Domain:** buy `fortrex.io` / `fortrex.in` — every shared referral link must carry the brand, not github.io.
5. **Platform deploy:** VortexFX on the revived backend, admin plane secured, then doors open.

---

## 10. Research Library (Sep 25-26, 2026 — six-track deep research)

All files in `research/`. Read the ones relevant to your task. Non-negotiable items are marked below.

| File | What it contains | Non-negotiable outcome |
|---|---|---|
| `research/01-competitor-teardown.md` | FTMO/TFT/Topstep/TradingView/TradingLeagues/TradeX/StockGro teardown: hooks, pricing, trust failures, visual identities; 10 exploitable gaps | We position as the "Sovereign Arena for Proven Skill" — non-custodial, the one thing no prop firm can honestly claim |
| `research/02-psychology-and-presentation.md` | Ranked hooks, landing wireframe (show/hide per stealth phase), post-signup 60 seconds, trust checklist, anti-patterns | Copy = institutional precision, zero hype; the vault/member-number/referral mechanics stay |
| `research/03-visual-direction.md` | 7 signature visual moments ranked by wow/effort (Vault Iris, Liquid Gold Volatility Ribbon, etc.), motion spec, social templates, performance rules | Gold-on-obsidian materialism, 1px gold hairlines, no neon, no glassmorphism clichés |
| `research/04-legal-and-business-setup.md` | Risk map (SAFE/GRAY/AVOID), disclaimer wording patterns, entity + payment rails, GST, IB compliance | **CRITICAL: never promote offshore forex brokers (XM etc.) to Indian residents — FEMA/RBI AVOID. India-facing product = NSE/BSE demo/virtual data only. Geo-block banned states. Global (non-IN) traffic may use offshore-broker model behind geo-fencing. REX must be non-refundable utility points, no fiat cashout.** |
| `research/05-repo-audit-and-features.md` | Page-by-page audit of all 7 repos, broken bits, feature merge matrix, ranked new features, admin console spec | Merge matrix is the build order for the master site |
| `research/06-automation-and-ops.md` | Growth automation map (6 modules), founder dashboard spec, skills/tools inventory, phased smart-work sequence to Nov 7 | Welcome/nurture, referral nudges, streak reminders, launch-day sequences run as Base44 workflows |
