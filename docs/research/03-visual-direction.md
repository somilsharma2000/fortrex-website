# FORTREX Visual Direction & Experience Architecture
**Document Reference:** `03-visual-direction.md`  
**Brand:** FORTREX — Luxury Institutional Trading Brand  
**Palette:** Obsidian (`#050506`), Gold (`#D8A64D`), Bone White (`#FFF7E6`)  
**Typography:** Space Grotesk (Headlines/Display), Inter (Body/UI), JetBrains Mono (Data/Monospace)  
**Brand Voice:** Quiet Institutional Confidence  

---

## 1. Executive Summary & Brand Aesthetic Identity

Most prop firms and retail trading platforms operate in a sea of visual noise: electric neon blue SaaS gradients (`#0F172A`, `#3B82F6`), neon green/red buy/sell buttons, gamified confetti, and generic vector illustration kits. They look like temporary retail software built for retail gambling.

**FORTREX rejects retail SaaS tropes completely.**

FORTREX’s visual language is modeled after private Swiss vaults, high-frequency institutional trading desks, and hyper-exclusive asset management houses. It radiates **Quiet Institutional Confidence**:
*   **Palette Discipline:** Obsidian ground (`#050506`) as the dark canvas; metallic Gold (`#D8A64D`) reserved strictly for high-value signal, craftsmanship touches, and sovereign metrics; Bone White (`#FFF7E6`) for crisp, high-legibility typography and structure.
*   **Material Tactility:** Tactile dark surfaces, ultra-fine 1px golden hairlines, brushed metallic depth, dark noise texture, and subtle optical refraction instead of cheap blurry glassmorphism.
*   **Architectural Precision:** Extreme typographic hierarchy using Space Grotesk for commanding, tight-tracked display titles, paired with surgical JetBrains Mono tabular data layouts.

---

## 2. Signature Visual Moments (Ranked Matrix)

To establish an unforgettable identity, FORTREX relies on 7 signature visual moments, prioritized by Wow Factor versus Implementation Effort.

| Rank | Concept Name | Description & Interaction | Wow Factor | Effort Level | Technical Stack |
| :--- | :--- | :--- | :---: | :---: | :--- |
| **1** | **The Vault Iris** (Hero Entrance) | Interactive 3D mechanical gold/obsidian iris that unfolds quietly upon hero load or passkey auth, revealing sovereign platform telemetry. | **10/10** | **High** | Three.js / WebGL GLTF model + GSAP ScrollTrigger |
| **2** | **Liquid Gold Volatility Ribbon** | Live candlestick/order-book data rendered as an undulating 3D gold topography wave. High liquidity creates smooth liquid gold ripples; volatility creates sharp metallic peaks. | **9/10** | **High** | WebGL Custom Fragment Shader + WebSockets |
| **3** | **Gold-Leaf Payout Disintegration** | Upon passing an evaluation stage or confirming a payout request, a physics-driven burst of gold foil flakes crystallizes and disintegrates into obsidian space. | **9/10** | **Medium** | InstancedMesh GPU Particles + Canvas2D fallback |
| **4** | **Magnetic Golden Focal Cursor** | Minimalist reticle cursor that snaps to interactive elements, pulling a 1px gold border toward the focal point and illuminating a dark metallic substrate under the pointer. | **8/10** | **Medium** | Custom Pointer Events + CSS Variable Lighting Shader |
| **5** | **Trader Sovereign Parchment Badge** | Dynamic funded trader certificate featuring dynamic gold-embossed foil sheen that reflects phone gyroscope or desktop cursor tilt angles. | **8/10** | **Medium** | CSS 3D Tilt + Specular Gradient Overlay |
| **6** | **Institutional Monospaced Telemetry Ticker** | Micro-scale JetBrains Mono ticker running along ultra-fine gold hairlines at top/bottom viewport borders, displaying real-time spread, latency (ms), and liquidity depth. | **7/10** | **Low** | CSS Ticker / requestAnimationFrame |
| **7** | **Tactile Mechanical Audio Feedback** | Subdued, high-end mechanical clicks (sampled from physical luxury chronometers and vault switches) trigger on key user actions (order execution, tier selection). | **8/10** | **Low** | Web Audio API (Muted default + persistent toggle) |

---

## 3. Design System & Material Physics Specification

### 3.1 Material Realism & Depth Hierarchy
Rather than flat dark surfaces or generic Tailwind slate blues, FORTREX uses a 4-tier material depth system:

```
[ Tier 3: Gold Embellishment ]  --> #D8A64D (Metallic Specular, 1px Hairlines, Crown Badges)
[ Tier 2: Refractive Glass ]      --> rgba(216, 166, 77, 0.05) + Backdrop Blur (12px) + 1px Gold Border
[ Tier 1: Textured Obsidian ]     --> #0A0A0C + 2% Film Grain Noise Texture (Matte Finish)
[ Base Tier: Deep Obsidian Canvas ]--> #050506 (Absolute Depth Surface)
```

1.  **Obsidian Ground (`#050506`):** Deep, void-like canvas. Uses SVG noise texturing (2% opacity) to eliminate color banding on OLED screens and add physical paper/stone matte grain.
2.  **Gold Hairlines (`#D8A64D` at 15% - 100% opacity):** Borders are strictly 1px fine hairlines. Never use thick gold borders. Use linear gradients for borders: `linear-gradient(135deg, rgba(216,166,77,0.4) 0%, rgba(5,5,6,0) 50%, rgba(216,166,77,0.1) 100%)`.
3.  **Refractive Gold Glass:** Backdrop blur (12px to 16px), background `rgba(10, 10, 12, 0.75)`, with a top edge inset highlight of `1px solid rgba(216, 166, 77, 0.25)`.

### 3.2 Typography Scale & Rules

| Role | Font Family | Size (Desktop / Mobile) | Weight | Tracking / Line-Height | Case / Alignment |
| :--- | :--- | :--- | :---: | :---: | :--- |
| **Hero Display** | Space Grotesk | `80px` / `44px` | 700 Bold | `-0.04em` / `1.05` | Uppercase or Sentence |
| **H1 Section Title**| Space Grotesk | `48px` / `32px` | 600 SemiBold | `-0.03em` / `1.15` | Sentence case |
| **H2 Subhead** | Space Grotesk | `28px` / `22px` | 500 Medium | `-0.02em` / `1.25` | Sentence case |
| **Body Primary** | Inter | `16px` / `15px` | 400 Regular | `0em` / `1.6` | Left / Bone White (`#FFF7E6` @ 90%) |
| **Body Secondary**| Inter | `14px` / `13px` | 400 Regular | `0em` / `1.5` | Left / Muted (`#FFF7E6` @ 60%) |
| **Monospace Data** | JetBrains Mono | `13px` / `12px` | 500 Medium | `0em` / `1.4` | Tabular Figures (`font-variant-numeric: tabular-nums`) |
| **Micro Labels** | JetBrains Mono | `10px` / `10px` | 600 SemiBold | `+0.12em` / `1.2` | UPPERCASE / Muted Gold (`#D8A64D` @ 75%) |

### 3.3 Micro-Interactions & Hover Dynamics
*   **Button Hover State:** Buttons maintain a deep obsidian fill with a 1px `#D8A64D` border. On hover, a golden radial sheen follows the cursor inside the button bounds, and typography transitions from `#FFF7E6` to pure gold (`#D8A64D`) with zero layout shift.
*   **Card Hover State:** Cards lift slightly (`transform: translateY(-2px)`), the subtle top gold hairline opacity increases from 20% to 60%, and an inner shadow glow (`0 8px 32px -8px rgba(216, 166, 77, 0.12)`) reveals itself over 300ms cubic-bezier transition.
*   **Data Updates:** Price ticks and metric updates do NOT flash bright neon green/red. A positive tick displays a quiet, muted gold shimmer fade (200ms); a negative tick displays a quiet slate-grey dim (200ms).

### 3.4 Loading States & Telemetry Pacing
*   **No Generic Spinners:** Circular loading icons are strictly forbidden.
*   **The Telemetry Handshake:** Loading sequence displays a sleek JetBrains Mono terminal verification line:
    ```
    [SYS] VERIFYING INSTITUTIONAL VAULT KEYS... [OK]
    [DATA] ESTABLISHING 12ms FIX PROTOCOL BRIDGE... [CONNECTED]
    ```
    Accompanied by a 1px horizontal gold beam progress line extending along the top edge of the card or viewport.

### 3.5 Sound Design Specification
*   **Philosophy:** Audio must feel like operating a high-end physical vault or luxury timepiece.
*   **Audio Triggers:**
    *   *Click / Select:* Crisp 12ms mechanical tactile click (frequency peak at 2.4kHz, fast decay).
    *   *Success / Pass:* Low-frequency sub-bass thud (60Hz) combined with a soft 1.2s glass chime tail (1.8kHz resonance).
    *   *Error / Violation:* Muted dampener thud (80Hz, muted high-end).
*   **Rule:** Sound is disabled by default. A permanent minimalist speaker toggle (`AUDIO: OFF / ON`) sits in the top status bar. Settings persist in `localStorage`.

---

## 4. Evaluation of Unprecedented Trading / Fintech Concepts

| Concept | Visual & Functional Architecture | Feasibility & Verdict | Implementation Strategy |
| :--- | :--- | :--- | :--- |
| **1. Live Candlestick Data as Art** | Order book liquidity and historical candlestick velocity generate a 3D metallic ribbon topography in WebGL. High volume creates dramatic golden peaks and deep obsidian valleys. | **HIGHLY RECOMMENDED** (Signature Hero Concept) | WebGL shader running on offscreen canvas. Fallback to static vector topography SVG on mobile. |
| **2. Gold-Leaf Reward Particle FX** | Disintegration of gold leaf particles when completing an evaluation stage or reaching a payout milestone. Physics include gravity drift and specular gold lighting. | **HIGHLY RECOMMENDED** (High Viral Potential) | Three.js `InstancedMesh` with custom vertex shaders. Triggers on victory modal open. |
| **3. 3D Vault Door Login/Passkey** | Interactive heavy obsidian vault with brass/gold gear mechanisms that unlock and rotate 90 degrees when user enters 2FA / passkey. | **CONDITIONAL** (Use for Onboarding/Dashboard Entry) | High-impact for splash/login, but must be bypassable with "Quick Login" button to avoid frustrating daily traders. |
| **4. Ambient Dark Matter Field** | Subtle physics-based particle field hovering in hero background. Particles drift in dark gold and obsidian shades, slowly responding to mouse acceleration. | **RECOMMENDED** (Hero Background) | Canvas 2D particle simulation running with low particle count (40-60 max) to guarantee 60FPS. |
| **5. 'Trading Floor' Spatial Ambience** | Background subtle ambient audio (quiet low-frequency hum of a quiet private vault/floor) paired with reactive dark room lighting. | **REJECTED** (Too intrusive) | Replaced with explicit sound FX triggers on user interaction only. Background continuous audio distracts active traders. |

---

## 5. Social Media Visual System Specs

To build instant brand recognition across social channels (Instagram, X, LinkedIn, YouTube Shorts), FORTREX uses 4 production-ready template specifications.

### Spec 1: "The Institutional Directive" (Quote / Macro Statement)
*   **Format:** 1080x1350 (4:5 Portrait)
*   **Canvas:** Obsidian `#050506` with 3% film grain texture overlay.
*   **Outer Frame:** 1px Gold hairline border (`rgba(216, 166, 77, 0.2)`) offset 24px from image edge.
*   **Header:** JetBrains Mono 11px uppercase, tracking `+0.15em`, Muted Gold (`#D8A64D`): `FORTREX // INSTITUTIONAL DIRECTIVE 084`.
*   **Main Copy:** Space Grotesk 42px Bold, tracking `-0.03em`, line-height `1.15`, Bone White (`#FFF7E6`). Max 3 lines.
*   **Accent Element:** 1px horizontal gold line (`#D8A64D`, 60px length) separating copy from footer.
*   **Footer:** Left: JetBrains Mono 10px `LOCATION: ZÜRICH / FIXED-INCOME METRICS`. Right: Gold beveled crown logo mark (32px width).
*   **Safe Zone:** 64px padding on all edges.

### Spec 2: "Trade Telemetry Card" (Payout / Funded Performance)
*   **Format:** 1080x1350 (4:5 Portrait)
*   **Canvas:** Dark Obsidian `#0A0A0C` centered card resting over `#050506` ground.
*   **Card Container:** Rounded corners `8px`, 1px gold border gradient, subtle inset gold glow.
*   **Header Badge:** Muted Gold pill badge: `SOVEREIGN FUNDED TRADER`. Font: JetBrains Mono 10px Bold.
*   **Hero Stat:** JetBrains Mono 64px Bold, Tabular, Gold (`#D8A64D`): `$124,500.00`. Label below: Space Grotesk 12px uppercase `NET DISBURSED PAYOUT`.
*   **Metrics Grid (2x2):**
    *   *Win Rate:* `68.4%` (JetBrains Mono 20px)
    *   *Profit Factor:* `2.84` (JetBrains Mono 20px)
    *   *Instrument:* `XAU/USD` (JetBrains Mono 20px)
    *   *Trading Duration:* `14 DAYS` (JetBrains Mono 20px)
*   **Watermark:** Ultra-large muted Crown logo outline (opacity 4%) placed behind statistics.

### Spec 3: "Sovereign Trader Hall of Fame Certificate"
*   **Format:** 1080x1350 (4:5 Portrait)
*   **Canvas:** Brushed obsidian texture look (`#08080A`).
*   **Visual Motif:** Embossed golden wax seal / 3D crown emblem centered at top.
*   **Title:** Space Grotesk 36px SemiBold: `CERTIFICATE OF CAPITAL ALLOCATION`.
*   **Recipient Name:** Space Grotesk 28px Bold, Gold (`#D8A64D`): `TRADER ID // #8849-FX`.
*   **Allocation Tier:** JetBrains Mono 18px: `ACCOUNT TIER: $500,000 INSTITUTIONAL`.
*   **Cryptographic Verification:** Bottom edge displays 128-bit hash in JetBrains Mono 9px `HASH: 0x9f8a...3b21` to signal unforgeable authority.

### Spec 4: "Cinematic Reel Intro / Outro Slate"
*   **Format:** 1080x1920 (9:16 Vertical Video)
*   **Duration:** Intro 2.5 seconds / Outro 3.0 seconds.
*   **Animation Sequence (Intro):**
    *   *0.0s - 0.8s:* Black screen. Single 1px gold vertical line expands from center.
    *   *0.8s - 1.5s:* 3D Beveled Gold Crown logo forms with liquid gold reflection effect.
    *   *1.5s - 2.5s:* Space Grotesk text reveals letter-by-letter: `PRECISION CAPITAL. INSTITUTIONAL EXECUTION.`
*   **Sound:** Low sub-bass thud (0.8s) followed by crisp mechanical lock sound (1.5s).

---

## 6. Mobile-First Performance & Technical Rules

Over 70% of target traffic in key expansion markets (such as India) accesses FORTREX via mobile devices (Android mid-tier, Snapdragon 6xx/7xx series). Performance must be flawless.

### 6.1 Performance Budget Rules
*   **JS Bundle Size:** Total initial JavaScript budget <= **120 KB gzipped**.
*   **Core Web Vitals Targets:**
    *   First Contentful Paint (FCP): `< 1.0s`
    *   Largest Contentful Paint (LCP): `< 1.8s`
    *   Interaction to Next Paint (INP): `< 50ms`
    *   Cumulative Layout Shift (CLS): `0.00`
*   **Frame Rate Guarantee:** Locked **60 FPS** on desktop, stable **30-60 FPS** on mid-range mobile.

### 6.2 Progressive WebGL Canvas Strategy
1.  **Tiered GPU Rendering:**
    *   *High Tier (Desktop / High-end Mobile):* Active WebGL 3D Shader, particle canvas, dynamic depth blur.
    *   *Low Tier (Mobile low power / budget Android):* WebGL canvas automatically disabled. Replaced with lightweight CSS SVG mesh gradients and hardware-accelerated 2D CSS transforms.
2.  **Resolution Capping:**
    *   Never render WebGL canvas at native 3x DPR on mobile. Cap canvas resolution rendering at `DPR = Math.min(window.devicePixelRatio, 1.5)`.
3.  **Viewport Offscreen Pause:**
    *   All canvas render loops (`requestAnimationFrame`) MUST pause using `IntersectionObserver` when the canvas element scrolls out of the active viewport.

### 6.3 Accessibility & Reduced Motion Compliance
*   Respect user OS settings: `@media (prefers-reduced-motion: reduce)`.
*   When reduced motion is active:
    *   Disable particle field loops and liquid gold WebGL shaders.
    *   Replace scroll scrubbing animations with instant CSS opacity transitions (150ms).
    *   Disable magnetic cursor tracking.

---

## 7. Anti-Pattern Do / Don't Matrix

To ensure FORTREX never falls into the generic competitor trap, all design and engineering outputs must obey this strict matrix:

| Visual Element | ❌ COMPETITOR SAAS TEMPLATE (NEVER DO) | FORTREX INSTITUTIONAL (ALWAYS DO) |
| :--- | :--- | :--- |
| **Primary Ground** | Generic dark blue/slate gradients (`#0F172A`, `#1E293B`). | Deep Obsidian (`#050506`) with subtle 2% film grain noise. |
| **Accent Colors** | Neon electric blue (`#3B82F6`), neon cyan, neon purple gradients. | Metallic Gold (`#D8A64D`) reserved for high-signal metrics & craft details. |
| **Status Indicators** | Bright fluorescent neon green (`#00FF66`) and neon red (`#FF0055`). | Muted champagne gold (`#D8A64D`) for positive signal, slate grey (`#666666`) for neutral/negative. |
| **Typography** | Generic Sans-serifs (Plus Jakarta Sans, Outfit, Montserrat, Roboto). | **Space Grotesk** display, **Inter** body, **JetBrains Mono** tabular telemetry data. |
| **Borders & Framing** | Thick blue rounded borders (12px - 24px radius). | Crisp 1px gold/obsidian hairlines with minimal border radius (2px - 8px). |
| **Imagery & Icons** | 3D isometric blue coins, generic rocket ships, stock trading vectors. | Beveled gold crown mark, cryptographic security hashes, 3D liquidity topography. |
| **Loading States** | Generic spinning circles or bouncing dots. | Monospaced FIX protocol telemetry handshake and gold hairline beam loader. |
| **Buttons & CTAs** | Giant pill-shaped blue/green gradient buttons with heavy drop shadows. | Rectangular razor-sharp obsidian buttons with 1px gold stroke and subtle radial hover sheen. |
| **Social Content** | Cluttered graphics with huge stock charts, neon arrows, and spammy text. | High-contrast "Institutional Directive" layout with luxury typography scale and gold hairline framing. |
