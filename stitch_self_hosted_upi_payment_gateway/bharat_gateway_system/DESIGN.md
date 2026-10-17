---
name: Bharat Gateway System
colors:
  surface: '#f8f9ff'
  surface-dim: '#cbdbf5'
  surface-bright: '#f8f9ff'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#eff4ff'
  surface-container: '#e5eeff'
  surface-container-high: '#dce9ff'
  surface-container-highest: '#d3e4fe'
  on-surface: '#0b1c30'
  on-surface-variant: '#43474d'
  inverse-surface: '#213145'
  inverse-on-surface: '#eaf1ff'
  outline: '#74777e'
  outline-variant: '#c4c6ce'
  surface-tint: '#476080'
  primary: '#00162d'
  on-primary: '#ffffff'
  primary-container: '#0f2b48'
  on-primary-container: '#7a93b5'
  inverse-primary: '#afc8ed'
  secondary: '#006e2d'
  on-secondary: '#ffffff'
  secondary-container: '#7cf994'
  on-secondary-container: '#007230'
  tertiary: '#261000'
  on-tertiary: '#ffffff'
  tertiary-container: '#442100'
  on-tertiary-container: '#da7808'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#d2e4ff'
  primary-fixed-dim: '#afc8ed'
  on-primary-fixed: '#001c37'
  on-primary-fixed-variant: '#2f4867'
  secondary-fixed: '#7ffc97'
  secondary-fixed-dim: '#62df7d'
  on-secondary-fixed: '#002109'
  on-secondary-fixed-variant: '#005320'
  tertiary-fixed: '#ffdcc3'
  tertiary-fixed-dim: '#ffb77d'
  on-tertiary-fixed: '#2f1500'
  on-tertiary-fixed-variant: '#6e3900'
  background: '#f8f9ff'
  on-background: '#0b1c30'
  surface-variant: '#d3e4fe'
typography:
  headline-xl:
    fontFamily: Inter
    fontSize: 36px
    fontWeight: '700'
    lineHeight: 44px
  headline-xl-mobile:
    fontFamily: Inter
    fontSize: 28px
    fontWeight: '700'
    lineHeight: 36px
  headline-lg:
    fontFamily: Inter
    fontSize: 28px
    fontWeight: '600'
    lineHeight: 36px
  headline-lg-mobile:
    fontFamily: Inter
    fontSize: 22px
    fontWeight: '600'
    lineHeight: 28px
  headline-md:
    fontFamily: Inter
    fontSize: 20px
    fontWeight: '600'
    lineHeight: 28px
  headline-sm:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '600'
    lineHeight: 24px
  body-lg:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  body-md:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
  body-sm:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '400'
    lineHeight: 16px
  label-lg:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '500'
    lineHeight: 20px
  label-md:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '500'
    lineHeight: 16px
  label-sm:
    fontFamily: Inter
    fontSize: 11px
    fontWeight: '600'
    lineHeight: 14px
    letterSpacing: 0.04em
  currency-display:
    fontFamily: Inter
    fontSize: 32px
    fontWeight: '700'
    lineHeight: 40px
    letterSpacing: -0.02em
  currency-tabular:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '500'
    lineHeight: 20px
    letterSpacing: -0.01em
rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px
spacing:
  gutter: 1.5rem
  gutter-mobile: 0.75rem
  margin: 2rem
  margin-mobile: 1rem
  space-xs: 0.25rem
  space-sm: 0.5rem
  space-md: 1rem
  space-lg: 1.5rem
  space-xl: 2.5rem
---

## Brand & Style

This design system embodies institutional trust, infrastructural durability, and frictionless transaction speed. Designed specifically for Indian enterprise merchants, developers, and finance operations managing high-volume, self-hosted UPI payments, the aesthetic synthesizes the clean precision of global fintech leaders with the functional pragmatism required by Indian financial rails (NPCI, UPI AutoPay, dynamic QR, settlements, and VPA reconciliation).

The visual language balances **Corporate Modernism** with **Data-Dense Utility**:
- **Absolute Dependability:** Generous white space, rigorous tabular balance, and deep foundational navy tones that convey sovereign-grade security.
- **Immediate Feedback:** Instant visual recognition for UPI transaction states—unambiguous emerald green for credit success, balanced amber for bank-side queueing, and decisive vermilion for processing failures.
- **Engineered Restraint:** Avoid gratuitous gradients, novelty blurs, or skeuomorphic embellishments. Visual distinction is achieved through razor-sharp borders, exact spacing, and structural typography.

## Colors

The palette is engineered for prolonged operational focus, high legibility under dense transaction dashboards, and rapid risk assessment:

- **Primary (`#0f2b48`):** Deep Naval Slate. Represents stability, core infrastructure, primary action buttons, focused navigation rails, and dominant metric labels.
- **Secondary (`#16a34a`):** Emerald Success. Specifically tuned for Indian payment psychology where Green (`#16a34a`) signifies instant UPI confirmation, bank settlement completion, and terminal webhook successes.
- **Tertiary (`#d97706`):** Amber Processing / Warning. Handles intermediate transaction states (e.g., "Pending Bank Authorization", "VPA Validation In Progress", "Rate-limit Approaching").
- **Error / Failure (`#dc2626`):** Precision Vermilion. Reserved exclusively for failed payments, unauthorized VPAs, expired intent links, and settlement breaches.
- **Neutral Canvas (`#f8fafc` base, `#ffffff` card surface, `#e2e8f0` border):** Clean cool-gray and slate undertones that keep financial data distinct and legible without causing eye strain.

## Typography

The typography uses Inter across all viewports to ensure mechanical precision and legibility. For numbers, settlements, and UPI IDs:

- **Tabular Figures (`tnum`):** All ledger items, transaction amounts, timestamps, latency meters, and UPI reference numbers (RRN) must strictly render with OpenType `font-feature-settings: "tnum" 1, "cv05" 1`. This prevents column jitter during real-time streaming data updates.
- **Rupee Symbol Consistency:** Always prefix currency entries with standard `₹` followed by a non-breaking hair space or inline format (e.g., `₹12,48,930.50`), formatting large values in accordance with the Indian numbering standard (Lakhs and Crores) rather than Western Millions.
- **Hierarchy & Case:** Section and metric descriptors rely on uppercase micro-labels (`label-sm`) with subtle letter-spacing for effortless scanning across high-volume dashboards.

## Layout & Spacing

The layout is built upon an 8pt base grid implemented using a 12-column responsive fluid grid:

- **Desktop (1280px+):** 12-column layout with 24px (`1.5rem`) gutters and 32px (`2rem`) outer boundaries. High-density data tables, side navigation bars (fixed 260px), and dual-column ledger inspection drawers.
- **Tablet (768px – 1279px):** 8-column layout with 16px gutters and 24px margins. Side rails collapse into an icon drawer; metrics wrap into 2x2 grids.
- **Mobile (< 768px):** 4-column layout with 12px (`0.75rem`) gutters and 16px (`1rem`) margins. Navigation collapses to a bottom persistent app bar or sticky top bar with direct QR inspection and payment link generation triggers.

## Elevation & Depth

Visual hierarchy is maintained primarily via structural borders and subtle ambient surface differentiation rather than heavy drop shadows:

- **Base Layer (L0):** Background surface rendered in `#f8fafc`.
- **Card Surface (L1):** Pure `#ffffff` framed by a 1px solid slate border (`#e2e8f0`). No shadow in neutral state; hovering introduces an ultra-diffused ambient shadow: `0 2px 4px -1px rgba(15, 43, 72, 0.04), 0 4px 12px -2px rgba(15, 43, 72, 0.06)`.
- **Raised & Overlay Elements (L2 - Popovers, Dropdowns, Date Pickers):** Background `#ffffff`, framed by `#cbd5e1`, with elevated projection: `0 10px 15px -3px rgba(15, 43, 72, 0.08), 0 4px 6px -4px rgba(15, 43, 72, 0.04)`.
- **Modals & Drawer Sheets (L3):** Backdrop blur tinted with deep navy: `rgba(15, 43, 72, 0.45)` with backdrop filter `blur(4px)`. Centered dialog containers use `0 20px 25px -5px rgba(15, 43, 72, 0.12)`.

## Shapes

The design system enforces a calibrated "Soft" shape posture (`roundedness: 1`), keeping elements crisp, structured, and institutional:

- **Core Elements (Buttons, Inputs, Metric Tiles):** Standard border radius of `0.25rem` (4px).
- **Cards & Data Modules:** Medium radius of `0.5rem` (8px), preventing clinical harshness while preserving maximum space for dense table rows.
- **Status Pills & UPI Badges:** Full pill-shaped rounding (`9999px`) to immediately distinguish contextual status tags (e.g., `SUCCESS`, `PENDING`, `DISPUTED`) from actionable rectangular controls.

## Components

### Buttons
- **Primary Action:** Solid Navy (`#0f2b48`) fill with pure white text, 4px corner radius, font weight 500 (`label-lg` or `label-md`). Hover transitions to `#1a3d63`. Focus ring: 2px solid `#0f2b48` with a 2px offset in `#ffffff`.
- **Secondary / Ghost:** Transparent background with 1px border in `#cbd5e1`, text in `#0f2b48`. Hover fills to `#f1f5f9`.
- **Destructive:** Border and text in `#dc2626`, hovering to `#fee2e2`.

### Status Chips & Badges
- **UPI Success:** Background `#dcfce7`, text `#15803d`, 1px border `#bbf7d0`. Accompanied by a solid 6px emerald status dot.
- **UPI Processing / Queued:** Background `#fef3c7`, text `#b45309`, 1px border `#fde68a`.
- **Failed / Expired:** Background `#fee2e2`, text `#b91c1c`, 1px border `#fecaca`.

### Form Fields & Inputs
- **Base Style:** 1px border `#cbd5e1`, background `#ffffff`, 4px radius, padded with `0.5rem 0.75rem`. Text rendered in `body-md`.
- **Focus State:** 1px solid `#0f2b48` with a continuous `0 0 0 1px #0f2b48` halo; no fuzzy glow.
- **VPA Input:** Specialized dual-segment input with fixed leading `@` prefix icon and dedicated domain suffix selector dropdown (e.g., `@okaxis`, `@okhdfcbank`, `@icici`).

### Cards & Metrics
- **Metric Tile:** Pure white background, 1px `#e2e8f0` border, 8px radius. Contains uppercase `label-sm` title, large `currency-display` figure, and secondary comparison badge showing transaction volume changes.
- **Data Table Containers:** Framed by 1px slate borders, headers featuring a subdued slate fill (`#f8fafc`) with bolded `label-sm` labels, and rows separated by `1px solid #f1f5f9`.

### Specialized UPI Components
- **Dynamic UPI QR Drawer:** Fixed 240x240px white square, sharp 4px padding, crisp QR canvas with centered bank/gateway emblem, countdown expiration timer in tabular amber, and quick-copy string for Intent URL.
- **RRN / UTR Copy Anchor:** Clickable monospaced snippet displaying the 12-digit UPI reference number with a single-click copy confirmation tooltip.