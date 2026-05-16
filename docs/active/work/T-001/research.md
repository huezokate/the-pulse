# Research — T-001: foundation-css-shell

## Project State

Greenfield. No existing code. Only assets are CLAUDE.md and DESIGN.md (spec documents).
No framework, no build system — vanilla single-file HTML/CSS/JS.

## Constraints from Spec

**File target**: `index.html` — single file, all CSS and JS inline.

**Fonts**: Google Fonts CDN — DM Serif Display (0;1 italic axes) + DM Sans (9..40, weights 300/400/500).
Preconnect hints required for fonts.gstatic.com.

**Colors**: 5-color SW Chinatown SF palette + surface colors + text scale + semantic + border + shadow.
CSS custom properties, all defined in :root.

**Layout**: Mobile-first. max-width: 430px, margin: 0 auto. No media queries needed for the prototype.
Page background: --bg (#F2E8D5). Scrollable body. Bottom nav: position fixed.

**Bottom sheet**: position fixed, left: 50%, transform: translateX(-50%), max-width: 430px.
Overlay: position fixed, inset: 0. Both transition on .open class toggle.

## Design Token Inventory (from DESIGN.md)

Brand palette: --stop, --coral, --pink, --calypso, --honied (5 colors)
Surfaces: --bg, --bg-warm, --surface, --surface-tint
Text: --text-primary, --text-secondary, --text-muted, --text-on-dark
Semantic: --open, --soon, --live, --community, --corner
Borders: --border, --border-warm
Shadows: --shadow-card, --shadow-sheet
Fonts: --font-display, --font-body
Spacing: --page-px, --gap-sm, --gap-md, --gap-lg, --gap-section
Radii: --radius-sm, --radius-md, --radius-lg, --radius-xl, --radius-pill

## Animations Required

- Live badge dot: pulse-dot keyframe (opacity + scale, 2s ease-in-out infinite)
- Neon circle (glow corner only): glow-pulse keyframe (box-shadow, 2s ease-in-out infinite)
- Bottom sheet: translateY(20px) → translateY(0) + opacity 0 → 1, 0.25s ease

## Section Background Alternation

Hero → --bg
Stats + Activity → --bg
Food → --bg-warm
Corners → --bg
Stories → --bg-warm
Founders → --bg

## Bottom Nav Constraints

position: fixed, bottom: 0, left: 50%, transform: translateX(-50%)
max-width: 430px, width: 100%
backdrop-filter: blur(10px), rgba(242,232,213,0.95) background
Content needs padding-bottom to clear nav

## No Assumptions Made

No state management beyond simple JS variables.
No localStorage, no sessionStorage, no cookies.
No external CSS frameworks.
