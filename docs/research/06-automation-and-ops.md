# FORTREX Automation, Growth-Ops & Smart-Work Research
**Document Reference:** `06-automation-and-ops.md`  
**Brand:** FORTREX ("Where Traders Rise" / "Trade Real. Win Real.")  
**Launch Target:** November 7, 2026 (Genesis Waitlist Cap: 10,000 Seats)  
**Execution Context:** Solo Founder (Somil Sharma) + Agency (Beyond Pixells) + AI Superagent (Vesper on Base44)

---

## Executive Summary

FORTREX is entering its stealth growth and launch execution phase leading up to November 7, 2026. Operating as a lean startup with a solo founder and agency support requires extreme leverage. By combining **Base44 serverless backend functions**, **Base44 CNCF v1.0 automated workflows**, and **Vesper (Base44 AI Superagent)**, FORTREX can automate 85%+ of growth operations, community management, and launch sequences without introducing unsustainable operational overhead.

This document presents the complete growth-ops architecture:
1. **Growth Automation Map**: Comprehensive inventory of triggers, channels, effort levels, and stack feasibility.
2. **Analytics & Control Spec**: Minimal telemetry event spec, viral equations, and single-pane founder dashboard.
3. **Tools & Skills Inventory**: Clear division of responsibilities between AI Agents, Founder, Agency, and paid toolstack.
4. **Smart-Work Sequence to Nov 7**: Prioritized, phased execution plan balancing manual high-touch tactics (<1,000 users) with automated scale (>1,000 users).

---

## 1. Growth Automation Map

The FORTREX growth funnel spans 6 key automation modules across pre-launch, viral acquisition, and launch-day conversion. All workflows utilize the existing `FortrexWaitlist`, `Trader`, `Tournament`, `Participant`, `CheckIn`, and `Referral` entity schemas.

### 1.1 Funnel Automation Matrix

| Funnel Stage / Use Case | Trigger | Primary & Secondary Channels | Setup Effort | Stack Compatibility & Dependencies | Automation Status |
|---|---|---|---|---|---|
| **1. Waitlist Welcome & Nurture** | `FortrexWaitlist` record created (`entity.create`) | Email (Transactional), WhatsApp (Direct/Group) | **Medium** | **Base44 Workflow + Deno Function** (`sendEmail.ts`). *Dependency: Transactional Email API Key (Resend/SendGrid) required.* | 🟡 Ready for API Key |
| **2. Referral Nudges & Milestones** | `invite_count` updated OR Scheduled CRON (72h inactive) | Email, Member Portal Toast, WhatsApp | **Low-Medium** | **Base44 Scheduled Workflow** + `FortrexWaitlist` lookup. Bumps waitlist `position` dynamically. | 🟢 Native Stack Compatible |
| **3. Streak & Daily Check-in Reminders** | Scheduled CRON Daily at 18:00 UTC | WhatsApp, Discord Webhook, Push/Email | **Medium** | **Base44 Workflows** querying `CheckIn` entity vs active waitlist/traders. | 🟢 Native Stack Compatible |
| **4. Launch-Day Sequences (Nov 7)** | Scheduled Time Trigger (Nov 7, 00:00 UTC) Staggered Waves | Email Broadcast, WhatsApp Broadcast, Discord `#announcements`, X | **High** | **Base44 Staggered Workflow** + Vesper multi-channel publishing. | 🟢 Native Stack Compatible |
| **5. Leaderboard Digest Posts** | Scheduled CRON Weekly (Fridays 16:00 UTC) | Instagram, X, Discord, LinkedIn, GitHub Repo | **Low** | **Vesper Superagent Autonomous Skill**. Reads `LeaderboardEntry` / `Participant`, formats visual summary, posts to channels. | 🟢 Fully Native |
| **6. Abandoned-Signup Recovery** | Frontend Form Heartbeat / Partial Submit Exit (2h decay) | Email Follow-up, Browser LocalStorage Recovery | **Low** | **Base44 Deno Function** (`recordAbandonedDraft`) with 24-hour delayed trigger. | 🟢 Native Stack Compatible |

---

### 1.2 Detailed Module Specifications

#### Module 1: Waitlist Welcome & Nurture
* **Objective**: Instant confirmation, position assignment, and viral referral link delivery.
* **Workflow Logic**:
  1. Trigger: `FortrexWaitlist` `entity.create` fires upon submission to `landingpage` or `fortrex-website`.
  2. Action 1: Assign unique `referral_code` (e.g., `FX9K2A1B`) and calculate initial `position` (e.g., Member #1,420 of 10,000).
  3. Action 2: Trigger Base44 backend function `sendWaitlistWelcome`.
  4. Payload: HTML/Text email with personalized referral link (`somilsharma2000.github.io/landingpage?ref=FX9K2A1B`), position badge, and WhatsApp VIP channel invite.
  5. *Stack Reality*: Native Base44 workflow execution is complete. Connecting Resend/SendGrid API key in environment variables enables instant delivery.

#### Module 2: Referral Nudges & Milestone Alerts
* **Objective**: Turn waitlist members into distribution nodes using gamified position skipping.
* **Workflow Logic**:
  1. Trigger A (Event-Driven): `FortrexWaitlist.invite_count` increments when a referee completes registration.
     * Action: Recalculate `position` (`position = max(1, position - 25)` per referral). Send instant "Position Bumped!" email/WhatsApp message.
  2. Trigger B (Scheduled Nudge): CRON runs every 3 days for members with `invite_count == 0`.
     * Action: Send personalized nudge: *"You are currently #3,410 in line. Share your code with 2 trading peers to leap into the Top 1,000 before Nov 7."*

#### Module 3: Streak & Daily Check-in Reminders
* **Objective**: Maintain high engagement and build daily habits before platform launch via REX reward distribution.
* **Workflow Logic**:
  1. Trigger: Scheduled CRON daily at 18:00 UTC.
  2. Query: Compare active `FortrexWaitlist` or `Trader` IDs against `CheckIn` entity records for the last 24 hours.
  3. Action: Send automated reminder via WhatsApp connector or Discord webhook: *"Your 5-day streak is about to expire! Claim today's +50 REX before midnight UTC."*

#### Module 4: Launch-Day Sequences (Nov 7 "Doors Open")
* **Objective**: Zero-downtime, staggered rollout to avoid server congestion and create intense opening-day energy.
* **Workflow Logic**:
  1. T-24 Hours (Nov 6): Final readiness check, automated database backup, lock waitlist order.
  2. T-0 (Nov 7, 00:00 UTC - Wave 1): Email & WhatsApp broadcast to Top 1,000 members (`position <= 1000`) with direct platform access pass.
  3. T+2 Hours (Wave 2): Email broadcast to Positions 1001–5000.
  4. T+4 Hours (Wave 3): General broadcast to remaining waitlist + global social announcements across X, Discord, and Instagram.

#### Module 5: Leaderboard Digest Posts
* **Objective**: Showcase social proof, top referral advocate standings, and trading tournament benchmarks.
* **Workflow Logic**:
  1. Trigger: Friday 16:00 UTC CRON.
  2. Action: Vesper Superagent executes `getPublicLeaderboard` function.
  3. Aggregation: Extract Top 5 referrers and top arena traders, format brand-compliant copy ("The Kings of the Arena - Week 42").
  4. Execution: Post across connected channels (Instagram, X, LinkedIn, Discord) and update `analytics/` folder in `fortrex-command-center`.

#### Module 6: Abandoned-Signup Recovery
* **Objective**: Re-engage users who entered email/phone on `fortrex-website` but failed to complete registration.
* **Workflow Logic**:
  1. Trigger: Frontend JS fires `saveDraft` payload when email field passes validation but form is not submitted within 120 seconds.
  2. Wait State: 2-hour delay buffer in Base44 workflow.
  3. Check: If no matching `FortrexWaitlist` record created, send lightweight recovery email: *"Your Genesis seat at FORTREX is reserved for 24 hours. Complete your registration to lock your position."*

---

## 2. Analytics & Control Spec

A solo founder cannot monitor dozens of scattered tools. This spec defines the **minimal telemetry event model**, **key operational equations**, and a **single-pane control dashboard**.

### 2.1 Telemetry Event Schema

```json
{
  "event_name": "waitlist_signup_completed",
  "timestamp": "2026-09-25T22:54:00Z",
  "user_id": "usr_99218a",
  "properties": {
    "email": "trader@example.com",
    "source": "fortrex-website",
    "referral_code_used": "FX3K8P",
    "form_completion_time_sec": 14,
    "position": 1842,
    "country": "IN",
    "has_phone": true
  }
}
```

#### Core Telemetry Events List:
1. `waitlist_signup_completed`: Fired upon successful `FortrexWaitlist` creation.
2. `referral_link_generated_and_shared`: Fired when a member copies/shares their invite URL.
3. `referral_conversion_achieved`: Fired when a referee completes registration using a member's code.
4. `member_portal_authenticated`: Fired when a user checks status on `landingpage` member portal.
5. `daily_checkin_completed`: Fired when user claims daily REX in `CheckIn`.
6. `abandoned_form_detected`: Fired when user leaves uncompleted signup form.
7. `system_health_heartbeat`: Hourly telemetry monitoring Base44 rate limits and database latency.

---

### 2.2 Key Operational Metrics & Equations

#### 1. Signup Velocity ($S_v$) & Cap Trajectory ($T_{cap}$)
* **Daily Velocity ($S_d$)**: $S_d = \text{Total Signups Today}$
* **Hourly Rate ($S_h$)**: $S_h = \frac{S_d}{24}$
* **Days to 10,000 Cap ($T_{cap}$)**:
  $$T_{cap} = \frac{10000 - S_{\text{current}}}{S_d}$$
  *Target*: $T_{cap} \le \text{Days remaining to Nov 7}$ (42 days as of late September 2026 $\rightarrow$ Target $S_d \ge 238$ signups/day).

#### 2. Viral Coefficient ($K$-Factor)
$$K = i \times c$$
* Where $i$ = Average number of invite links shared per waitlist member.
* Where $c$ = Conversion rate of referees clicking the link and registering.
* *Benchmark*: $K \ge 1.2$ indicates exponential self-sustaining growth; $K < 0.5$ requires paid/organic top-of-funnel injection.

#### 3. Churn & Friction Indicators
* **Email Bounce/Unverified Rate**: $\frac{\text{Bounced/Invalid Emails}}{\text{Total Registrations}} \times 100\%$ (Target $< 3\%$).
* **Form Abandonment Rate**: $\frac{\text{Abandoned Form Events}}{\text{Total Form Interactions}} \times 100\%$ (Target $< 25\%$).
* **Stale Waitlist Index**: Percentage of waitlist members with 0 portal logins in 14+ days.

#### 4. System Launch-Readiness Metrics
* **Base44 API Quota Utilization**: $\frac{\text{Monthly API Requests Used}}{\text{Base44 Plan Quota Cap}} \times 100\%$ (Alert trigger at $80\%$).
* **Database Query Latency**: Average response time for `joinWaitlist` and `getMemberStatus` functions (Target $< 350\text{ms}$).
* **WhatsApp / Discord Conversion Ratio**: $\frac{\text{Community Group Members}}{\text{Waitlist Registrations}} \times 100\%$ (Target $\ge 30\%$).

---

### 2.3 Single-Pane Founder Dashboard Layout Spec

The dashboard lives on `somilsharma2000_fortrex-command-center` or within the `admin.html` plane of `VortexFX`.

```
+-----------------------------------------------------------------------------------+
|  FORTREX COMMAND CENTER -- LAUNCH CONTROL (NOV 7 COUNTDOWN: T-42 DAYS)            |
+-----------------------------------------------------------------------------------+
| [WIDGET 1: SEAT CAP SPEEDOMETER]                                                  |
| Total Signups: 3,420 / 10,000 Seats (34.2%) | Daily Velocity: +310/day           |
| Estimated Cap Hit Date: October 18, 2026 (19 Days Ahead of Schedule)              |
+-----------------------------------------------------------------------------------+
| [WIDGET 2: VIRAL ENGINE (K-FACTOR)]          | [WIDGET 3: CHANNEL SOURCE MATRIX]  |
| K-Factor: 1.34 (VIRAL BOOST ACTIVE)          | Landingpage: 48% (1,641)           |
| Total Referrals Generated: 1,420             | Fortrex-Website: 28% (957)         |
| Top Referrer: FX_KING_99 (42 Invites)       | Direct Referral: 24% (822)         |
+----------------------------------------------+------------------------------------+
| [WIDGET 4: FRICTION & CHURN MONITOR]         | [WIDGET 5: LAUNCH READINESS GAUGE] |
| Email Bounce Rate: 1.8% (HEALTHY)            | Base44 API Quota: 42% Used (OK)    |
| Unverified Members: 112                      | Resend Email Status: CONNECTED     |
| Form Abandonment (24h): 14                   | VIP WhatsApp Group: 1,120 Members  |
+-----------------------------------------------------------------------------------+
```

---

## 3. Tools & Skills Inventory

To maximize leverage, tasks are categorized by **AI Agent Ownership** vs. **Human (Founder / Agency) Ownership**, along with necessary paid tool integrations.

| Workstream | AI Agent Owned (Vesper & Sub-Agents) | Human / Founder / Agency Owned | Required Paid Tools & API Stack |
|---|---|---|---|
| **Design & Branding** | • Generating social post graphics (DALL-E 3 / Flux)<br>• Formatting UI themes (CSS token maintenance)<br>• Resizing banner assets | • Core brand direction & crown emblem design<br>• High-fidelity Figma master designs<br>• Final asset visual sign-off (Beyond Pixells) | • Midjourney / Flux API ($20/mo)<br>• Figma Professional ($15/mo) |
| **Frontend Development** | • GitHub Pages HTML/JS bug fixes<br>• Landing page component updates<br>• Responsive styling adjustments | • Complex React component architecture (`FORTREX` repo)<br>• Core UX page flow review<br>• Cross-browser QA | • GitHub (Free)<br>• Vercel/GitHub Pages (Free) |
| **Backend & Infrastructure** | • Writing Base44 Deno serverless functions<br>• Authoring CNCF v1.0 workflow JSON/YAML<br>• Database schema migration scripts | • Architecture review & security audits<br>• Upgrading platform plans & API keys<br>• Financial/payment ledger integrations | • Base44 Pro Tier Plan ($20–$50/mo)<br>• Resend / SendGrid API ($20/mo) |
| **Legal & Compliance** | • First-draft Terms of Service & Privacy Policy<br>• Regulatory disclaimer copy per region<br>• Contest rule template generation | • Regulatory legal review (Prop firm / CFD rules)<br>• Final contract execution with brokers/IBs<br>• Corporate entity setup & compliance | • Specialized Legal Counsel (As needed) |
| **Content & Copywriting** | • Weekly social media content batching<br>• Email nurture copy variants<br>• Hashtag banking & caption generation | • Brand voice alignment & tone tuning<br>• High-stakes founder launch announcements<br>• Video script final review | • OpenAI / Anthropic API (Vesper core)<br>• Sub-agent executor |
| **Paid Advertising** | • Ad copy generation & variant testing<br>• UTM tracking code builder<br>• Weekly ad performance summary parsing | • Ad budget allocation & strategy ($500–$2k)<br>• Meta / Google / TikTok Ad Account setup<br>• Target audience definition | • Meta Ads / Google Ads budget<br>• TikTok Ads Manager |
| **Community Ops** | • 24/7 Discord & WhatsApp automated Q&A<br>• Daily streak & REX check-in prompts<br>• Spam & bot filtration | • Hosting live AMA events & trader calls<br>• Managing VIP trader partnerships<br>• Resolving escalated member disputes | • WhatsApp Business API / Twilio<br>• Discord Bot Webhooks |

---

## 4. Prioritized Smart-Work Sequence to Nov 7

To ensure maximum user acquisition prior to November 7 with minimum wasted effort, FORTREX follows a strict **manual vs. automated threshold rule**:

### The <1,000 Users Threshold Rule
* **At <1,000 Users**: *Do things that don't scale.* Focus on personal founder outreach, manual VIP WhatsApp onboarding, direct conversation with high-volume traders, and simple scheduled CRON scripts. Do not over-engineer complex multi-tier automation.
* **At >1,000 Users**: *Activate full automation engines.* Transition entirely to event-driven Base44 workflows, automated referral position bumps, algorithmic email recovery, and AI-driven community moderation.

---

### Timeline & Phase-by-Phase Execution Sequence

```
[NOW: Sep 25] ------------> [Phase I: Oct 5] ------------> [Phase II: Oct 20] ------------> [Phase III: Nov 1] ------------> [LAUNCH: Nov 7]
Infra & Email Setup          Viral Engine Active          Content Machine & Ads         Launch Countdown Wave          Doors Open
```

#### Phase I: Infrastructure Repair & Core Automation (Sep 26 – Oct 5, 2026)
1. **Clear Base44 Platform Limits**: Upgrade Base44 organization plan to clear integration limits across `koda` and `arlo` apps.
2. **Connect Transactional Email API**: Input Resend/SendGrid API key into Base44 environment variables; verify `sendEmail.ts` delivery.
3. **Deploy Waitlist Welcome Workflow**: Activate automated welcome email + unique referral link creation on `FortrexWaitlist` `entity.create`.
4. **Deploy Telemetry Dashboard**: Mount single-pane analytics view on Command Center to track live signup velocity.

#### Phase II: Viral Referral Engine & Community Staging (Oct 6 – Oct 20, 2026)
1. **Activate Position-Bumping Automation**: Enable automatic position leap logic whenever `invite_count` increases.
2. **Launch WhatsApp VIP Community**: Connect WhatsApp API / group invite workflow for waitlist members reaching Top 1,000 positions.
3. **Deploy 3-Day Referral Nudge**: Schedule automated CRON workflow nudging inactive waitlist members with referral links.
4. **Scale Past 1,000 Users**: Transition from manual onboarding to full AI agent (Vesper) community moderation.

#### Phase III: Content Machine & Paid Acquisition (Oct 21 – Nov 1, 2026)
1. **Automated Weekly Content Batches**: Vesper generates and queues social post batches across Instagram, X, and LinkedIn.
2. **Launch Targeted Paid Ads**: Initiate micro-budget Meta/TikTok ad campaigns pointing to `landingpage` (track via UTM telemetry).
3. **Weekly Leaderboard Digest**: Run automated Friday social digests highlighting top referrers and countdown metrics.

#### Phase IV: Launch Countdown & VIP Wave Staging (Nov 2 – Nov 6, 2026)
1. **Activate T-5 Daily Countdown**: Vesper posts daily marker content across all social media and WhatsApp groups.
2. **Staggered Queue Staging**: Segment waitlist into Wave 1 (Top 1,000), Wave 2 (1,001–5,000), and Wave 3 (5,001+).
3. **Launch Sequence Dry Run**: Test automated email/WhatsApp broadcast execution on internal test contacts.

#### Phase V: Doors Open / Launch Day (Nov 7, 2026)
1. **00:00 UTC - Wave 1 Release**: Automated launch workflow sends platform credentials to Top 1,000 members.
2. **02:00 UTC - Wave 2 Release**: Second access wave released.
3. **Global Announcement**: Vesper broadcasts launch announcement across X, Discord, Instagram, and LinkedIn.
4. **Real-time Monitoring**: Founder monitors Base44 API quotas and database latency via Command Center dashboard.

---

## 5. Summary & Immediate Next Actions

1. **Deliverable Written**: Research document created at `/app/conversations/6ab65328f38dcd503d5b4965/research/06-automation-and-ops.md`.
2. **Immediate Bottleneck**: Base44 plan upgrade + Resend/SendGrid API key entry are the sole blockers preventing live welcome emails.
3. **Operational Leverage**: With Vesper managing social batching, leaderboard digests, and telemetry, the solo founder focuses 100% on high-value broker partnerships and product readiness.
