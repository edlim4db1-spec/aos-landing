# Design System: AOS (Agentic Operating System)

> **Single source of truth for all AOS surfaces.**
> Use this file to prompt any AI coding agent — Google Stitch, Cursor, Claude Code, Lovable, v0, or any other — to generate consistent, on-brand UI.
> AOS is dark-mode only. Do not add light mode variants.

---

## 1. Visual Theme & Atmosphere

AOS is the OS for factories that run themselves. The design must feel like precision instrumentation — not a SaaS dashboard, not a startup landing page, but a control surface built for industrial operators and the investors who back them. The visual language borrows from mission-critical software: dense information hierarchy, subdued chrome, purposeful color.

The canvas is near-black with a faint blue-violet undertone (`#0f0f14`), not pure black. Content emerges from this darkness through carefully calibrated surface levels — five distinct steps of luminance, each serving a structural role. Surfaces never feel "lit"; they feel like material differences. Borders are alpha-based and invisible at rest, brightening only at interaction boundaries.

The dual-font strategy is intentional and non-negotiable: **Instrument Serif** for marketing headlines creates editorial authority — the kind of serif confidence that signals "we've solved something real." **Inter** (variable, weight 420 as body default) handles all product UI. **JetBrains Mono** marks every data value, ID, timestamp, and agent decision. This three-voice system gives AOS the breadth to speak in a boardroom pitch and a factory floor dashboard.

The single brand accent is **teal (`#00D4AA`)**. It appears on primary actions, active states, and the agent network's orchestrator node. All six operational agents have their own chromatic identity — these colors are semantic, not decorative, and encode which agent is speaking at any moment.

The background carries two persistent structural motifs: a faint **structural grid** (1px lines at reduced opacity, masked with a radial gradient so they fade toward the edges) and ambient **SVG blur blobs** in the hero (feGaussianBlur stdDeviation=64, teal at 4% opacity). Neither element clutters; both signal that this is engineered infrastructure.

**Key Characteristics:**
- Dark-mode-only: `#0f0f14` base, five surface levels up to `#35354a`
- Instrument Serif for marketing headlines; Satoshi or Inter for product app headlines; Inter variable (weight 420) for body
- JetBrains Mono for all data, IDs, agent output, and code
- Single primary accent: teal `#00D4AA`, with six agent-specific colors
- Alpha-based borders throughout: `rgba(255,255,255,0.06)` default, `rgba(255,255,255,0.16)` at interaction
- No box-shadow on cards — border-only depth system (inherited from Vercel's precision, adapted for dark)
- Mouse-tracking shine on interactive cards via CSS `mask-image` radial gradient
- `filter: brightness()` for all hover states — never background-color changes
- Structural grid lines as background motif (1px, opacity 0.3, radial-gradient masked)
- SVG blur blobs for ambient hero glow (feGaussianBlur stdDeviation=64)
- Six agent colors encode operational domains: Procurement (teal), Production (blue), Inventory (amber), Sales (purple), Quality (red), Finance (gold)
- 6px radius for buttons, 10px for cards, 12px for modals — never pill/rounded-full
- No emoji anywhere. All icons are custom SVG paths at 1.5px stroke

---

## 2. Color Palette & Roles

### Background Surfaces

| Token | Value | Role |
|-------|-------|------|
| `--bg-base` | `#0f0f14` | Primary background — the canvas. Hero, full-bleed sections. |
| `--surface-1` | `#13131a` | First surface level — card backgrounds, panels. |
| `--surface-2` | `#1a1a22` | Second surface — elevated cards, sidebar. |
| `--surface-3` | `#21212b` | Third surface — hover targets, section backgrounds. |
| `--surface-4` | `#2a2a35` | Fourth surface — active states, selected items. |
| `--surface-5` | `#35354a` | Fifth surface — highest elevation, tooltips, dropdowns. |

**Elevation philosophy**: Depth is communicated through background luminance stepping, not shadows. Deeper = darker. Each level increases luminance fractionally, creating a stacking model where the user instinctively perceives z-order without explicit shadows.

### Brand Accent

| Token | Value | Role |
|-------|-------|------|
| `--accent` | `#00D4AA` | Primary teal — CTAs, active states, orchestrator node |
| `--accent-hover` | `#1AFFC4` | Hover variant — used via `brightness(1.15)` on the accent |
| `--accent-dim` | `rgba(0, 212, 170, 0.08)` | Teal background tint for chips, badges |
| `--accent-glow` | `rgba(0, 212, 170, 0.12)` | Ambient teal glow for hero SVG blobs |
| `--accent-border` | `rgba(0, 212, 170, 0.30)` | Teal accent border for highlighted elements |

### Agent Colors (Semantic — Not Decorative)

Each color represents exactly one agent domain. Use only in that context.

| Agent | Token | Value | Usage |
|-------|-------|-------|-------|
| Procurement | `--agent-procurement` | `#00D4AA` | Teal — same as brand accent |
| Production | `--agent-production` | `#5B8DEF` | Blue |
| Inventory | `--agent-inventory` | `#F59E42` | Amber |
| Sales | `--agent-sales` | `#A47AE8` | Purple |
| Quality | `--agent-quality` | `#EF6461` | Red |
| Finance | `--agent-finance` | `#E2B94B` | Gold |

Dim variants (8% opacity backgrounds for chips/badges):
```css
--agent-procurement-dim: rgba(0, 212, 170, 0.08);
--agent-production-dim:  rgba(91, 141, 239, 0.08);
--agent-inventory-dim:   rgba(245, 158, 66, 0.08);
--agent-sales-dim:       rgba(164, 122, 232, 0.08);
--agent-quality-dim:     rgba(239, 100, 97, 0.08);
--agent-finance-dim:     rgba(226, 185, 75, 0.08);
```

### Text Hierarchy

| Token | Value | Role |
|-------|-------|------|
| `--text-primary` | `#e4e4e7` | Headings, important content. Not pure white — reduces eye strain. |
| `--text-secondary` | `#8b8b94` | Body copy, descriptions, most UI labels. |
| `--text-tertiary` | `#5a5a65` | Captions, metadata, timestamps. |
| `--text-faint` | `#3a3a45` | Disabled text, placeholders. |
| `--text-inverse` | `#0f0f14` | Text on teal accent backgrounds. |

### Border System

All borders use alpha-based white, adapting to any surface without explicit overrides.

| Token | Value | Role |
|-------|-------|------|
| `--border-default` | `rgba(255, 255, 255, 0.06)` | Default — dividers, card edges, separators |
| `--border-strong` | `rgba(255, 255, 255, 0.10)` | Inputs, interactive containers |
| `--border-vivid` | `rgba(255, 255, 255, 0.16)` | Hover state, active borders |
| `--border-focus` | `rgba(0, 212, 170, 0.50)` | Focus rings on interactive elements |

### Semantic Status

| Token | Value | Role |
|-------|-------|------|
| `--success` | `#34d399` | Confirmed, on-track, completed |
| `--warning` | `#F59E42` | In-progress, manufacturing alerts (same as Inventory agent) |
| `--error` | `#EF6461` | Errors, overdue, destructive (same as Quality agent) |

### Secondary Accent

| Token | Value | Role |
|-------|-------|------|
| `--amber` | `#F59E42` | Manufacturing alerts, warnings — the "factory floor" signal color |

---

## 3. Typography Rules

### Font Families

```css
/* Marketing / Landing page headlines only */
--font-display:  'Instrument Serif', Georgia, 'Times New Roman', serif;

/* Product app headlines — alternative display */
--font-display-alt: 'Satoshi', 'Inter', system-ui, sans-serif;

/* All body text, UI, navigation */
--font-body:     'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;

/* Data, IDs, agent output, code, monospace labels */
--font-mono:     'JetBrains Mono', 'SF Mono', 'Fira Code', ui-monospace, monospace;
```

**Font loading:**
- Inter: Google Fonts variable, `wght@100..900`
- Instrument Serif: Google Fonts, regular + italic
- JetBrains Mono: Google Fonts, `wght@400;500`
- Satoshi: Fontshare CDN (for product app headlines, optional)

**OpenType features on Inter:**
```css
font-feature-settings: "cv01", "ss03";
```
These are non-negotiable — `cv01` gives a single-story 'a', `ss03` cleans up specific letterforms. Without them, Inter looks generic; with them, it reads as a deliberate choice.

### Type Scale

| Role | Font | Size | Weight | Line Height | Letter Spacing | Notes |
|------|------|------|--------|-------------|----------------|-------|
| Hero Display | Instrument Serif | `clamp(2.75rem, 2rem + 4vw, 4.5rem)` | 400 | 1.05 | -0.03em | Landing page hero. Serif italic permitted on select words. |
| Section Title | Instrument Serif | `clamp(1.75rem, 1.25rem + 2vw, 2.75rem)` | 400 | 1.10 | -0.025em | Marketing section headings |
| App Heading XL | Satoshi / Inter | 2.25rem (36px) | 600 | 1.10 | -0.025em | Product app top-level headers |
| App Heading L | Inter | 1.75rem (28px) | 590 | 1.15 | -0.02em | Dashboard section titles |
| App Heading M | Inter | 1.25rem (20px) | 590 | 1.25 | -0.015em | Card headers, feature titles |
| App Heading S | Inter | 1rem (16px) | 590 | 1.33 | -0.01em | Sub-section headers |
| Body | Inter | 0.9375rem (15px) | 420 | 1.60 | -0.011em | **Default body text. Weight 420, not 400 — heavier for dark backgrounds.** |
| Body Small | Inter | 0.875rem (14px) | 420 | 1.55 | -0.008em | Descriptions, secondary content |
| Label / UI | Inter | 0.8125rem (13px) | 510 | 1.50 | -0.005em | Navigation, buttons, labels |
| Caption | Inter | 0.8125rem (13px) | 420 | 1.45 | 0 | Metadata, timestamps |
| Micro | Inter | 0.75rem (12px) | 510 | 1.40 | 0 | Tiny labels, overlines |
| Mono / Data | JetBrains Mono | 0.75rem (12px) | 400 | 1.50 | 0 | IDs, numbers, agent output |
| Mono Body | JetBrains Mono | 0.875rem (14px) | 400 | 1.60 | 0 | Code blocks, terminal output |

**Weight reference for Inter variable:**
- 420 — AOS body default (between regular 400 and medium 500 — reads heavier on dark backgrounds without feeling bold)
- 510 — AOS emphasis/UI default (signature weight for navigation, labels, interactive elements)
- 590 — Semibold — headings, card titles, strong emphasis

**Display letter-spacing formula:** Letter-spacing tightens with scale. At 72px: -0.03em. At 48px: -0.025em. At 32px: -0.02em. Relaxes toward 0 below 16px. Apply this progressively — never positive letter-spacing on display text.

### Typography Principles

1. **Serif / sans contrast is the marketing signature.** Instrument Serif for headlines, Inter for everything else on landing pages. The contrast creates editorial authority that generic SaaS sans-serif stacks lack.
2. **420 is the body weight.** Dark backgrounds demand slightly heavier type for the same optical weight as 400 on white. Do not revert to 400 for body text.
3. **Mono for all data values.** Any number, ID, timestamp, currency value, quantity, or agent decision output must use JetBrains Mono. This is non-negotiable — it signals precision and makes data scannable.
4. **Never ALL CAPS on body.** Uppercase reserved for overlines, table headers, and agent chip labels only — max 0.05em letter-spacing when used.
5. **Line height for marketing: 1.05–1.10 for display, 1.6 for body.** The contrast between compressed headlines and open body text creates visual tension.

---

## 4. Component Stylings

### Buttons

**Primary (Teal — Brand CTA):**
```css
.btn-primary {
  background: #00D4AA;
  color: #0f0f14;
  font-family: 'Inter', sans-serif;
  font-size: 0.8125rem;        /* 13px */
  font-weight: 590;
  letter-spacing: -0.005em;
  padding: 0.5rem 1.25rem;
  border-radius: 6px;
  border: none;
  transition: filter 0.12s cubic-bezier(0.23, 1, 0.32, 1);
  cursor: pointer;
}
.btn-primary:hover {
  filter: brightness(1.15);    /* Never change background-color — use brightness() */
}
.btn-primary:active {
  filter: brightness(0.92);
}
```

**Ghost (Secondary):**
```css
.btn-ghost {
  background: transparent;
  color: #8b8b94;
  font-size: 0.8125rem;
  font-weight: 510;
  padding: 0.5rem 1.25rem;
  border-radius: 6px;
  border: 1px solid rgba(255, 255, 255, 0.10);
  transition: border-color 0.12s cubic-bezier(0.23, 1, 0.32, 1),
              color 0.12s cubic-bezier(0.23, 1, 0.32, 1),
              filter 0.12s cubic-bezier(0.23, 1, 0.32, 1);
}
.btn-ghost:hover {
  border-color: rgba(255, 255, 255, 0.16);
  color: #e4e4e7;
}
```

**Danger:**
```css
.btn-danger {
  background: #EF6461;
  color: #0f0f14;
  /* Same metrics as primary */
}
.btn-danger:hover { filter: brightness(1.12); }
```

**Button rules:**
- 6px radius. Never pill-shaped (`border-radius: 9999px`).
- Always sentence case. Never ALL CAPS.
- Max one primary button per view or major section.
- Disabled: `opacity: 0.4`, no hover effect, `cursor: not-allowed`.
- Icon-only buttons: 32×32px, same radius.
- Hover technique: `filter: brightness()` — not `background-color` change.

### Cards

```css
.card {
  background: #13131a;                           /* Surface Level 1 */
  border: 1px solid rgba(255, 255, 255, 0.06);  /* --border-default */
  border-radius: 10px;
  padding: 1.5rem;
  position: relative;
  overflow: hidden;
  transition: border-color 0.28s cubic-bezier(0.23, 1, 0.32, 1),
              filter 0.28s cubic-bezier(0.23, 1, 0.32, 1);
}
.card:hover {
  border-color: rgba(255, 255, 255, 0.16);     /* --border-vivid */
  filter: brightness(1.06);
}
```

**No `box-shadow` on cards.** The border-only system (inspired by Vercel's engineering precision) provides clean separation on dark backgrounds without the muddiness of drop shadows.

**Mouse-tracking card shine** (interactive cards):
```css
/* Applied via JS: track mousemove, update --mouse-x and --mouse-y as percentages */
.card-interactive::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: inherit;
  background: radial-gradient(
    400px circle at var(--mouse-x, 50%) var(--mouse-y, 50%),
    rgba(255, 255, 255, 0.04),
    transparent 60%
  );
  mask-image: radial-gradient(
    400px circle at var(--mouse-x, 50%) var(--mouse-y, 50%),
    black,
    transparent 60%
  );
  pointer-events: none;
  z-index: 1;
}
```

**Dashboard stat card:**
```css
.stat-card {
  background: #13131a;
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 10px;
  padding: 1.5rem;
}
.stat-card .value {
  font-family: 'JetBrains Mono', monospace;
  font-size: 1.75rem;
  font-weight: 500;
  color: #e4e4e7;
  letter-spacing: -0.02em;
}
.stat-card .label {
  font-size: 0.75rem;
  font-weight: 510;
  color: #5a5a65;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin-top: 0.25rem;
}
.stat-card .delta {
  font-size: 0.8125rem;
  font-family: 'JetBrains Mono', monospace;
}
.stat-card .delta.positive { color: #34d399; }
.stat-card .delta.negative { color: #EF6461; }
```

### Inputs & Forms

```css
.input {
  height: 2rem;                               /* 32px */
  padding: 0 0.75rem;
  background: #0f0f14;
  border: 1px solid rgba(255, 255, 255, 0.10);
  border-radius: 6px;
  color: #e4e4e7;
  font-family: 'Inter', sans-serif;
  font-size: 0.8125rem;
  font-weight: 420;
  transition: border-color 0.12s cubic-bezier(0.23, 1, 0.32, 1),
              box-shadow 0.12s cubic-bezier(0.23, 1, 0.32, 1);
}
.input::placeholder { color: #3a3a45; }
.input:focus {
  border-color: rgba(0, 212, 170, 0.50);
  box-shadow: 0 0 0 3px rgba(0, 212, 170, 0.10);
  outline: none;
}
.input:disabled { opacity: 0.4; cursor: not-allowed; }
```

### Navigation

**Top navigation bar (marketing/landing):**
```css
.nav {
  position: sticky;
  top: 0;
  z-index: 100;
  background: rgba(15, 15, 20, 0.85);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
  height: 56px;
  display: flex;
  align-items: center;
  padding: 0 1.5rem;
}
.nav-link {
  font-size: 0.8125rem;
  font-weight: 510;
  color: #8b8b94;
  text-decoration: none;
  transition: color 0.12s ease;
}
.nav-link:hover { color: #e4e4e7; }
```

**Sidebar navigation (product app):**
```css
.sidebar {
  width: 240px;
  background: #13131a;
  border-right: 1px solid rgba(255, 255, 255, 0.06);
  padding: 0.5rem;
}
.nav-item {
  display: flex;
  align-items: center;
  height: 28px;
  padding: 0 0.5rem;
  border-radius: 6px;
  color: #5a5a65;
  font-size: 0.8125rem;
  font-weight: 510;
  gap: 0.5rem;
  cursor: pointer;
  transition: background 0.12s ease, color 0.12s ease;
}
.nav-item:hover {
  background: rgba(255, 255, 255, 0.04);
  color: #8b8b94;
}
.nav-item.active {
  background: rgba(0, 212, 170, 0.08);
  color: #00D4AA;
}
.nav-section-label {
  font-size: 0.6875rem;       /* 11px */
  font-weight: 510;
  color: #3a3a45;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  padding: 1rem 0.5rem 0.25rem;
}
```

### Badges & Status Indicators

**Active/status pulse dot:**
```css
.status-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  display: inline-block;
  flex-shrink: 0;
}
.status-dot.active {
  background: #34d399;
  box-shadow: 0 0 0 0 rgba(52, 211, 153, 0.4);
  animation: pulse-dot 2s cubic-bezier(0.19, 1, 0.22, 1) infinite;
}
@keyframes pulse-dot {
  0%   { box-shadow: 0 0 0 0 rgba(52, 211, 153, 0.4); }
  70%  { box-shadow: 0 0 0 6px rgba(52, 211, 153, 0); }
  100% { box-shadow: 0 0 0 0 rgba(52, 211, 153, 0); }
}
.status-dot.warning  { background: #F59E42; }
.status-dot.error    { background: #EF6461; }
.status-dot.inactive { background: #3a3a45; }
```

**Agent chip** (identifies which agent produced a piece of content):
```css
.agent-chip {
  display: inline-flex;
  align-items: center;
  height: 18px;
  padding: 0 0.375rem;
  border-radius: 3px;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.5625rem;       /* 9px */
  font-weight: 500;
  letter-spacing: 0.04em;
  text-transform: uppercase;
}
/* Apply agent color via modifier classes */
.agent-chip.procurement { background: rgba(0,212,170,0.08);   color: #00D4AA; }
.agent-chip.production  { background: rgba(91,141,239,0.08);  color: #5B8DEF; }
.agent-chip.inventory   { background: rgba(245,158,66,0.08);  color: #F59E42; }
.agent-chip.sales       { background: rgba(164,122,232,0.08); color: #A47AE8; }
.agent-chip.quality     { background: rgba(239,100,97,0.08);  color: #EF6461; }
.agent-chip.finance     { background: rgba(226,185,75,0.08);  color: #E2B94B; }
```

**Badge (count / label):**
```css
.badge {
  display: inline-flex;
  align-items: center;
  height: 18px;
  padding: 0 0.375rem;
  border-radius: 4px;
  font-size: 0.75rem;
  font-weight: 510;
}
.badge.default  { background: #21212b; color: #8b8b94; }
.badge.success  { background: rgba(52,211,153,0.10); color: #34d399; }
.badge.warning  { background: rgba(245,158,66,0.10); color: #F59E42; }
.badge.error    { background: rgba(239,100,97,0.10); color: #EF6461; }
```

### Tables

```css
.table { width: 100%; border-collapse: collapse; }
.table th {
  height: 28px;
  padding: 0 0.75rem;
  font-size: 0.6875rem;       /* 11px */
  font-weight: 510;
  color: #5a5a65;
  text-transform: uppercase;
  letter-spacing: 0.04em;
  text-align: left;
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
  position: sticky;
  top: 0;
  background: #0f0f14;
}
.table td {
  height: 36px;
  padding: 0 0.75rem;
  font-size: 0.8125rem;
  color: #8b8b94;
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
}
.table tr:hover td { background: rgba(255, 255, 255, 0.03); }
.table td.id {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.6875rem;
  color: #5a5a65;
}
.table td.numeric {
  font-family: 'JetBrains Mono', monospace;
  text-align: right;
}
```

**Table rules:**
- No visible vertical borders, ever.
- Horizontal dividers: `--border-default` only.
- No zebra striping.
- Header row: sticky, uppercase, 11px/510, `--text-tertiary`.
- Numeric columns: right-aligned, JetBrains Mono.

### Modals / Dialogs

```css
.modal-backdrop {
  background: rgba(0, 0, 0, 0.70);
  backdrop-filter: blur(6px);
  -webkit-backdrop-filter: blur(6px);
}
.modal {
  background: #1a1a22;
  border: 1px solid rgba(255, 255, 255, 0.10);
  border-radius: 12px;
  padding: 1.5rem;
  max-width: 480px;
  width: 100%;
  animation: modal-enter 0.28s cubic-bezier(0.23, 1, 0.32, 1);
}
@keyframes modal-enter {
  from { opacity: 0; transform: scale(0.97) translateY(6px); }
  to   { opacity: 1; transform: scale(1)    translateY(0);   }
}
.modal-title {
  font-size: 1rem;
  font-weight: 590;
  color: #e4e4e7;
  margin-bottom: 0.5rem;
}
.modal-body {
  font-size: 0.8125rem;
  color: #8b8b94;
  line-height: 1.60;
}
.modal-footer {
  display: flex;
  justify-content: flex-end;
  gap: 0.5rem;
  margin-top: 1.5rem;
}
```

### Code Blocks & Terminal Output

Inspired by Vercel's terminal/code block aesthetic — dark surface with precise mono typography:

```css
.code-block {
  background: #13131a;
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 10px;
  padding: 1rem 1.25rem;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.8125rem;
  line-height: 1.65;
  color: #8b8b94;
  overflow-x: auto;
}
.code-block .token-keyword   { color: #00D4AA; }
.code-block .token-string    { color: #A47AE8; }
.code-block .token-comment   { color: #3a3a45; font-style: italic; }
.code-block .token-number    { color: #F59E42; }
.code-block .token-function  { color: #5B8DEF; }
```

**Browser chrome frame** (for product screenshots):
```css
.browser-frame {
  background: #1a1a22;
  border: 1px solid rgba(255, 255, 255, 0.10);
  border-radius: 12px;
  overflow: hidden;
}
.browser-frame .chrome-bar {
  height: 36px;
  background: #21212b;
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
  display: flex;
  align-items: center;
  padding: 0 1rem;
  gap: 0.375rem;
}
.browser-frame .traffic-light {
  width: 10px; height: 10px; border-radius: 50%;
  background: rgba(255, 255, 255, 0.10);
}
.browser-frame .url-bar {
  flex: 1;
  height: 22px;
  background: #13131a;
  border-radius: 4px;
  margin: 0 0.75rem;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.6875rem;
  color: #5a5a65;
  display: flex;
  align-items: center;
  padding: 0 0.5rem;
}
```

### Command Palette (⌘K)

```css
.command-palette {
  background: #1a1a22;
  border: 1px solid rgba(255, 255, 255, 0.10);
  border-radius: 12px;
  width: 560px;
  max-height: 400px;
  overflow: hidden;
  /* Layered shadow from Linear for dialogs on dark surfaces */
  box-shadow:
    rgba(0,0,0,0)    0px  8px  2px,
    rgba(0,0,0,0.01) 0px  5px  2px,
    rgba(0,0,0,0.04) 0px  3px  2px,
    rgba(0,0,0,0.07) 0px  1px  1px,
    rgba(0,0,0,0.08) 0px  0px  1px;
}
.command-input {
  height: 44px;
  padding: 0 1rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
  font-size: 0.9375rem;
  font-weight: 420;
  background: transparent;
  color: #e4e4e7;
}
.command-item {
  height: 36px;
  padding: 0 1rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.8125rem;
  font-weight: 420;
  color: #8b8b94;
  cursor: pointer;
  transition: background 0.08s ease;
}
.command-item:hover, .command-item.selected {
  background: rgba(255, 255, 255, 0.04);
  color: #e4e4e7;
}
.command-item .shortcut {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.6875rem;
  color: #3a3a45;
  margin-left: auto;
}
```

### AOS-Specific Components

**Live operations feed** (auto-scrolling agent decisions):
```css
.ops-feed {
  background: #13131a;
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 10px;
  padding: 0;
  overflow: hidden;
  height: 320px;
  position: relative;
}
.ops-feed .feed-scroll {
  animation: feed-scroll 20s linear infinite;
}
@keyframes feed-scroll {
  0%   { transform: translateY(0); }
  100% { transform: translateY(-50%); }  /* Duplicate content for seamless loop */
}
.ops-feed-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.625rem 1rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.04);
}
.ops-feed-item .timestamp {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.6875rem;
  color: #3a3a45;
  flex-shrink: 0;
  min-width: 3.5rem;
}
.ops-feed-item .message {
  font-size: 0.8125rem;
  color: #8b8b94;
  font-weight: 420;
}
```

**Agent network hexagonal display** (hero visualization):
- 6 outer nodes arranged at 60° intervals around a central orchestrator
- Each outer node uses its agent color (`--agent-*`)
- Central node uses `--accent` teal with a pulsing ring
- Connection lines: `stroke: rgba(255,255,255,0.08)`, gradient from source agent color to transparent at midpoint
- SVG-only — no canvas. Animatable with CSS transforms on SVG `<g>` elements.

**Comparison table** (AOS column highlighted):
```css
.comparison-table th.aos-column {
  color: #00D4AA;
  border-bottom: 2px solid #00D4AA;
}
.comparison-table td.aos-column {
  background: rgba(0, 212, 170, 0.04);
  border-left:  1px solid rgba(0, 212, 170, 0.15);
  border-right: 1px solid rgba(0, 212, 170, 0.15);
}
```

---

## 5. Layout Principles

### Spacing System

Base unit: 4px. All spacing is a multiple of this unit.

| Token | Value | Usage |
|-------|-------|-------|
| `--space-1` | 4px | Icon-to-text gaps, tight inline spacing |
| `--space-2` | 8px | Default component gap, compact padding |
| `--space-3` | 12px | Input padding, chip padding |
| `--space-4` | 16px | Card internal spacing, nav item padding |
| `--space-5` | 20px | Small section gaps |
| `--space-6` | 24px | Card padding default, column gaps |
| `--space-8` | 32px | Section separators, large content gaps |
| `--space-12` | 48px | Major section spacing (product app) |
| `--space-section` | `clamp(5rem, 10vw, 10rem)` | Landing page section padding |

**Card padding:** `1.5rem` (24px) — this is the fixed value.
**Component gap:** `0.75rem` (12px) — gap between elements within a component.
**Section padding:** `clamp(5rem, 10vw, 10rem)` — generous negative space between sections.
**Max content width:** `1180px`.

### Grid & Container

**Landing page:**
```css
.container {
  max-width: 1180px;
  margin: 0 auto;
  padding: 0 1.5rem;
}
@media (min-width: 768px)  { .container { padding: 0 3rem; } }
@media (min-width: 1024px) { .container { padding: 0 4rem; } }
```

**Product app:**
```css
.app-layout {
  display: grid;
  grid-template-columns: 240px 1fr;
  min-height: 100vh;
}
/* Below 1024px: sidebar collapses to 48px icon rail */
/* Below 768px: sidebar becomes slide-over drawer */
```

**Feature card grids:**
- Desktop (≥1024px): 3-column grid, `gap: 1.5rem`
- Tablet (768–1023px): 2-column grid
- Mobile (<768px): single column

**Structural grid background:**
```css
.structural-grid {
  position: absolute;
  inset: 0;
  pointer-events: none;
  background-image:
    linear-gradient(rgba(255,255,255,0.04) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.04) 1px, transparent 1px);
  background-size: 48px 48px;
  mask-image: radial-gradient(ellipse 80% 80% at 50% 50%, black 30%, transparent 100%);
  opacity: 0.3;
}
```

### Whitespace Philosophy

**Darkness as negative space:** On `#0f0f14`, the background IS the whitespace. Do not fill sections out of anxiety — emptiness is intentional and communicates confidence.

**Section rhythm:** Marketing sections need `clamp(5rem, 10vw, 10rem)` vertical padding. This cinematic pacing lets each section breathe as its own scene. Dense product data in the app follows different rules (36px rows, tight 24px padding), but marketing always has room.

**Sticky scroll storytelling:** For feature explanation sections, pin the text column to the left (`position: sticky; top: 5rem`) while the right column scrolls through product screenshots. This technique reveals product depth without requiring the user to navigate away.

### Border Radius Scale

| Value | Usage | Context |
|-------|-------|---------|
| 3px | Inline code spans, micro tags | The smallest visual container |
| 6px | Buttons, inputs, dropdowns, nav items | Functional interactive elements |
| 10px | Cards, content containers | Standard card — the workhorse |
| 12px | Modals, large panels, browser frames | Overlapping surfaces |
| 50% | Status dots, avatars | Circles only — never for buttons |

**NEVER use `border-radius: 9999px` on buttons.** This is the most important constraint in the system. Pill buttons look like consumer SaaS. AOS looks like precision tooling.

---

## 6. Depth & Elevation

### Surface Stack

| Level | Background | Border | Use |
|-------|-----------|--------|-----|
| Base (0) | `#0f0f14` | None | Page canvas, hero sections |
| Surface 1 | `#13131a` | `rgba(255,255,255,0.06)` | Cards, panels, main content areas |
| Surface 2 | `#1a1a22` | `rgba(255,255,255,0.06)` | Elevated cards, sidebars, modals |
| Surface 3 | `#21212b` | `rgba(255,255,255,0.10)` | Hover states, section backgrounds |
| Surface 4 | `#2a2a35` | `rgba(255,255,255,0.10)` | Active states, selected rows |
| Surface 5 | `#35354a` | `rgba(255,255,255,0.16)` | Tooltips, dropdowns, highest elevation |

### Shadow Usage

Shadows are used sparingly — only where surfaces overlap and the hierarchy is ambiguous.

```css
/* Floating elements (tooltips, dropdowns) only */
--shadow-sm: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.08);

/* Modals, command palette — from Linear's dialog shadow stack */
--shadow-dialog:
  rgba(0,0,0,0)    0px  8px  2px,
  rgba(0,0,0,0.01) 0px  5px  2px,
  rgba(0,0,0,0.04) 0px  3px  2px,
  rgba(0,0,0,0.07) 0px  1px  1px,
  rgba(0,0,0,0.08) 0px  0px  1px;
```

**No `box-shadow` on cards.** Cards use border-only separation. On dark backgrounds, box-shadows are nearly invisible and add visual noise without contributing to hierarchy.

### SVG Blur Blob (Hero Glow)

```html
<svg class="hero-blob" xmlns="http://www.w3.org/2000/svg"
     style="position:absolute; top:0; left:50%; transform:translateX(-50%); 
            width:900px; height:600px; pointer-events:none; overflow:visible; z-index:0;">
  <defs>
    <filter id="blur-heavy">
      <feGaussianBlur stdDeviation="64" />
    </filter>
  </defs>
  <!-- Teal primary blob -->
  <ellipse cx="450" cy="200" rx="300" ry="180"
           fill="rgba(0, 212, 170, 0.12)" filter="url(#blur-heavy)" />
  <!-- Secondary Production-blue blob -->
  <ellipse cx="280" cy="300" rx="200" ry="140"
           fill="rgba(91, 141, 239, 0.06)" filter="url(#blur-heavy)" />
</svg>
```

This technique provides ambient color that feels emergent from the darkness rather than painted on.

---

## 7. Motion & Interaction

### Easing Functions

```css
--ease-out-expo:  cubic-bezier(0.19, 1, 0.22, 1);   /* Exits, dismissals — fast then sharp stop */
--ease-standard:  cubic-bezier(0.23, 1, 0.32, 1);   /* Standard enters, hover transitions */
--ease-spring:    cubic-bezier(0.34, 1.56, 0.64, 1); /* Energetic reveals, popping into place */
```

### Transition Durations

| Token | Duration | Usage |
|-------|----------|-------|
| `--t-quick` | 0.12s | Icon state, immediate feedback |
| `--t-normal` | 0.28s | Hover, focus, card transitions |
| `--t-slow` | 0.5s | Page-level reveals, scroll animations |
| `--t-modal` | 0.28s | Modal/dialog enter with `--ease-standard` |

### Hover Principle

**Use `filter: brightness()` — not background-color changes.**

```css
/* Correct */
.btn-primary:hover { filter: brightness(1.15); }
.card:hover        { filter: brightness(1.06); }

/* Wrong */
.btn-primary:hover { background-color: #1AFFC4; }  /* Never */
```

This technique preserves complex backgrounds (gradients, images) and ensures consistent behavior across all surface types without needing per-element hover color overrides.

### Scroll Reveal

```css
.reveal {
  opacity: 0;
  transform: translateY(14px);
  transition:
    opacity   var(--t-slow) var(--ease-standard),
    transform var(--t-slow) var(--ease-standard);
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}

/* Stagger siblings — 70ms between children */
.reveal-group > .reveal:nth-child(1) { transition-delay:   0ms; }
.reveal-group > .reveal:nth-child(2) { transition-delay:  70ms; }
.reveal-group > .reveal:nth-child(3) { transition-delay: 140ms; }
.reveal-group > .reveal:nth-child(4) { transition-delay: 210ms; }
.reveal-group > .reveal:nth-child(5) { transition-delay: 280ms; }
.reveal-group > .reveal:nth-child(6) { transition-delay: 350ms; }
```

Trigger with `IntersectionObserver` at `threshold: 0.12`. Add `.visible` on enter. **Never replay on scroll-up.** Use `once: true` in the observer.

### Counter Animation

For metric displays (e.g., "42 orders automated today"):

```javascript
function animateCounter(el, target, duration = 1200) {
  const start = performance.now();
  const ease = t => 1 - Math.pow(1 - t, 4); // ease-out-quart
  function step(now) {
    const p = Math.min((now - start) / duration, 1);
    el.textContent = Math.round(ease(p) * target).toLocaleString();
    if (p < 1) requestAnimationFrame(step);
    else el.textContent = target.toLocaleString();
  }
  requestAnimationFrame(step);
}
```

Trigger via IntersectionObserver on the parent section.

### Page Transitions (Product App)

```css
.page-enter {
  opacity: 0;
  transform: translateY(4px);
}
.page-enter-active {
  opacity: 1;
  transform: translateY(0);
  transition: opacity 0.2s var(--ease-standard),
              transform 0.2s var(--ease-standard);
}
```

Sidebar stays static; only the main content area transitions.

### Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
  .reveal {
    opacity: 1;
    transform: none;
    transition: none;
  }
  .ops-feed .feed-scroll { animation: none; }
  .status-dot.active { animation: none; }
  * { transition-duration: 0.01ms !important; }
}
```

---

## 8. Responsive Behavior

### Breakpoints

| Name | Width | Key Changes |
|------|-------|-------------|
| Mobile | < 768px | Single column, hamburger nav, no product screenshot |
| Tablet | 768px – 1023px | 2-column grids, sidebar visible (icon rail) |
| Desktop | 1024px – 1179px | Full 3-column grids, full sidebar |
| Wide | ≥ 1180px | Centered at max-width, generous margins |

### Touch Targets

All interactive elements: minimum 44px hit area. Applies to buttons, nav items, and form controls. Small visual components (chips, dots) use invisible padding to meet this requirement.

### Collapsing Strategy

**Hero:**
- Desktop: `clamp(2.75rem, 2rem + 4vw, 4.5rem)` headline, product screenshot with perspective tilt visible
- Mobile: reduce to `2.25rem` headline, product screenshot **hidden** (performance and readability)

**Navigation:**
- Desktop: full horizontal bar with links + CTA
- Mobile (<768px): hamburger toggle, slide-down drawer, full-width links, 44px tap targets

**Feature cards:**
- Desktop: 3 columns
- Tablet: 2 columns
- Mobile: 1 column, full-width

**Section padding:**
- Desktop: `clamp(5rem, 10vw, 10rem)` vertical
- Mobile: `3.5rem` vertical (reduced but still generous)

**Sticky scroll storytelling:**
- Desktop: left column sticky, right scrolls
- Mobile: stacks vertically — no sticky behavior

**Tables (product app):**
- Desktop: full column set, sticky header
- Tablet: scroll-x with pinned first column
- Mobile: card-row view — each row becomes a card

### Mobile-First CSS Pattern

```css
/* Mobile base */
.feature-grid { grid-template-columns: 1fr; }

/* Tablet */
@media (min-width: 768px) {
  .feature-grid { grid-template-columns: repeat(2, 1fr); }
}

/* Desktop */
@media (min-width: 1024px) {
  .feature-grid { grid-template-columns: repeat(3, 1fr); }
}
```

---

## 9. Agent Prompt Guide

This section is written for AI coding agents (Cursor, Claude Code, Google Stitch, Lovable, v0, etc.). Use the patterns below as reference implementations. Do not deviate from the color values, weights, or radius values specified — they are non-negotiable.

### Quick Color Reference

```
Background (canvas):   #0f0f14
Surface 1 (cards):     #13131a
Surface 2 (panels):    #1a1a22
Surface 3 (hover):     #21212b
Surface 4 (active):    #2a2a35
Surface 5 (tooltips):  #35354a

Accent (teal):         #00D4AA
Accent hover:          #1AFFC4  (or brightness(1.15) on accent)
Accent dim:            rgba(0, 212, 170, 0.08)
Accent glow:           rgba(0, 212, 170, 0.12)

Text primary:          #e4e4e7
Text secondary:        #8b8b94
Text tertiary:         #5a5a65
Text faint:            #3a3a45

Border default:        rgba(255, 255, 255, 0.06)
Border strong:         rgba(255, 255, 255, 0.10)
Border vivid:          rgba(255, 255, 255, 0.16)
Border focus:          rgba(0, 212, 170, 0.50)

Success:               #34d399
Warning:               #F59E42
Error:                 #EF6461

Agent Procurement:     #00D4AA
Agent Production:      #5B8DEF
Agent Inventory:       #F59E42
Agent Sales:           #A47AE8
Agent Quality:         #EF6461
Agent Finance:         #E2B94B
```

### Google Fonts Import

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&family=Inter:wght@100..900&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
```

### CSS Custom Properties (Global)

```css
:root {
  /* Surfaces */
  --bg-base:     #0f0f14;
  --surface-1:   #13131a;
  --surface-2:   #1a1a22;
  --surface-3:   #21212b;
  --surface-4:   #2a2a35;
  --surface-5:   #35354a;

  /* Accent */
  --accent:       #00D4AA;
  --accent-dim:   rgba(0, 212, 170, 0.08);
  --accent-glow:  rgba(0, 212, 170, 0.12);

  /* Agent Colors */
  --agent-procurement: #00D4AA;
  --agent-production:  #5B8DEF;
  --agent-inventory:   #F59E42;
  --agent-sales:       #A47AE8;
  --agent-quality:     #EF6461;
  --agent-finance:     #E2B94B;

  /* Text */
  --text-primary:    #e4e4e7;
  --text-secondary:  #8b8b94;
  --text-tertiary:   #5a5a65;
  --text-faint:      #3a3a45;
  --text-inverse:    #0f0f14;

  /* Borders */
  --border-default:  rgba(255, 255, 255, 0.06);
  --border-strong:   rgba(255, 255, 255, 0.10);
  --border-vivid:    rgba(255, 255, 255, 0.16);
  --border-focus:    rgba(0, 212, 170, 0.50);

  /* Semantic */
  --success:  #34d399;
  --warning:  #F59E42;
  --error:    #EF6461;

  /* Typography */
  --font-display: 'Instrument Serif', Georgia, serif;
  --font-body:    'Inter', system-ui, sans-serif;
  --font-mono:    'JetBrains Mono', ui-monospace, monospace;

  /* Spacing */
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-6: 24px;
  --space-8: 32px;
  --space-12: 48px;

  /* Radius */
  --radius-sm: 6px;
  --radius-md: 10px;
  --radius-lg: 12px;

  /* Motion */
  --ease-out-expo: cubic-bezier(0.19, 1, 0.22, 1);
  --ease-standard: cubic-bezier(0.23, 1, 0.32, 1);
  --t-quick:  0.12s;
  --t-normal: 0.28s;
  --t-slow:   0.5s;
}
```

### Example Component Prompts

**Hero section (landing page):**
> "Create a hero section on `#0f0f14` background. Include a structural grid (1px lines, `rgba(255,255,255,0.04)`, 48px grid, opacity 0.3, radial-gradient mask fading to edges). Add SVG blur blobs: two ellipses with feGaussianBlur stdDeviation=64 in teal `rgba(0,212,170,0.12)` and blue `rgba(91,141,239,0.06)`. Headline: Instrument Serif, `clamp(2.75rem, 2rem + 4vw, 4.5rem)`, weight 400, `#e4e4e7`, letter-spacing -0.03em, line-height 1.05. Subheadline: Inter, 1.125rem, weight 420, `#8b8b94`, line-height 1.6. Two buttons: primary (`#00D4AA` bg, `#0f0f14` text, 6px radius, weight 590, padding 0.5rem 1.25rem, hover `filter: brightness(1.15)`) and ghost (transparent bg, `1px solid rgba(255,255,255,0.10)` border, `#8b8b94` text, same size). Below buttons: agent chip row showing 6 agent names in their respective colors at 8% opacity backgrounds. No emoji. No box-shadow on any element."

**Feature card grid:**
> "Build a 3-column card grid on `#0f0f14` background. Each card: `#13131a` bg, `1px solid rgba(255,255,255,0.06)` border, 10px radius, 1.5rem padding. Hover: `border-color rgba(255,255,255,0.16)`, `filter brightness(1.06)`. Apply mouse-tracking shine via `::before` with `mask-image: radial-gradient(400px circle at var(--mouse-x) var(--mouse-y), black, transparent 60%)`. Card icon: 36px, SVG custom path, agent color at full opacity. Card title: Inter 16px weight 590, `#e4e4e7`. Card body: Inter 14px weight 420, `#8b8b94`, line-height 1.6. No box-shadow."

**Agent decision card (live ops feed item):**
> "Create a live operations feed component: `#13131a` bg, `1px solid rgba(255,255,255,0.06)` border, 10px radius. Each item row has: JetBrains Mono 11px `#3a3a45` timestamp, agent chip (mono 9px uppercase, agent color at 8% bg), and Inter 13px weight 420 `#8b8b94` decision text. Animate the scroll container with a continuous upward CSS animation. Top and bottom fade via `mask-image: linear-gradient(transparent, black 15%, black 85%, transparent)`."

**Navigation bar:**
> "Create a sticky nav on `rgba(15,15,20,0.85)` with `backdrop-filter: blur(12px)`. Height 56px. Left: AOS hexagonal logo SVG (geometric hexagon, 6 vertices with subtle teal glow). Center: nav links at Inter 13px weight 510, `#8b8b94`, hover `#e4e4e7`. Right: ghost button + primary teal button. Bottom border: `1px solid rgba(255,255,255,0.06)`. Mobile: hide nav links, show hamburger (3 SVG lines at `rgba(255,255,255,0.16)`)."

**Dashboard stat row:**
> "Create a stats row of 4 cards. Each card: `#13131a` bg, `1px solid rgba(255,255,255,0.06)` border, 10px radius, 1.5rem padding. Value: JetBrains Mono 28px weight 500, `#e4e4e7`. Label: Inter 11px weight 510 uppercase letter-spacing 0.05em, `#5a5a65`. Delta: JetBrains Mono 12px — `#34d399` for positive, `#EF6461` for negative. Include 6px status dot with pulse animation for 'active' items."

**Comparison table:**
> "Create a feature comparison table. Background `#0f0f14`. Header row: Inter 11px weight 510 uppercase `#5a5a65`. AOS column header: `#00D4AA` text, 2px bottom border `#00D4AA`. AOS column cells: `rgba(0,212,170,0.04)` bg, `1px solid rgba(0,212,170,0.15)` left+right borders. Check marks: custom SVG path checkmark in `#34d399`. X marks: custom SVG path in `#3a3a45`. No box-shadow. Cell height 44px. JetBrains Mono for any numeric values."

### Iteration Guide for AI Agents

1. **Background is always `#0f0f14`** — never `#000000`, never `#111111`. The precise value matters.
2. **Body weight is 420, not 400** — load Inter variable and set `font-weight: 420`. This is what makes text readable on dark backgrounds.
3. **Hover = `filter: brightness()`** — never override `background-color` for hover states on buttons or cards.
4. **Borders are alpha-based, always** — use `rgba(255,255,255,N)` for all borders. This adapts to any surface without explicit overrides.
5. **Agent colors are semantic** — a teal chip means Procurement. An amber chip means Inventory. Never swap them for aesthetic reasons.
6. **No `border-radius: 9999px` on buttons or cards** — buttons are 6px, cards are 10px, modals are 12px. Hard stop.
7. **No `box-shadow` on cards** — borders only. If a shadow is needed (modal, dropdown), use the `--shadow-dialog` stack.
8. **JetBrains Mono for all data** — every number, ID, timestamp, currency value, quantity, and agent output must use the mono font.
9. **Font-feature-settings on Inter** — set `font-feature-settings: "cv01", "ss03"` globally on the `<body>`.
10. **No emoji, ever** — icon requirements are met by custom SVG paths only. Status is communicated via colored dots, agent chips, and badges.
11. **Structural grid on backgrounds** — hero and feature section backgrounds should include the `background-image` grid pattern at 0.3 opacity with radial-gradient mask.
12. **Serif only for marketing headlines** — Instrument Serif on the landing page hero and section titles. In the product app, use Inter or Satoshi for all headings.
13. **Section padding uses `clamp()`** — `clamp(5rem, 10vw, 10rem)` for landing page vertical rhythm. Never a fixed `padding: 80px`.
14. **Reduced motion respected** — every animation must have a `@media (prefers-reduced-motion: reduce)` override.
15. **The tagline is "Your factory runs itself."** — period included. Never rephrase this.

---

*This document is the law for all AOS UI surfaces. When in doubt, return to this file. When proposing changes, update this file first and get alignment before shipping components.*

*Last updated: 2026 · Applies to: getaos.ai (landing), app.getaos.ai (product), all marketing surfaces*
