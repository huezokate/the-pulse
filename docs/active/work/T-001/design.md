# Design — T-001: foundation-css-shell

## Approach: Single <style> block in <head>

All CSS in one `<style>` block in `<head>`. Sections ordered: root vars → reset → layout → component
styles → animations. This keeps the file self-contained and readable in order.

Rejected: external stylesheet — adds HTTP request, breaks single-file portability.
Rejected: CSS-in-JS / style tags per section — harder to audit, no real benefit here.

## Bottom Sheet Architecture

Two elements: `.sheet-overlay` (covers viewport) and `.sheet` (positioned above overlay).
Both receive `.open` class on trigger. Transitions on both elements simultaneously.

Sheet positioning: `position: fixed; bottom: 0; left: 50%; transform: translateX(-50%) translateY(Npx)`
Initial: translateY(20px), opacity: 0, pointer-events: none
Open: translateY(0), opacity: 1, pointer-events: all

The `translateX(-50%)` persists across both states — only Y and opacity change.
The sheet max-width matches app container (430px) so it appears "inside" the app.

Rejected: dialog element — limited browser support for the animation pattern we need.
Rejected: separate translate properties — only one transform allowed cleanly here; combining is correct.

## Body Scroll Lock

When sheet opens: `document.body.style.overflow = 'hidden'`
When sheet closes: `document.body.style.overflow = ''`
Simple, effective, no scrollbar compensation needed on mobile.

## Fixed Bottom Nav

`position: fixed; bottom: 0; left: 50%; transform: translateX(-50%); width: 100%; max-width: 430px`
App content gets `padding-bottom: 80px` to clear the nav.
`safe-area-inset-bottom` env var in nav padding for iPhone notch support.

Rejected: `position: sticky` — doesn't produce the "always visible" mobile nav behavior
on long pages. Fixed is the correct choice for a persistent nav bar.

## CSS Architecture Decision

All component styles in one block, ordered by document flow (top to bottom section order).
No BEM, no utility classes — straightforward selectors matching the component structure.
Color and spacing from CSS custom properties exclusively — no hardcoded hex in component styles
except for the corner card themes (which need in-scope theming per card background).

## Scroll Row

`overflow-x: auto; scrollbar-width: none` on scroll containers.
`::webkit-scrollbar { display: none }` for Safari.
Items: `flex-shrink: 0` to prevent compression.
Padding-bottom: 8px for momentum scroll visibility.
