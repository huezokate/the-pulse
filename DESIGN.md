# DESIGN.md — The Pulse
## Visual Design System

---

## Palette Origin

All accent colors are pulled from the **Sherwin-Williams Chinatown SF** palette —
photographed on Market Street's Chinatown corridor. The background and surfaces
use the warmest neutral from the same pull.

This palette is light, bright, and saturated. Not muted. Not pastel. Not dark.

---

## Color System

```css
:root {
  /* ── BRAND PALETTE (Sherwin-Williams SF Chinatown) ── */
  --stop:         #C0392B;   /* SW 6869 Stop        — deep Chinatown red    */
  --coral:        #E8756A;   /* SW 6598 Dishy Coral  — warm salmon           */
  --pink:         #C2527A;   /* SW 6860 Eros Pink    — berry, rich           */
  --calypso:      #1BAAB0;   /* SW 6950 Calypso      — bright SF bay teal    */
  --honied:       #F2E8D5;   /* SW 7106 Honied White — warm parchment        */

  /* ── SURFACES ── */
  --bg:           #F2E8D5;   /* Page background — Honied White               */
  --bg-warm:      #EDE0C8;   /* Slightly deeper warm, for section alternates */
  --surface:      #FFFFFF;   /* Card surface — pure white                    */
  --surface-tint: #FDF8F0;   /* Slightly warm white for secondary cards      */

  /* ── TEXT ── */
  --text-primary:   #1A1A1A; /* Near black — all body + headline text        */
  --text-secondary: #6B6B6B; /* Medium gray — labels, metadata, captions     */
  --text-muted:     #A0A0A0; /* Light gray — hints, disabled, timestamps     */
  --text-on-dark:   #F2E8D5; /* Honied White — text on colored backgrounds   */

  /* ── SEMANTIC ── */
  --open:         #1BAAB0;   /* Calypso — "open now" status                  */
  --soon:         #E8756A;   /* Dishy Coral — "opening soon" status          */
  --live:         #C0392B;   /* Stop red — live dot, urgent, active          */
  --community:    #C2527A;   /* Eros Pink — community/social actions         */
  --corner:       #E8756A;   /* Dishy Coral — corner crew program            */

  /* ── BORDERS ── */
  --border:       rgba(26, 26, 26, 0.10); /* Soft dark border, light surfaces */
  --border-warm:  rgba(192, 57, 43, 0.15); /* Warm red-tinted border          */

  /* ── SHADOWS ── */
  --shadow-card:  0 2px 12px rgba(26, 26, 26, 0.08);
  --shadow-sheet: 0 -4px 32px rgba(26, 26, 26, 0.16);
}
```

---

## Typography

```css
/* Import */
@import url('https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500&display=swap');

:root {
  --font-display: 'DM Serif Display', Georgia, serif;
  --font-body:    'DM Sans', system-ui, sans-serif;
}
```

### Type Scale

| Role | Font | Size | Weight | Color |
|---|---|---|---|---|
| Hero title | DM Serif Display | clamp(42px, 10vw, 72px) | 400 | `--text-primary` |
| Section heading | DM Serif Display | 22px | 400 | `--text-primary` |
| Story title | DM Serif Display | 16px | 400 | `--text-primary` |
| Stat number | DM Serif Display | 28px | 400 | varies by card |
| Body | DM Sans | 13px | 400 | `--text-secondary` |
| Label (eyebrow) | DM Sans | 10px | 500 | `--text-muted`, uppercase, 3px letter-spacing |
| Tag pill | DM Sans | 9px | 500 | themed |
| CTA / link | DM Sans | 11px | 500 | `--calypso` |
| Caption | DM Sans | 10px | 400 | `--text-muted` |

---

## Spacing & Layout

```css
:root {
  --page-px:    16px;   /* Horizontal page padding (mobile) */
  --gap-sm:     8px;
  --gap-md:     12px;
  --gap-lg:     20px;
  --gap-section: 32px;

  --radius-sm:  8px;
  --radius-md:  14px;
  --radius-lg:  18px;
  --radius-xl:  24px;
  --radius-pill: 100px;
}
```

---

## Components

### Stat Card
```
Background:     --surface (#FFFFFF)
Border:         1px solid --border
Border-radius:  --radius-md (14px)
Padding:        16px 14px
Shadow:         --shadow-card
Hover:          border-color: --calypso
Active (tap):   scale(0.97), 0.1s

Contents:
  Emoji icon    18px, margin-bottom 8px
  Number        DM Serif Display 28px, --text-primary (color varies by type)
  Label         DM Sans 10px, --text-muted, uppercase
  Delta         DM Sans 10px, --calypso (positive) or --coral (neutral)
```

Color overrides by type:
- Places Open → number: `--text-primary`
- Corners Active → number: `--corner` (#E8756A Dishy Coral)
- Events → number: `--text-primary`
- Outdoor % → number: `--stop` (#C0392B Stop red)

---

### Food Chip
```
Background:     --surface
Border:         1px solid --border
Border-radius:  --radius-sm (10px)
Padding:        10px 12px
Min-width:      120px
Flex-shrink:    0

States:
  Open:         border-color: rgba(27, 170, 176, 0.35) — calypso tint
  Opening soon: border-color: rgba(232, 117, 106, 0.35) — coral tint

Contents:
  Business name   12px, --text-primary
  Category        10px, --text-muted
  Status text     10px — --open (teal) or --soon (coral)
```

---

### Corner Card
```
Width:          200px (fixed, horizontal scroll)
Border-radius:  --radius-lg (18px)
Border:         1px solid --border
Background:     --surface
Overflow:       hidden
Hover:          border-color: --calypso, translateY(-2px), 0.2s

Image area:     200 x 130px — themed bg (see theme table below)
Info area:      12px padding

  Corner name:  DM Serif Display 13px, --text-primary
  Cross street: 10px, --text-muted
  Tag pill:     9px, 2px 8px padding, themed color
  UGC prompt:   9px, --calypso, flex row with 📷
```

#### Corner Visual Themes

| Theme | Bg gradient | Accent color | Tag style |
|---|---|---|---|
| glow | `#0D0020 → #1A0035` dark purple | `#B44FFF` | `rgba(180,79,255,0.15)` bg, `#C07AFF` text |
| plants | `#0A1F0A → #152E15` dark green | `#2DB870` | `rgba(45,184,112,0.15)` bg, `#3DD880` text |
| kids | `#2A1F08 → #3A2A10` warm dark | `#E8A83E` | `rgba(232,168,62,0.15)` bg, `#F0C060` text |
| CTA | `rgba(0,0,0,0.03)` | — | dashed, `--text-muted` |

Note: corner image areas are intentionally dark/moody — contrast against the warm light page bg.

---

### Story Card
```
Width:          260px (fixed, horizontal scroll)
Border-radius:  --radius-lg (18px)
Border:         1px solid --border
Background:     --surface
Padding:        16px
Hover:          border-color: --coral, background: rgba(232,117,106,0.04)

Contents:
  Year badge:   10px, --stop, uppercase, letter-spacing 1px
  Title:        DM Serif Display 16px, --text-primary, line-height 1.3
  Excerpt:      11px, --text-secondary, line-height 1.6
  CTA:          "Read the full story →" — 10px, --calypso
```

---

### Founder Card
```
Border-radius:  --radius-md (14px)
Border:         1px solid --border
Background:     --surface
Padding:        14px 12px
Text-align:     center
Hover:          border-color: --coral (Dishy Coral), background: rgba(232,117,106,0.04)

Contents:
  Icon emoji:   24px, margin-bottom 6px
  Name:         DM Serif Display 11px, --text-primary
  Type:         DM Sans 9px, --text-muted, margin-top 2px
```

---

### Tag / Pill
```css
.tag {
  display: inline-block;
  font-family: var(--font-body);
  font-size: 9px;
  font-weight: 500;
  padding: 3px 9px;
  border-radius: var(--radius-pill);
  letter-spacing: 0.3px;
}
/* Themed variants set background + color inline */
```

---

### Bottom Sheet
```
Overlay:        position fixed, inset 0
                background: rgba(26,26,26,0.50)
                transition: opacity 0.25s

Sheet:          position fixed, bottom 0, left 0, right 0
                background: --surface (#FFFFFF)
                border-radius: 20px 20px 0 0
                padding: 24px
                max-height: 70vh
                overflow-y: auto
                box-shadow: --shadow-sheet
                transform: translateY(20px) → translateY(0), 0.25s ease

Close button:   32px × 32px, border-radius 50%
                border: 1px solid --border
                background: --surface-tint
                position: absolute, top 16px, right 16px

Sheet title:    DM Serif Display 22px, --text-primary
Sheet subtitle: DM Sans 12px, --text-secondary, margin-bottom 20px

Detail row:
  display: flex, justify-content: space-between
  padding: 10px 0
  border-bottom: 1px solid --border
  Label: DM Sans 13px, --text-secondary
  Value: DM Sans 13px, --text-primary, font-weight 500
```

---

### Live Badge
```
Position:       absolute, top of hero, right side
Display:        inline-flex, align-items center, gap 6px
Font:           DM Sans 11px, --calypso, letter-spacing 1px

Dot:
  width/height: 6px
  border-radius: 50%
  background:   --calypso
  animation:    pulse 2s ease-in-out infinite
    0%,100% { opacity: 1; transform: scale(1) }
    50%      { opacity: 0.5; transform: scale(1.5) }
```

---

### Day / Night Toggle
```
Container:      display flex, width fit-content, margin 0 auto
                background: rgba(26,26,26,0.06)
                border: 1px solid --border
                border-radius: --radius-pill
                padding: 4px

Button:         padding 8px 20px, border-radius --radius-pill
                border: none, background: transparent
                font: DM Sans 13px, --text-secondary
                transition: 0.2s

Button.active:  background: --calypso
                color: --text-on-dark (#F2E8D5)
```

---

### Pentagon Chart
```
SVG size:       160 × 160px, centered in card
Viewbox:        0 0 150 150, cx=75, cy=75

Background rings:
  outer pentagon:   stroke rgba(26,26,26,0.08), stroke-width 0.8, fill none
  inner pentagon:   stroke rgba(26,26,26,0.05), stroke-width 0.8, fill none

Data polygon:
  fill:         rgba(27,170,176,0.18) — calypso tint
  stroke:       --calypso (#1BAAB0)
  stroke-width: 1.5

Axis labels:    DM Sans 9px, --text-muted
  Top:          "Arts"
  Top-right:    "Food"
  Bottom-right: "Music"
  Bottom-left:  "Community"
  Top-left:     "Sport"

Week nav arrows:
  border: 1px solid --border
  border-radius: 6px
  color: --text-muted
  hover: border-color --calypso, color --calypso
```

---

### Horizontal Scroll Rows
```css
.scroll-row {
  display: flex;
  gap: 12px;
  overflow-x: auto;
  padding-bottom: 8px;
  /* Hide scrollbar */
  scrollbar-width: none;
  -ms-overflow-style: none;
}
.scroll-row::-webkit-scrollbar { display: none; }
```

---

### Bottom Navigation
```
Position:       sticky, bottom 0
Background:     rgba(242,232,213,0.95) — honied white, translucent
                backdrop-filter: blur(10px)
Border-top:     1px solid --border
Display:        flex, justify-content: space-around
Padding:        10px 0 env(safe-area-inset-bottom, 16px)

Nav item:
  display: flex, flex-direction: column, align-items: center, gap 3px
  font: DM Sans 9px, --text-muted, uppercase, letter-spacing 0.5px
  cursor: pointer

  Icon: 20px emoji or Tabler icon
  Active: color --calypso
```

Tabs: ⚡ Pulse · 📍 Map · 📸 Corners · 📅 Events · 👤 Me

---

### Divider
```css
.divider {
  border: none;
  border-top: 1px solid var(--border);
  margin: 4px 0 24px;
}
```

---

### Neon Glow Animation (Glow Corner only)
```css
@keyframes glow-pulse {
  0%, 100% {
    box-shadow: 0 0 8px #B44FFF, 0 0 16px rgba(180,79,255,0.3);
  }
  50% {
    box-shadow: 0 0 18px #B44FFF, 0 0 36px rgba(180,79,255,0.5);
  }
}

.neon-circle {
  width: 56px; height: 56px;
  border: 2px solid #B44FFF;
  border-radius: 50%;
  animation: glow-pulse 2s ease-in-out infinite;
}
```

---

## Section Background Alternation

Alternate between `--bg` and `--bg-warm` for visual rhythm:

| Section | Background |
|---|---|
| Hero | `--bg` (#F2E8D5) |
| Stats + Activity | `--bg` |
| Food row | `--bg-warm` (#EDE0C8) |
| Corners | `--bg` |
| Stories | `--bg-warm` |
| Founders | `--bg` |

---

## Do Not

- ❌ Use dark backgrounds on the main page surface
- ❌ Use Inter, Roboto, Space Grotesk, or system-ui for display text
- ❌ Use purple gradients — purple is only for the Glow Corner card interior
- ❌ Use off-palette colors — every accent must trace to one of the 5 SW colors
- ❌ Use box shadows that are too heavy — keep them subtle (0.08 alpha max outside sheets)
- ❌ Use ALL CAPS for anything other than eyebrow labels
- ❌ Use `border-radius` >20px on cards (too bubbly, loses the editorial quality)

---

## Color Quick Reference

```
#C0392B  Stop           — live dot, outdoor stat, urgent states
#E8756A  Dishy Coral    — corner program, hover borders, opening soon
#C2527A  Eros Pink      — community/social accent, story hover
#1BAAB0  Calypso        — open status, primary interactive, links, CTAs
#F2E8D5  Honied White   — page background, text on dark surfaces
#FFFFFF  White          — card surfaces
#1A1A1A  Near black     — primary text
#6B6B6B  Mid gray       — secondary text
#A0A0A0  Light gray     — muted / hints
```

---

*Built at (un)common ground · Frontier Tower × Human+Tech Week 2026 · Kate Huezo Designs*
