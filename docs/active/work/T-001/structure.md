# Structure — T-001: foundation-css-shell

## Files

### Created
- `index.html` — single file prototype shell

### Not created (T-002)
- `data/mock.js` — separate ticket

## index.html Structure

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="...">
  <title>The Pulse — Mid-Market SF</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="...DM+Serif+Display+DM+Sans..." rel="stylesheet">
  <style>
    /* 1. :root CSS custom properties */
    /* 2. Reset & base */
    /* 3. .app layout container */
    /* 4. Hero */
    /* 5. Stats grid */
    /* 6. Activity row */
    /* 7. Scroll rows */
    /* 8. Food chips */
    /* 9. Corner cards + themes */
    /* 10. Story cards */
    /* 11. Founder grid */
    /* 12. Bottom nav */
    /* 13. Bottom sheet */
    /* 14. Animations */
  </style>
</head>
<body>
  <div class="app">
    <!-- Hero (T-003) -->
    <!-- Stats (T-003) -->
    <!-- Activity (T-003) -->
    <!-- Food (T-003) -->
    <!-- Corners (T-003) -->
    <!-- Stories (T-003) -->
    <!-- Founders (T-003) -->
    <!-- Bottom Nav (T-003) -->
  </div>
  <!-- Sheet overlay -->
  <div class="sheet-overlay" id="overlay"></div>
  <div class="sheet" id="sheet">
    <button class="sheet-close">✕</button>
    <div class="sheet-title" id="sheet-title"></div>
    <div class="sheet-subtitle" id="sheet-subtitle"></div>
    <div id="sheet-content"></div>
  </div>
  <script>
    /* T-004 JS goes here */
  </script>
</body>
</html>
```

## CSS Sections (detailed)

`:root` — all design tokens (~40 vars)
`html, body` — scroll, background, font, antialiasing
`.app` — max-width 430px, margin auto, padding-bottom 80px
Hero — .hero, .hero-eyebrow, .hero-title, .hero-sub, .live-badge, .live-dot, .toggle-wrap, .toggle-btn
Stats — .stats-section, .stats-grid, .stat-card, .stat-icon, .stat-number, .stat-label, .stat-delta
Activity — .activity-section, .activity-row, .activity-card, .pentagon-card, .pentagon-nav, .pentagon-week,
           .pentagon-arrow, .pentagon-svg-wrap, .widgets-col, .widget-card, .widget-label,
           .io-bar-row, .io-bar-label, .io-bar-track, .io-bar-fill, .club-item, .club-name, .club-badge
Scroll rows — .section, .section-bg-warm, .section-header, .section-title, .section-cta, .divider, .scroll-row
Food — .food-chip, .food-name, .food-cat, .food-status
Corners — .corner-card, .corner-img (+ .glow .plants .kids .cta), .neon-circle, .corner-emoji-big,
          .uv-label, .corner-cta-inner, .cta-circle, .corner-info, .corner-name, .corner-cross, .tag, .corner-ugc
Stories — .story-card, .story-year, .story-title, .story-excerpt, .story-cta
Founders — .founders-grid, .founder-card, .founder-icon, .founder-name, .founder-type, .founder-join
Bottom nav — .bottom-nav, .nav-item, .nav-item.active, .nav-icon
Bottom sheet — .sheet-overlay, .sheet-overlay.open, .sheet, .sheet.open, .sheet-close, .sheet-title,
               .sheet-subtitle, .sheet-row, .sheet-row-label, .sheet-row-value, .sheet-body
Animations — @keyframes pulse-dot, @keyframes glow-pulse
