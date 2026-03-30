# Renderer Reference

Spec for building the live interactive design system renderer.

The renderer is built as a standalone HTML file saved to the user's project directory
(e.g., `design-system-preview.html`). It is the primary feedback mechanism — always
show it before asking for feedback.

---

## Rendering approach

**Primary method: Write an HTML file and open in browser.**

1. Write the renderer as `design-system-preview.html` in the user's project root
   (or a temp directory if no project exists)
2. Open it in the user's default browser using the appropriate tool
3. After the design system is finalized, offer to delete this file

If a Visualizer/widget tool (e.g., `show_widget`) is available in your environment,
you may use that instead. But always default to the HTML file approach — it works
in every agent environment (Claude Code, Cursor, Copilot, Codex, etc.).

---

## Core requirements

### Structure
- Light/dark theme toggle at the top — clicking switches instantly, no reload
- All sections stacked vertically (no tabs, no hidden content)
- Page background should use the design system's bg color (not transparent)
- Google Fonts loaded via @import for the chosen font families
- Responsive: looks good from 375px to 1400px wide

### Sections — always include ALL of these

1. **Hero / editorial section** — shows display type at large size with eyebrow + subtext
2. **Color swatches** — all background layers + accents + semantic colors,
   **each with WCAG contrast ratio badge** (see contrast display section below)
3. **Typography scale** — all type sizes with actual fonts, labeled with size/role
4. **Navigation bar** — logo placeholder, nav links, CTA button
5. **Metric cards** — 2-3 stat cards with label, value, delta
6. **Content cards** — 2-3 cards appropriate to the user's project type
7. **Data table** — rows with badges, mono values, hover state
8. **Buttons** — primary, default, ghost, destructive
9. **Badges / tags** — success, warning, error, accent, neutral
10. **Text inputs** — with label, placeholder, focus state
11. **Toast / notification** — success and error variants, with dismiss icon
12. **Modal dialog** — with overlay, title, body text, action buttons
13. **Motion demo** — hoverable boxes that demonstrate timing + easing
14. **Mobile preview** — a 375px-wide container showing a card + type at mobile scale

### Theme implementation
Use CSS custom properties on the `.renderer` container, not on `:root`.
Switching theme = toggling a class. Example:

```css
.renderer.light { --bg: #faf9f7; --t1: #111111; ... }
.renderer.dark  { --bg: #000000; --t1: #f5f5f7; ... }
```

All component styles reference `var(--bg)`, `var(--t1)`, etc.
The toggle button JS just does:
```js
renderer.className = 'renderer ' + theme;
```

---

## Contrast ratio display

For each color swatch in the Color section, display the WCAG contrast ratio
against its most common pairing:

```
┌──────────────┐
│              │
│   #0a0a0a    │
│   bg-base    │
│              │
│  text-1: 18.2:1 ✓  │
│  text-2: 8.4:1 ✓   │
│  text-3: 4.1:1 ✗   │
└──────────────┘
```

Use these indicators:
- ✓ (green) — passes WCAG AA (≥4.5:1 for normal text, ≥3:1 for large text)
- ✗ (red) — fails WCAG AA

Calculate contrast in JS within the HTML file:
```js
function luminance(hex) {
  const rgb = [parseInt(hex.slice(1,3),16), parseInt(hex.slice(3,5),16), parseInt(hex.slice(5,7),16)];
  return rgb.map(c => {
    c = c / 255;
    return c <= 0.03928 ? c / 12.92 : Math.pow((c + 0.055) / 1.055, 2.4);
  }).reduce((a, c, i) => a + c * [0.2126, 0.7152, 0.0722][i], 0);
}
function contrast(hex1, hex2) {
  const l1 = luminance(hex1), l2 = luminance(hex2);
  const lighter = Math.max(l1, l2), darker = Math.min(l1, l2);
  return ((lighter + 0.05) / (darker + 0.05)).toFixed(1);
}
```

---

## Reference-specific components

Adapt the content card and hero based on the user's inspiration references.

### If Apple product pages cited
Hero section: full-width, centered, large display type (clamp 2.5rem–5rem),
tight letter-spacing (-0.03em), light weight subtext (font-weight: 300),
two CTA buttons side by side, generous padding (48px+).

### If Airbnb cited
Include a listing card grid (3 cards, auto-fit columns):
- Image placeholder area (aspect-ratio 4/3, colored background)
- Card body: title (500 weight), location + duration (secondary color), price (500 weight)
- 10-14px border radius on the cards
- Subtle hover: translateY(-2px) + border-color change, 100ms

### If Vercel cited
Include a deployment/data table:
- Monospace font for IDs, durations, branch names
- Status badges as pills (ready/building/error)
- Very thin borders (1px rgba at 6-10% opacity)
- Table header: uppercase, letter-spacing, tertiary color, 10px mono

### If Linear cited
Include a task/issue list:
- Dense rows, minimal padding (8-10px vertical)
- Priority indicators (colored dots or small badges)
- Assignee initials circle
- Keyboard shortcut hints in tertiary color

### If Stripe cited
Include a form + summary panel side by side:
- Form: labeled inputs, clean validation states
- Summary: line items, total, divider, primary CTA button
- Very restrained, functional, no decorative elements

### If no specific reference
Default to: navigation bar + metric cards + generic content cards + table + forms.

---

## CSS patterns to use

### Borders (always rgba, not flat hex)
```css
/* Dark */
--b0: rgba(255,255,255,0.06);   /* subtle */
--b1: rgba(255,255,255,0.10);   /* default */
--b2: rgba(255,255,255,0.18);   /* hover/strong */

/* Light */
--b0: rgba(0,0,0,0.06);
--b1: rgba(0,0,0,0.10);
--b2: rgba(0,0,0,0.16);
```

### Card pattern
```css
.card {
  background: var(--surface);
  border: 1px solid var(--b0);
  border-radius: [from tokens];
  padding: [from tokens];
  transition: transform 100ms ease-out, border-color 100ms ease-out;
}
.card:hover { transform: translateY(-2px); border-color: var(--b1); }
```

### Focus ring pattern
```css
.input:focus {
  border-color: var(--a1);
  box-shadow: 0 0 0 3px var(--a1s);  /* accent at 8-12% opacity */
  outline: none;
}
```

### Badge pattern (pill vs square)
- Status badges (running, ready, error) → pill, border-radius 20px
- Category/metadata badges → square, border-radius 2-4px, monospace font

### Typography pattern
```css
.display {
  font-family: var(--font-display);
  font-size: clamp(2rem, 5vw, 4rem);
  font-weight: 700;
  letter-spacing: -0.03em;
  line-height: 1.05;
}
.body-prose {
  font-size: 15px;
  font-weight: 300;
  line-height: 1.65;
  color: var(--t2);
}
.mono-data {
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--t2);
}
```

### Toast / notification pattern
```css
.toast {
  background: var(--surface);
  border: 1px solid var(--b1);
  border-left: 3px solid var(--color-success); /* or --color-danger */
  border-radius: [from tokens];
  padding: var(--space-3) var(--space-4);
  display: flex;
  align-items: center;
  gap: var(--space-3);
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
}
```

### Modal pattern
```css
.modal-overlay {
  background: rgba(0,0,0,0.6);
  backdrop-filter: blur(4px);
}
.modal {
  background: var(--surface);
  border: 1px solid var(--b1);
  border-radius: [from tokens, lg size];
  padding: var(--space-6);
  max-width: 480px;
  width: 90vw;
}
```

### Navigation bar pattern
```css
.nav {
  background: var(--bg);
  border-bottom: 1px solid var(--b0);
  padding: var(--space-3) var(--space-6);
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: sticky;
  top: 0;
  z-index: 100;
}
```

---

## Section label pattern

Use a consistent section label style throughout:
```css
.section-label {
  font-family: var(--font-mono);
  font-size: 10px;
  color: var(--t3);
  letter-spacing: 0.08em;
  text-transform: uppercase;
  margin-bottom: 14px;
  padding-bottom: 8px;
  border-bottom: 1px solid var(--b0);
}
```

---

## Mobile preview section

Include a section at the bottom that simulates a mobile viewport:

```css
.mobile-preview {
  max-width: 375px;
  margin: 0 auto;
  border: 1px solid var(--b1);
  border-radius: 20px;
  padding: var(--space-4);
  overflow: hidden;
}
```

Inside, show:
- A card component at mobile density
- Display type with mobile-scale clamp
- A button at full width (common mobile pattern)
- Input at full width

This helps the user see how their tokens hold up at small sizes without
leaving the renderer.

---

## Iteration renders

When re-rendering after feedback, always:
1. Keep the same section structure
2. Apply only the changed tokens
3. After the render, show a brief changelog:
   > "Changed: card border-radius 4px → 12px, background base #0d0d0f → #000000,
   >  body font DM Sans → Outfit 300"

This makes iteration legible — the user knows exactly what shifted.
