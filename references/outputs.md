# Outputs Reference

Exact formats for all output files produced by this skill.

---

## 1. TASTE.md

Plain-language aesthetic brief. Human-readable. The *why* behind the tokens.

```markdown
# TASTE.md — Personal Design Brief
_v{version} · Updated {date}_

## Project context
Primarily building: {project types}

## Aesthetic direction
{1-2 paragraphs describing the core aesthetic direction and feel.
Should be specific enough that a designer could execute it without seeing the tokens.}

## Inspiration references
{For each reference provided by the user:}
- **{Name/URL}** — {what the user loves about it} → signals: {extracted signals}

## Shared signals across references
{2-3 bullet points: the things all references have in common}

## Color
- Mood: {dark/light/both}
- Strategy: {one accent / two accents / monochrome}
- Never: {specific colors or approaches to avoid}

## Typography
- Display: {font name + feel description}
- Body: {font name + weight + leading notes}
- Mono: {font name + when to use it}
- Never: {specific fonts or approaches to avoid}

## Shape & form
- Border radius: {value + rationale}
- Borders: {weight, opacity approach, rationale}
- Shadows: {use or avoid, and why}

## Motion
- Duration: {value + feel description}
- Easing: {curve + rationale}
- Never: {animation patterns to avoid}

## Density
{Description of intended information density with rationale}

## Responsive behavior
- Mobile spacing: {reduction strategy, e.g., "reduce by 25%"}
- Mobile typography: {how the scale adapts}
- Touch targets: {minimum size for interactive elements}

## The gap (words vs references)
{Only include if there was a meaningful gap between what the user said and
what their references revealed. E.g., "User said 'minimal' but references
are actually editorial — we went with editorial."}

## Anti-patterns
Things an agent must NEVER do when building with this design system:
- {anti-pattern 1}
- {anti-pattern 2}
- {anti-pattern 3}
...

## What makes this memorable
{1 sentence: the one thing that will make UIs built with this system stand out}
```

---

## 2. tokens.json

Structured token file. Machine-readable. The *what*.

```json
{
  "_meta": {
    "version": "1.0.0",
    "created": "{ISO date}",
    "updated": "{ISO date}",
    "taste": "TASTE.md",
    "changelog": [
      { "version": "1.0.0", "date": "{date}", "notes": "Initial design system" }
    ]
  },

  "theme": {
    "dark": {
      "color": {
        "background": {
          "base":     "{hex}",
          "surface":  "{hex}",
          "elevated": "{hex}",
          "overlay":  "{hex}"
        },
        "border": {
          "subtle":   "rgba(255,255,255,{opacity})",
          "default":  "rgba(255,255,255,{opacity})",
          "strong":   "rgba(255,255,255,{opacity})"
        },
        "text": {
          "primary":   "{hex}",
          "secondary": "{hex}",
          "muted":     "{hex}",
          "inverse":   "{hex}"
        },
        "accent": {
          "primary":          "{hex}",
          "primary-dim":      "{hex}",
          "primary-subtle":   "rgba({r},{g},{b},{opacity})",
          "secondary":        "{hex}",
          "secondary-dim":    "{hex}",
          "secondary-subtle": "rgba({r},{g},{b},{opacity})"
        },
        "semantic": {
          "success": "{hex}",
          "warning": "{hex}",
          "danger":  "{hex}",
          "info":    "{hex}"
        }
      },
      "_contrast": {
        "text-primary-on-base":    "{ratio}:1",
        "text-secondary-on-base":  "{ratio}:1",
        "text-primary-on-surface": "{ratio}:1",
        "accent-on-base":          "{ratio}:1",
        "notes": "All ratios must meet WCAG AA: ≥4.5:1 for normal text, ≥3:1 for large text"
      }
    },
    "light": {
      "color": {
        "background": {
          "base":     "{hex — warm off-white, never #ffffff}",
          "surface":  "#ffffff",
          "elevated": "{hex}",
          "overlay":  "{hex}"
        },
        "border": {
          "subtle":   "rgba(0,0,0,{opacity})",
          "default":  "rgba(0,0,0,{opacity})",
          "strong":   "rgba(0,0,0,{opacity})"
        },
        "text": {
          "primary":   "{hex — near black, not pure black}",
          "secondary": "{hex}",
          "muted":     "{hex}",
          "inverse":   "#ffffff"
        },
        "accent": {
          "primary":          "{hex — ~15-20% darker than dark theme accent}",
          "primary-dim":      "{hex}",
          "primary-subtle":   "rgba({r},{g},{b},{opacity})",
          "secondary":        "{hex}",
          "secondary-dim":    "{hex}",
          "secondary-subtle": "rgba({r},{g},{b},{opacity})"
        },
        "semantic": {
          "success": "{hex — accessible on white}",
          "warning": "{hex}",
          "danger":  "{hex}",
          "info":    "{hex}"
        }
      },
      "_contrast": {
        "text-primary-on-base":    "{ratio}:1",
        "text-secondary-on-base":  "{ratio}:1",
        "text-primary-on-surface": "{ratio}:1",
        "accent-on-base":          "{ratio}:1",
        "notes": "All ratios must meet WCAG AA: ≥4.5:1 for normal text, ≥3:1 for large text"
      }
    }
  },

  "shared": {
    "typography": {
      "family": {
        "display": "'{Font}', {fallback}, sans-serif",
        "body":    "'{Font}', {fallback}, sans-serif",
        "mono":    "'{Font}', {fallback}, monospace"
      },
      "scale": {
        "xs":      "0.75rem",
        "sm":      "0.8125rem",
        "base":    "0.875rem",
        "md":      "1rem",
        "lg":      "1.125rem",
        "xl":      "1.375rem",
        "2xl":     "1.75rem",
        "3xl":     "2.25rem",
        "display": "clamp({min}, {vw}, {max})"
      },
      "weight": {
        "light":    "300",
        "normal":   "400",
        "medium":   "500",
        "semibold": "600",
        "bold":     "700"
      },
      "leading": {
        "tight":   "1.1",
        "snug":    "1.35",
        "normal":  "1.6",
        "relaxed": "1.75"
      },
      "tracking": {
        "tightest": "-0.04em",
        "tight":    "-0.02em",
        "normal":   "0",
        "wide":     "0.04em",
        "widest":   "0.12em"
      }
    },
    "spacing": {
      "1": "4px",   "2": "8px",   "3": "12px",  "4": "16px",
      "5": "20px",  "6": "24px",  "8": "32px",  "10": "40px",
      "12": "48px", "16": "64px", "20": "80px",  "24": "96px"
    },
    "radius": {
      "none": "0px",
      "xs":   "2px",
      "sm":   "{from tokens}",
      "md":   "{from tokens}",
      "lg":   "{from tokens}",
      "xl":   "{from tokens}",
      "full": "9999px"
    },
    "shadow": {
      "none":   "none",
      "sm":     "{if used — otherwise omit}",
      "policy": "{borders preferred / shadows preferred / mixed}"
    },
    "motion": {
      "duration": {
        "instant": "75ms",
        "fast":    "100ms",
        "normal":  "150ms",
        "slow":    "300ms"
      },
      "easing": {
        "default":   "ease-out",
        "enter":     "ease-out",
        "exit":      "ease-in",
        "emphasis":  "cubic-bezier(0.34, 1.56, 0.64, 1)"
      }
    },
    "breakpoints": {
      "sm":  "640px",
      "md":  "768px",
      "lg":  "1024px",
      "xl":  "1280px",
      "2xl": "1536px"
    },
    "responsive": {
      "mobile-spacing-scale": 0.75,
      "min-touch-target": "44px",
      "notes": "Below sm breakpoint, apply mobile-spacing-scale to spacing tokens"
    }
  }
}
```

When iterating, always bump the version and add a changelog entry:
```json
{ "version": "1.2.0", "date": "{date}", "notes": "Warmer light bg, 12px card radius, switched to Geist display" }
```

---

## 3. tokens.css

Ready-to-paste CSS custom properties. The *how*.

```css
/* Design System Tokens — v{version} */
/* Generated from tokens.json · See TASTE.md for rationale */

/* === SHARED === */
:root {
  /* Typography */
  --font-display: '{Font}', {fallback}, sans-serif;
  --font-body:    '{Font}', {fallback}, sans-serif;
  --font-mono:    '{Font}', {fallback}, monospace;

  /* Type scale */
  --text-xs:      0.75rem;
  --text-sm:      0.8125rem;
  --text-base:    0.875rem;
  --text-md:      1rem;
  --text-lg:      1.125rem;
  --text-xl:      1.375rem;
  --text-2xl:     1.75rem;
  --text-3xl:     2.25rem;
  --text-display: clamp({min}, {vw}, {max});

  /* Font weights */
  --weight-light:    300;
  --weight-normal:   400;
  --weight-medium:   500;
  --weight-semibold: 600;
  --weight-bold:     700;

  /* Leading */
  --leading-tight:   1.1;
  --leading-snug:    1.35;
  --leading-normal:  1.6;
  --leading-relaxed: 1.75;

  /* Tracking */
  --tracking-tightest: -0.04em;
  --tracking-tight:    -0.02em;
  --tracking-normal:   0;
  --tracking-wide:     0.04em;
  --tracking-widest:   0.12em;

  /* Spacing */
  --space-1:  4px;   --space-2:  8px;   --space-3:  12px;  --space-4:  16px;
  --space-5:  20px;  --space-6:  24px;  --space-8:  32px;  --space-10: 40px;
  --space-12: 48px;  --space-16: 64px;  --space-20: 80px;  --space-24: 96px;

  /* Border radius */
  --radius-none: 0px;
  --radius-xs:   2px;
  --radius-sm:   {value};
  --radius-md:   {value};
  --radius-lg:   {value};
  --radius-xl:   {value};
  --radius-full: 9999px;

  /* Motion */
  --dur-instant: 75ms;
  --dur-fast:    100ms;
  --dur-normal:  150ms;
  --dur-slow:    300ms;
  --ease-default:  ease-out;
  --ease-enter:    ease-out;
  --ease-exit:     ease-in;

  /* Responsive */
  --min-touch-target: 44px;
}

/* === DARK THEME (default) === */
:root,
[data-theme="dark"] {
  --bg:         {hex};
  --surface:    {hex};
  --elevated:   {hex};
  --overlay:    {hex};

  --border-0:   rgba(255,255,255,{op});
  --border-1:   rgba(255,255,255,{op});
  --border-2:   rgba(255,255,255,{op});

  --text-1:     {hex};
  --text-2:     {hex};
  --text-3:     {hex};
  --text-inv:   {hex};

  --accent-1:      {hex};
  --accent-1-dim:  {hex};
  --accent-1-sub:  rgba({r},{g},{b},{op});
  --accent-2:      {hex};
  --accent-2-dim:  {hex};
  --accent-2-sub:  rgba({r},{g},{b},{op});

  --color-success: {hex};
  --color-warning: {hex};
  --color-danger:  {hex};
  --color-info:    {hex};
}

/* === LIGHT THEME === */
[data-theme="light"],
@media (prefers-color-scheme: light) {
  :root:not([data-theme="dark"]) {
    --bg:         {hex};
    --surface:    #ffffff;
    --elevated:   {hex};
    --overlay:    {hex};

    --border-0:   rgba(0,0,0,{op});
    --border-1:   rgba(0,0,0,{op});
    --border-2:   rgba(0,0,0,{op});

    --text-1:     {hex};
    --text-2:     {hex};
    --text-3:     {hex};
    --text-inv:   #ffffff;

    --accent-1:      {hex};
    --accent-1-dim:  {hex};
    --accent-1-sub:  rgba({r},{g},{b},{op});
    --accent-2:      {hex};
    --accent-2-dim:  {hex};
    --accent-2-sub:  rgba({r},{g},{b},{op});

    --color-success: {hex};
    --color-warning: {hex};
    --color-danger:  {hex};
    --color-info:    {hex};
  }
}

/* === MOBILE RESPONSIVE === */
@media (max-width: 640px) {
  :root {
    --space-4:  12px;
    --space-5:  16px;
    --space-6:  20px;
    --space-8:  24px;
    --space-10: 32px;
    --space-12: 40px;
    --space-16: 48px;
    --space-20: 64px;
    --space-24: 80px;
  }
}
```

---

## 4. agent-prompt.md

A ready-made snippet the user pastes at the start of any new project conversation.
This gives the agent their full design system as a hard constraint, with active
guardrails against falling back to generic defaults.

```markdown
# Design System

Before building anything, read and apply this design system completely.
Make NO design decisions outside of these tokens. You implement; you don't design.

## Critical guardrails — read before writing ANY CSS or markup

Before outputting any color hex, font-family, border-radius, or spacing value,
verify it comes from the tokens below. If you cannot find an appropriate token,
ASK THE USER — do not invent a value.

Specifically, NEVER:
- Use a color hex not listed in the tokens (no #3b82f6, no #6366f1, no #e5e7eb)
- Use Inter, Roboto, Arial, system-ui, or sans-serif as a font-family
- Use Tailwind default colors (bg-blue-500, text-gray-400, etc.) without mapping
  them to token values first
- Use a border-radius value not from the radius scale
- Use padding/margin values not from the spacing scale
- Add drop shadows unless the shadow policy below says "shadows preferred"
- Use purple-to-blue gradients anywhere

If you catch yourself about to write something generic, stop and check the tokens.

## Aesthetic brief
{Paste the core paragraph from TASTE.md — 2-3 sentences capturing the feel}

## Anti-patterns — NEVER do these
{Paste the anti-patterns list from TASTE.md — 5-10 bullets}

## Tokens (use these exactly)

### Typography
- Display font: {font name} — use for all headlines and hero text
- Body font: {font name} — use for all prose and UI labels
- Mono font: {font name} — use for code, data values, metadata
- Load from Google Fonts: {Google Fonts URL with all weights needed}
- Use `font-display: swap` on all @font-face rules

### Colors — Dark theme
- Page background: {hex}
- Card/surface: {hex}
- Elevated surface: {hex}
- Text primary: {hex} (contrast on base: {ratio}:1)
- Text secondary: {hex} (contrast on base: {ratio}:1)
- Text muted: {hex}
- Border subtle: {rgba}
- Border default: {rgba}
- Accent 1 (primary): {hex}
- Accent 2 (secondary): {hex}
- Success: {hex} / Warning: {hex} / Danger: {hex}

### Colors — Light theme
- Page background: {hex}
- Card/surface: #ffffff
- Elevated surface: {hex}
- Text primary: {hex} (contrast on base: {ratio}:1)
- Text secondary: {hex} (contrast on base: {ratio}:1)
- Text muted: {hex}
- Border subtle: {rgba}
- Border default: {rgba}
- Accent 1 (primary): {hex}
- Accent 2 (secondary): {hex}
- Success: {hex} / Warning: {hex} / Danger: {hex}

### Shape & motion
- Card border radius: {value}
- Button border radius: {value}
- Input border radius: {value}
- Default transition: all {duration} {easing}
- Shadow policy: {borders preferred / shadows preferred / mixed}

### Spacing scale
4 · 8 · 12 · 16 · 20 · 24 · 32 · 40 · 48 · 64 · 80 · 96 px
On mobile (< 640px), reduce spacing by 25% for space-4 and above.

### Responsive rules
- Display type uses clamp() — already fluid, no breakpoint overrides needed
- Minimum touch target: 44px on mobile
- Cards go single-column below md breakpoint
- Navigation collapses to hamburger below md breakpoint

### Implementation rules
1. Implement light/dark toggle using [data-theme] attribute on <html>
2. Use CSS custom properties — do not hardcode any color hex values
3. Cards get 1px border at --border-0, hover shifts to --border-1
4. Focus states: border-color --accent-1 + box-shadow 0 0 0 3px --accent-1-sub
5. Buttons: primary uses --accent-1 bg with white text; default uses --elevated bg
6. All badge/tag text must use a color from the same hue family as its background
7. Data/numbers use the mono font
8. Section labels: uppercase, letter-spacing 0.08em, --text-3 color, 10px mono
9. All text/background combinations must meet WCAG AA contrast (≥4.5:1)
10. Use the spacing scale — no arbitrary padding/margin values

The full token file is at tokens.json. The rationale is in TASTE.md.
```

---

## 5. Integration Output

When integrating into an existing project, the agent should provide:

### Integration Summary File: `INTEGRATION.md`

Create this file in the project root to document what was changed:

```markdown
# Design System Integration
_Integrated: {date}_

## Project Type
{Framework + styling solution}

## Files Modified
- `{file path}` — {what was changed}
- `{file path}` — {what was changed}

## Design System Applied
- Version: {from tokens.json}
- Fonts: {display}, {body}, {mono}
- Primary: {color}
- Secondary: {color}
- Contrast: All text passes WCAG AA (≥4.5:1)

## Usage
```css
/* Use these classes */
.font-display — headlines and hero text
.font-body — body text (default)
.font-mono — code and data
.section-label — uppercase metadata labels
```

## Theme Toggle
To toggle themes, add this to your HTML:
```html
<button onclick="toggleTheme()">Toggle Theme</button>
<script>
function toggleTheme() {
  const html = document.documentElement;
  const current = html.getAttribute('data-theme');
  html.setAttribute('data-theme', current === 'dark' ? 'light' : 'dark');
}
</script>
```

## Original Files
Backup of original files saved to: `.design-system-backup/{date}/`

## Next Steps
1. Run dev server: `{command}`
2. Update components to use new tokens
3. Test both light and dark modes
4. Test at mobile width (375px) — verify touch targets and spacing
```

---

## Version bump rules

When iterating on an existing design system:

- **Patch (1.0.x)** — small color tweaks, minor spacing adjustments
- **Minor (1.x.0)** — font change, radius philosophy change, new theme variant
- **Major (x.0.0)** — full aesthetic direction change, complete rebuild

Always add a changelog entry. Never remove previous entries.
The changelog is how the user tracks the evolution of their taste.
