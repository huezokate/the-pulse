# CLAUDE.md — The Pulse
## Project Intelligence & Build Rules

---

## What This Is

**The Pulse** is a mobile-first community dashboard for the Mid-Market corridor of San Francisco (Market St, 5th to Van Ness). It surfaces real-time neighborhood activity: open businesses, corner crews, events, clubs, and local stories.

It pairs with **Adopt a Corner** — a community activation program where residents claim a street corner, show up Saturdays at noon, and collectively beautify it. Corners become content for The Pulse. The Pulse is home base for the corners.

Built for: **(un)common ground Hackathon · Frontier Tower × Human+Tech Week 2026**
Partners: BLICK Art Materials, Mid-Market Foundation, MMBA, Urban Alchemy

---

## Stack

- **Framework**: Vanilla HTML/CSS/JS (single file for hackathon portability) OR React
- **Fonts**: DM Serif Display (display) + DM Sans (body) — load from Google Fonts
- **Icons**: Tabler Icons outline webfont OR emoji (emoji preferred for hackathon speed)
- **Charts**: Vanilla SVG for the pentagon — no chart library needed
- **No backend**: All data is hardcoded JSON for the prototype
- **Deploy**: Netlify drop, Cloudflare Pages, or GitHub Pages

---

## Theme

**LIGHT & BRIGHT.** This is not a dark dashboard. The Pulse is warm, community-made, alive.

- Background: Honied White (`#F2E8D5`) — warm parchment, not white
- Surface cards: `#FFFFFF` with soft shadow
- Text: near-black (`#1A1A1A`) for primary, `#6B6B6B` for secondary
- All accent colors come from the SW Chinatown SF palette (see DESIGN.md)

The vibe: a community bulletin board that got a great designer. Not a tech product. Not a startup. Something that feels like it was made *by* the neighborhood, *for* the neighborhood.

---

## File Structure

```
/
├── index.html          # Single-file prototype (HTML + CSS + JS inline)
├── CLAUDE.md           # This file
├── DESIGN.md           # Color system, typography, component specs
└── data/
    └── mock.js         # All hardcoded data objects
```

---

## Data Model

### Business
```js
{
  id: "bubbles-bakery",
  name: "Bubbles Bakery",
  type: "cafe",               // cafe | restaurant | bar | retail | gallery
  isOpen: true,
  closesAt: "9pm",            // null if closed now
  opensAt: null,              // null if open now
  story: "Maria Tanaka moved from Osaka...",
  foundingYear: 2024,
  isFoundingPartner: false,
  emoji: "🧋"
}
```

### Corner
```js
{
  id: "glow-corner",
  name: "Market & 7th",
  nickname: "The Glow Corner",
  theme: "glow",              // glow | plants | kids | music | ...
  tagLabel: "Blacklight Art",
  tagEmoji: "🌟",
  crewSize: 8,
  meetupDay: "Saturday",
  meetupTime: "12pm",
  ugcCount: 47,
  bestTime: "After 8pm",
  story: "Team Glow claims the corner every Saturday...",
  ugcPrompt: "Share your glow photo"
}
```

### Event
```js
{
  id: "jazz-chapel",
  title: "Jazz at The Chapel",
  time: "7pm",
  isDay: false,
  isNight: true,
  category: "music",          // arts | food | music | community | sport
  location: "The Chapel",
  isFree: false,
  emoji: "🎷"
}
```

### Week (Pentagon)
```js
{
  weekLabel: "May 12–18",
  arts: 70,
  food: 85,
  music: 60,
  community: 90,
  sport: 45,
  // svgPoints computed from these values at render time
}
```

---

## Section Map (Render Order)

1. **Hero** — title, live badge, day/night toggle
2. **Stats Row** — 4 cards: Places Open, Corners Active, Events, Outdoor %
3. **Activity Row** — Pentagon chart (left) + Mini widgets (right): Indoor/Outdoor bar, Active Clubs
4. **Food Open Now** — horizontal scroll chips
5. **Our Corners** — horizontal scroll corner cards
6. **Neighborhood Stories** — horizontal scroll editorial cards
7. **Founding Partners** — 3-column grid
8. **Bottom Navigation** — sticky: Pulse · Map · Corners · Events · Me

---

## Day / Night Toggle Behavior

| Element | Day | Night |
|---|---|---|
| Events stat label | "Events today" | "Events tonight" |
| Events delta | "2 tonight" | "3 still going" |
| Outdoor % | 71% | 38% |
| Food section label | "🍳 Food open now" | "🍺 Open tonight" |

---

## Interaction Pattern: Bottom Sheet

Every tappable card opens a bottom sheet. Build this as a **single reusable component** first.

```
Overlay: position fixed, inset 0, rgba(0,0,0,0.5) backdrop
Sheet: slides up from bottom, border-radius 20px top corners
       background: #FFFFFF, max-height 70vh, overflow-y auto
Close: tap ✕ button OR tap outside the sheet
Animation: sheet translateY +20px → 0, opacity 0 → 1, duration 0.25s ease
```

Sheet anatomy:
- `✕` close button — top right
- Title — DM Serif Display 22px
- Subtitle — 12px secondary text
- Body rows — label (left) + value (right), border-bottom between rows

---

## Pentagon Chart

SVG-based. No library. Compute polygon points from 5 axis values (0–100).

```js
function pentaPoints(arts, food, music, community, sport, cx=75, cy=75, r=60) {
  const angles = [-90, -18, 54, 126, 198]; // top, then clockwise
  const values = [arts, food, music, community, sport];
  return values.map((v, i) => {
    const a = angles[i] * Math.PI / 180;
    const scale = v / 100;
    return `${cx + r * scale * Math.cos(a)},${cy + r * scale * Math.sin(a)}`;
  }).join(' ');
}
```

Axes order (clockwise from top): Arts · Food · Music · Community · Sport

---

## Corner Card Visual Themes

| Theme | Background | Key Visual | Tag Color |
|---|---|---|---|
| glow | `#0D0020` dark purple | Animated neon circle, UV ACTIVE text | `#B44FFF` purple |
| plants | `#0A1F0A` dark green | 🌿 emoji large | `#2BA868` green |
| kids | `#1A1A0A` warm dark | 🎨 emoji large | `#E8A83E` gold |
| [empty CTA] | Barely visible | Dashed + circle | Fog gray |

---

## Bottom Sheet Inventory

| Trigger | Sheet Title | Key Content |
|---|---|---|
| Places Open card | "Open right now" | Breakdown: cafés 6, restaurants 5, bars soon, retail 3 |
| Corners Active card | "Active corner crews" | List of 6 corners, next meetup, $50/mo city grant |
| Events card | "Events today/tonight" | List with times |
| Outdoor % card | "Outdoor vs Indoor" | %, weather, top spots |
| Active Clubs widget | "Active clubs" | Running Club live, Scavenger Hunt, Night Run, etc. |
| Glow Corner card | "Market & 7th · Glow Corner" | Type, best time, crew, UGC count, wear white tip |
| Garden Corner card | "Market & 9th · Garden Corner" | Plants, how to contribute |
| Kids Corner card | "Market & 6th · Chalk Corner" | Bring chalk, weekly theme |
| Adopt CTA | "Adopt a corner" | Program details, $50 reimbursement, BLICK kits |
| Any story card | Story name | Full text + business details |
| Any founder card | Partner name | Story + contribution |
| Join Founders slot | "Become a founding partner" | Tiers, benefits, contact email |

---

## Do Not

- ❌ Use a dark background — this is a LIGHT, WARM theme
- ❌ Use Inter, Roboto, or system-ui as the display font
- ❌ Use purple gradients or generic "tech dashboard" aesthetics
- ❌ Build a backend or auth system for the hackathon
- ❌ Use a charting library for the pentagon — SVG only
- ❌ Use localStorage or sessionStorage
- ❌ Forget the day/night toggle — it's a key interaction

---

## Voice & Copy Tone

- Community-made, not corporate
- Warm, specific, human — "Jon's Bar has poured every decade Market Street has lived through"
- No startup jargon. No "leverage synergies."
- Stories are written like a neighborhood paper, not a press release
- Labels are lowercase or sentence case — never ALL CAPS except for the eyebrow labels

---

*Built at (un)common ground · Frontier Tower × Human+Tech Week 2026 · Kate Huezo Designs*
