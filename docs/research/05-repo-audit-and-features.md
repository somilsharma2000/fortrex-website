# FORTREX Ecosystem — Feature & Quality Audit, Merge Matrix, and Roadmap

> **Audit Date:** September 25, 2026  
> **Target Scope:** 7 Repositories (`VortexFX`, `landingpage`, `fortrex-website`, `fortrex-arena`, `FORTREX`, `fortrex-command-center`, `fortrexfxmanusgold`)  
> **Master Reference:** `somilsharma2000_fortrex-command-center/FORTREX-MASTER-SPEC.md`

---

## Executive Alignment with `FORTREX-MASTER-SPEC.md`

1. **North Star & Funnel Direction:**  
   Every feature and page across all repositories must support the single overarching funnel:
   $$\text{Social Traffic} \longrightarrow \text{Genesis Waitlist Capture} \longrightarrow \text{Platform Activation (REX / Tournaments / Community)} \longrightarrow \text{Monetization (Broker IB + Tickets + Premium)}$$
2. **Brand Canon Enforcement:**  
   - Public Name: **FORTREX** (Internal repository names like `VortexFX`, `FORTEX-FX`, `Fortrex Arena` are strictly internal).
   - Taglines: *"Where Traders Rise"* (Brand) · *"Trade Real. Win Real."* (Product) · *"The Gates Are Opening"* (Stealth/Waitlist).
   - Voice: Institutional, minimal, quiet confidence. Scarcity is presented as absolute truth ("10,000 seats. The gates weld shut at capacity.").
3. **Non-Custodial Product Architecture:**  
   FORTREX operates as a gamified competition and analytics overlay above traders' external broker accounts (e.g., XM / MT4 / MT5). FORTREX never executes trades, holds client funds, or acts as a broker—eliminating regulatory friction.
4. **Visual Design Canon Tokens:**  
   - **Obsidian Background:** `#050506` | **Graphite Surface:** `#111114`  
   - **Bone White Text:** `#FFF7E6` | **Muted Gold Subtext:** `#A99B7A`  
   - **Fortrex Gold Accent:** `#D8A64D` | **Gold Bright Glow:** `#F4D28C` | **Gold Deep:** `#7D541D`  
   - **Market Semantics:** Verdant Profit `#15846E` | Destructive Red Loss `#DC2626`  
   - **Typography:** Space Grotesk (Headlines, -0.055em tracking), Inter (Body/UI), JetBrains Mono (Data/Badges).

---

## 1. Repo-by-Repo Feature & Quality Audit

### 1.1 `somilsharma2000_VortexFX` (The 23-Page Core Platform)
- **Role in Funnel:** The functional product core containing trader accounts, tournament execution, daily retention mechanics, REX currency, and administration.
- **Inventory of Pages & Features:**
  - `index.html`: Landing hero, registration teaser, live counter integration, feature highlights.
  - `signin.html` / `signout.html`: User authentication views (email/passcode & session termination).
  - `dashboard.html`: Trader dashboard with account balance (REX), tournament stats, active brackets, daily streak indicator, recent activity feeds.
  - `tournaments.html` / `contests.html`: Tournament arena catalog, weight-bracket filters (Micro, Feather, Welter, Heavy, Titan), prize pools, entry buttons.
  - `leaderboard.html` / `leaderboard-alt.html`: Global standings, rank changes, ROI %, trades count, REX earned, verified badge status.
  - `rex.html` / `offers.html`: REX Economy Hub, tier multipliers (1.25x - 2.0x), REX minting history, task claims, partner broker offers.
  - `checkin.html`: Daily check-in streak calendar (7-day compounding REX rewards: +10, +15, +20, +25, +30, +40, +50 REX + multiplier).
  - `invite.html`: Fleet Network referral dashboard, custom referral links, share buttons, tier progress bar, referred trader list.
  - `journal.html`: Community Trade Wall, trade sharing, screenshot attachments, verified ROI logs.
  - `community.html`: Citadel Discord/Telegram hub, signal channels, trader roles, leaderboard highlights.
  - `resources.html` / `tools.html`: Prop firm comparison sheets (FTMO, E8, FundedNext), lot-size & risk calculator tools.
  - `profile.html`: Trader avatar, country flag, XM account verification status, linked socials, win/loss stats.
  - `faq.html` / `terms.html` / `privacy.html`: Knowledge base, regulatory disclaimers, privacy policy, non-custodial disclosure.
  - `admin.html` + 6 Sub-Modules (`modules/`): Mission Control panel with passcode guard (`FORTREX-{somil-admin-2026}`).
    - `gate-control.html`: Genesis waitlist approvals, capacity control (10k cap), instant access keys.
    - `rex-treasury.html`: REX currency mint/burn, manual bonus grants, payout ledger.
    - `comms-hub.html`: Announcement broadcasts, Telegram/Discord webhook dispatchers.
    - `automation.html`: Rule-based trigger engine (e.g., Streak 7 -> Award Architect Badge).
    - `intelligence.html`: Analytics dashboard (waitlist sources, conversion funnel, REX velocity).
    - `audit-log.html`: System event log, admin action tracking, security events.
- **Backend Infrastructure:**
  - **20 Base44 Backend Functions:** `adminBanTrader.ts`, `adminCreateTournament.ts`, `adminTournamentControl.ts`, `adminUpdateSettings.ts`, `adminUpdateTrader.ts`, `adminVerifyTrader.ts`, `dailyCheckin.ts`, `discordAuth.ts`, `distributeRex.ts`, `getAdminData.ts`, `getPublicLeaderboard.ts`, `getPublicStats.ts`, `getPublicTournaments.ts`, `getTraderProfile.ts`, `getTraders.ts`, `joinWaitlist.ts`, `register.ts`, `sendEmail.ts`, `sendRex.ts`, `updateProfile.ts`.
  - **9 Base44 Entities:** `Trader.json`, `Tournament.json`, `Participant.json`, `Trade.json`, `CheckIn.json`, `Referral.json`, `TaskClaim.json`, `Transaction.json`, `PlatformSetting.json`.
- **Broken Bits & Flaws:**
  - Hardcoded admin passcode in client JavaScript (`admin.html:1086` -> `FORTREX-{somil-admin-2026}`).
  - Extensive fallback test data in `admin.html` (`FALLBACK_TOURNAMENTS`, `SAMPLE_GENESIS_TRADERS`, `SAMPLE_PARTICIPANTS`) used when Base44 API fails.
  - High count of dead link anchors (`href="#"` / `javascript:void(0)`) across internal navigation in sub-modules.
  - Backend currently blocked due to Base44 monthly organization integration limits (`koda` app returning rate-limit errors).
- **Genuinely GOOD Mechanics to Keep:**
  - Full daily check-in compounding streak system (`dailyCheckin.ts`).
  - Modular admin panel structure (`modules/` iframe/tab system).
  - REX economy logic (`sendRex.ts`, `distributeRex.ts`, tier multipliers).
  - Comprehensive entity schemas modeling the full tournament lifecycle.

---

### 1.2 `somilsharma2000_landingpage` (Genesis Waitlist)
- **Role in Funnel:** High-conversion TOFU/MOFU stealth waitlist landing page focused on scarcity and social virality.
- **Inventory of Features:**
  - 10,000-seat hard cap display with animated LED 7-segment digital counter (`segDisplay`).
  - Candlestick pattern background canvas, interactive wireframe globe, particle starfield, beveled crown logo animation.
  - Single-field email registration input with immediate Base44 API submission (`joinWaitlist` / `saveWaitlistEntry`).
  - **Vault Reveal Animation:** Upon signup, triggers gold confetti, particle explosions, vault door unlatching animation, revealing:
    - Unique Genesis Member Number (e.g., `#00042`).
    - "Architect" rank badge assignment.
    - Custom referral link generation with 1-click social sharing (X, WhatsApp, Telegram).
    - 1.25x REX Tier Multiplier hook for every referred friend.
- **Broken Bits & Flaws:**
  - Social icons in header/footer contain dead `href="#"` links (`navDiscord`, `vaultDiscordBtn`).
  - Social handles are unlinked or set to generic placeholders (`https://x.com/fortrex`).
- **Genuinely GOOD Mechanics to Keep:**
  - The entire post-signup Vault Reveal animation sequence (maximum dopamine conversion event).
  - LED 7-segment scarcity counter component.
  - Candlestick background canvas effect.

---

### 1.3 `somilsharma2000_fortrex-website` (International Waitlist Variant)
- **Role in Funnel:** Lead capture variant optimized for international user verification and social proof.
- **Inventory of Features:**
  - Multi-field waitlist form: Full Name, Phone Number (with international country code selector), Country, and Email.
  - **Live Signup Feed Ticker:** Real-time ticker showing simulated/actual recent signups (e.g., *"Ravi from India just claimed spot #8,492 · Confirmed"*).
  - Progress bar showing cap fill rate (e.g., `8,492 / 10,000 Seats Claimed`).
  - `tournaments.html`: Championship weight-bracket preview cards ($10k Featherweight to $250k Super Heavyweight).
  - `leaderboard.html`: Global leaderboard table preview with verified account filters.
  - `faq.html`: Categorized accordion FAQ (Broker rules, Non-custodial model, REX distribution).
- **Broken Bits & Flaws:**
  - Mock Genesis Pass card in `index.html` uses hardcoded inline CSS gradients and static sample names.
  - "Access Discord Hub" CTAs link to modal triggers (`onclick="openModal();return false;"`) rather than active Discord invites.
- **Genuinely GOOD Mechanics to Keep:**
  - Name/Phone/Country international form fields (critical for WhatsApp marketing & SMS verifications).
  - Live signup toast feed (high urgency/social proof).

---

### 1.4 `somilsharma2000_fortrex-arena` (Arena Concept Site)
- **Role in Funnel:** Educational product storytelling landing page explaining the non-custodial competition model.
- **Inventory of Features:**
  - Hero slogan: *"Trade Real. Win Real. The First Non-Custodial Forex Tournament Arena."*
  - "Three Steps to the Arena" onboarding story (1. Connect XM Account -> 2. Join Weight Class -> 3. Win Real Cash).
  - **Interactive Lot-Size & Risk Calculator:** Inputs for Account Capital ($), Risk %, Stop Loss (Pips), and Forex Pair -> outputs Exact Lot Size & Dollar Risk Amount.
  - "Earn Your Rex" currency breakdown (Volume rewards, streak bonuses, referral splits).
  - "Citadel Discord" community callout card.
- **Broken Bits & Flaws:**
  - Pure static HTML/JS without active backend API connections.
  - Anchor links (`#arenas`, `#calculator`, `#rex`) jump on-page but lack smooth scroll on some mobile browsers.
- **Genuinely GOOD Mechanics to Keep:**
  - Non-custodial explanation storytelling ("No trade execution, no custody = 100% legal clarity").
  - Client-side Lot Size & Risk Calculator (high organic utility and SEO magnet).

---

### 1.5 `somilsharma2000_FORTREX` (Next.js Tournament Showcase)
- **Role in Funnel:** Modern React/Next.js interactive showcase presenting tournament mechanics with high visual polish.
- **Inventory of Features:**
  - Developed using Next.js 14, Tailwind CSS, TypeScript, and Lucide React icons.
  - Hero headline: *"The Fortress of Trading Champions"*.
  - Dynamic Tournament Switcher: Interactive tab bar filtering weight brackets (Micro $1k, Feather $10k, Welter $50k, Heavy $100k, Titan $500k) with interactive modal details.
  - "The Fort Economy" showcase (Forts/REX earning & redemption mechanics).
  - Interactive Position Size & Leverage Calculator component in React.
  - Hall of Champions leaderboard table with trader avatars, profit metrics, and win-rate badges.
  - Live Market News ticker feed layout.
- **Broken Bits & Flaws:**
  - Entire application is currently frontend-only static components with hardcoded state (`app/page.tsx`).
  - Navigation links in header and footer point to empty anchors (`href="#"`).
- **Genuinely GOOD Mechanics to Keep:**
  - Clean React/Tailwind component architecture and stateful tournament bracket switcher.
  - Royal gold button styles (`btn-royal`) and glassmorphism cards (`glass-card`).

---

### 1.6 `somilsharma2000_fortrex-command-center` (Ops & Brand Canon)
- **Role in Funnel:** Internal operational hub, brand guideline repository, and marketing execution system.
- **Inventory of Features:**
  - `FORTREX-MASTER-SPEC.md`: The North Star spec document.
  - `brand-kit.html` & `brand-kit/`: Complete visual identity canon, color hex values, Space Grotesk typography guidelines, logo usage rules, and Instagram visual specs (`FORTREX_BASE44_INSTAGRAM_VISUAL_SPEC.md`).
  - `content-system/`: Launch countdown timeline (4 phases, doors open Nov 7, 2026), 4 content pillars (Alpha Trading, Scarcity & Proof, Citadel Culture, Platform Utility), hashtag banks, weekly social calendar.
  - `index.html` & `integrations.html`: Ops dashboard tracking Base44 Vesper/Koda status, Manus space links, and social channel status.
- **Broken Bits & Flaws:**
  - `analytics/README.md` is empty (placeholder only).
  - Static HTML files use hardcoded navigation links.
- **Genuinely GOOD Mechanics to Keep:**
  - Centralized single source of truth (`FORTREX-MASTER-SPEC.md`).
  - Content engine rules and social media automation specifications.

---

### 1.7 `somilsharma2000_fortrexfxmanusgold` (Flagship Brand Site)
- **Role in Funnel:** Production-grade full-stack web application hosted on Manus (`manus.space`) with obsidian-gold styling.
- **Inventory of Features:**
  - Built with React, TypeScript, Tailwind CSS, tRPC, Drizzle ORM, and MySQL backend (`drizzle/schema.ts`).
  - Production-grade Drizzle database schema defining 9 tables: `users`, `platform_settings`, `registrations`, `leaderboard_entries`, `analytics_events`, `rate_limit_buckets`, `security_events`, `admin_audit_logs`, `tournaments`.
  - Floating `AIChatBox.tsx` component providing real-time AI assistant interactions for visitors.
  - `ComponentShowcase.tsx`: Comprehensive UI component library (1,431 lines) testing all brand tokens, cards, modal dialogs, and form inputs.
  - Security suite: Built-in sliding window rate limiters (`rate_limit_buckets`) and security event logging (`security_events`).
- **Broken Bits & Flaws:**
  - Hosted on third-party Manus infrastructure (`fortrexfx-lwqfvhpi.manus.space`); needs full database and API migration to primary domain.
  - `Admin.tsx` page is minimal (70 lines) compared to the deep 6-module admin suite in `VortexFX`.
- **Genuinely GOOD Mechanics to Keep:**
  - Strict TypeScript Drizzle schema with audit logging and rate limiting.
  - Sleek obsidian-gold design tokens (`BrandTokens.tsx`) and `AIChatBox` component.

---

## 2. Cross-Repo Feature Merge Matrix

| Capability | Best Source Repo | Reason for Selection | Integration Strategy |
|---|---|---|---|
| **1. Visual Theme & Tokens** | `fortrexfxmanusgold` | Cleanest execution of `#050506` Obsidian & `#D8A64D` Fortrex Gold tokens with Tailwind system. | Adopt Tailwind config & `BrandTokens.tsx` as master CSS. |
| **2. Hero Section** | `FORTREX` + `landingpage` | Combines `FORTREX` "Fortress of Champions" title with `landingpage` candlestick background canvas. | Merge candlestick canvas behind Next.js/React Hero title & CTA. |
| **3. Waitlist Form** | `fortrex-website` | Includes Name, Phone (with country code selector), Country, and Email for international lead capture. | Use `fortrex-website` form layout backed by Base44 `joinWaitlist`. |
| **4. Scarcity & Counter** | `landingpage` | LED 7-segment digital counter displaying real-time 10,000-seat cap countdown. | Port `landingpage` 7-segment canvas component to main site. |
| **5. Post-Signup Virality** | `landingpage` | Vault reveal animation, confetti explosion, member `#00042` pass, and 1.25x REX share hook. | Trigger `landingpage` Vault modal upon successful registration submission. |
| **6. Live Social Feed** | `fortrex-website` | Real-time toaster feed showing live registrations ("Ravi claimed spot #8,492"). | Connect signup event stream to fixed bottom toast feed. |
| **7. Tournaments Showcase** | `VortexFX` + `FORTREX` | `FORTREX` interactive tab switcher UI + `VortexFX` backend entity model (`Tournament.json`). | Wire `FORTREX` tab UI to `getPublicTournaments` API endpoint. |
| **8. Leaderboard System** | `VortexFX` | Deep filtering (Weekly/Monthly/All-Time), verified XM badge status, ROI %, and REX totals. | Use `VortexFX` `getPublicLeaderboard` function to feed leaderboard tables. |
| **9. Daily Retention (Check-in)** | `VortexFX` | 7-day compounding streak calendar awarding scaling REX rewards and multipliers. | Embed `checkin.html` streak logic into user `/app` dashboard. |
| **10. Trading Calculators** | `fortrex-arena` | Exact lot-size, pip value, and dollar risk calculation formula based on account size & risk %. | Place interactive calculator on public `/tools` and dashboard. |
| **11. FAQ & Knowledge Base** | `fortrex-website` | Categorized accordion (Broker rules, Non-custodial model, REX, Security). | Render `fortrex-website` FAQ section on public `/faq`. |
| **12. Legal & Compliance** | `VortexFX` | Explicit non-custodial risk disclaimers, Terms of Service, and Privacy Policy. | Standardize `terms.html` & `privacy.html` across all platform footer links. |
| **13. Admin & Control Plane** | `VortexFX` + `manusgold` | `VortexFX` 6-module architecture (`modules/`) combined with `manusgold` Drizzle audit log schema. | Rebuild admin console as React SPA using `VortexFX` module layout. |

---

## 3. New Feature Opportunities & Gap Analysis

To become an industry-leading tournament platform, FORTREX must bridge specific gaps currently absent in all 7 repositories.

### Ranked Feature Roadmap (Impact vs. Effort)

```
HIGH IMPACT
   ▲
   │  [1] XM MT4/MT5 Broker Link       [3] Tournament Lobby States
   │  [2] Onboarding Quest             [6] Multichannel Alerts
   │
   │  [4] Read-Only Investor Sync       [5] Badges & Streaks
   │  [7] Anti-Sybil Fraud Radar
   └──────────────────────────────────────────────────────────►
   LOW EFFORT                                       HIGH EFFORT
```

### 3.1 Onboarding Quest & Trader Activation Flow
- **Impact:** HIGH | **Effort:** LOW
- **Concept:** A 4-step gamified onboarding progress bar on first login:
  1. *Complete Profile & Claim Handle* (+50 REX)
  2. *Connect XM MT4/MT5 Account Number* (+100 REX)
  3. *Join First Free Weight-Class Tournament* (+150 REX)
  4. *Share Referral Link on Telegram/X* (+200 REX + 1.25x Multiplier)
- **Value:** Instantly converts registered waitlist emails into active, connected platform traders.

### 3.2 XM MT4/MT5 Broker Verification & API Bridge
- **Impact:** HIGH | **Effort:** MEDIUM
- **Concept:** Automated verification modal where traders input their XM Trading Account ID and select server (e.g., `XMGlobal-Real 14`).
- **Mechanism:** The backend queries the XM Partner IB API or trade feed validator to verify account creation under FORTREX's IB link, automatically unlocking tournament entry.

### 3.3 Tournament Lobby Lifecycle States
- **Impact:** HIGH | **Effort:** MEDIUM
- **Concept:** Standardized 6-stage lifecycle for all tournaments:
  1. **Registration Open:** Traders lock in seats using REX or pass tickets.
  2. **Countdown (Lobby):** 24-hour pre-start phase displaying participant count and prize pool.
  3. **Live Competition:** Real-time leaderboard updates tracking verified trade ROI %.
  4. **Cool-down / Trade Lock:** No new trades counted; pending trades closing.
  5. **Audit Phase:** Fraud radar checks for hedging, latency arbitrage, or multi-account abuse.
  6. **Final Payout:** Automated REX/cash prize distribution to winner wallets.

### 3.4 Read-Only Portfolio Import & Investor Sync
- **Impact:** MEDIUM | **Effort:** HIGH
- **Concept:** Allow traders to submit MT4/MT5 read-only investor passwords or MetaStats/Myfxbook public API links.
- **Value:** Automatically syncs closed trade history, equity curves, win rate, and drawdown without manual trade posting in `journal.html`.

### 3.5 Achievement Badges & Win Streak Milestones
- **Impact:** MEDIUM | **Effort:** MEDIUM
- **Concept:** Visual NFT-style badges displayed on trader profiles:
  - *Apex Sniper:* 5 consecutive profitable trades.
  - *Titan Slayer:* Finished Top 3 in Heavyweight/Titan tournament.
  - *Centurion:* 100-day check-in streak.
  - *Fleet Commander:* Referred 50+ verified traders.

### 3.6 Multichannel Notification Engine
- **Impact:** HIGH | **Effort:** MEDIUM
- **Concept:** Unified notification hub alerting traders via In-App Toast, Email, Telegram Bot, and Discord webhook for:
  - Leaderboard rank displacement ("Trader @Alex overtook you for 2nd place!").
  - Tournament start/end reminders.
  - Daily check-in streak reset warnings.
  - REX referral payout confirmations.

### 3.7 Anti-Sybil Fraud Radar & IP Clustering
- **Impact:** HIGH | **Effort:** HIGH
- **Concept:** Automated admin intelligence tool scanning registrations for:
  - IP address overlap across multiple accounts.
  - Circular referral loops (User A refers User B refers User A).
  - Opposite-side trade hedging across two accounts in the same tournament.

---

## 4. Admin Console Specification ("Full Ops Control")

### 4.1 Existing Admin Capabilities (VortexFX & manusgold)
- **VortexFX `admin.html` + `modules/`:**
  - Basic passcode authentication (`FORTREX-{somil-admin-2026}`).
  - Manual creation of tournaments (`adminCreateTournament.ts`).
  - Trader banning and manual verification toggles (`adminBanTrader.ts`, `adminVerifyTrader.ts`).
  - Global platform setting updates (`adminUpdateSettings.ts`).
  - Basic gate control and 10k waitlist approval queue (`gate-control.html`).
- **manusgold Schema:**
  - Admin audit log database table (`admin_audit_logs`).
  - Rate limiting bucket monitor (`rate_limit_buckets`).

### 4.2 Target 'Full Ops Control' Architecture

The unified FORTREX Admin Console must combine the 6-module interface of `VortexFX` into a single-page React workspace with full read/write capabilities across all backend entities.

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ MISSION CONTROL OPS CONSOLE                                                            │
├───────────────┬────────────────────────────────────────────────────────────────────────┤
│ Navigation    │ Core Workspace Modules                                                 │
│               │                                                                        │
│ 🔍 Search     │ 1. USER & DOSSIER DIRECTORY                                            │
│ 📊 Analytics  │    - Real-time search by name, email, member #, XM account, IP         │
│ 🚪 Gate Keep  │    - Deep profile edit (REX balance, streak, ban state, verification)   │
│ 🏆 Arena Ops  │                                                                        │
│ 💰 Treasury   │ 2. DYNAMIC SEGMENTATION & BROADCAST                                    │
│ 📢 Comms Hub  │    - Filter cohorts (e.g., "India + XM Verified + REX > 500")           │
│ 🛡️ Fraud Radar│    - Multi-channel dispatch (Push, Email, Telegram, Discord)           │
│ 📜 Audit Trail│                                                                        │
│               │ 3. ARENA & TREASURY CONTROLLER                                         │
│               │    - Lifecycle control (Draft -> Live -> Audit -> Payout)               │
│               │    - One-click REX minting, clawbacks, and ticket refunds              │
│               │                                                                        │
│               │ 4. FRAUD RADAR & SECURITY                                              │
│               │    - Flagged IP clusters, duplicate wallets, suspicious trade timing   │
│               │                                                                        │
│               │ 5. IMMUTABLE SYSTEM AUDIT LOG                                          │
│               │    - Every admin action logged with timestamp, admin ID, and diff trail│
└───────────────┴────────────────────────────────────────────────────────────────────────┤
```

### 4.3 Functional Requirements for Full Ops Console

1. **Global Search & Deep Dossier Inspection:**
   - Universal search input indexing Email, Member ID (`#00042`), XM MT4/MT5 Account ID, IP Address, and Referral Code.
   - Dossier View: View trader's full history, connected accounts, referral tree, total REX earned/spent, trade journal entries, and IP logs.
2. **Cohort Segmenting & Automated Comms Dispatch:**
   - Filter traders by custom rules: `Country`, `XM Account Status` (Verified/Unverified), `REX Balance Range`, `Check-in Streak Length`, and `Tournament Participation`.
   - Send targeted bulk messages directly to selected segments via Email (`sendEmail.ts`), Telegram Bot, or Discord announcements.
3. **Financial Adjustments & Refund Engine:**
   - Ability to issue manual REX grants, penalize rule violators, or refund tournament entry tickets.
   - Payout approval queue requiring explicit admin sign-off prior to distributing prizes.
4. **Anti-Sybil Fraud Radar:**
   - Visual network graph displaying linked accounts sharing identical IP addresses, browser fingerprints, or referral chains.
   - One-click "Freeze Account & Freeze REX Balance" button.
5. **Immutable System Audit Trail:**
   - System automatically records every admin action into `admin_audit_logs` table (Admin User ID, Action Type, Target Entity, Previous State, New State, Timestamp, IP).

---

## Summary & Action Plan

1. **Unify Site & Funnel:** Consolidate all frontend repos into a single Next.js codebase adopting `manusgold` obsidian-gold design tokens, `FORTREX` showcase components, `landingpage` scarcity mechanics, and `fortrex-website` form fields.
2. **Unify Backend Infrastructure:** Restore Base44 platform API access and migrate `manusgold` Drizzle/tRPC schemas into the core Base44 application to support all 20 backend functions.
3. **Deploy Full Ops Console:** Build the 5-part Ops Console (User Search, Cohort Segmenting, Arena Controller, Fraud Radar, Audit Log) replacing legacy hardcoded passcodes with proper role-based authentication (`role: admin`).
