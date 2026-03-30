# Integration Guide

How to integrate the design system into different project types.

Read this file when the user wants to apply their design system to an existing project.

---

## When to Integrate

After Step 5 (Lock and Output), ask the user:

> "Your design system is ready! Would you like me to integrate it into your current project? I can detect your project type and apply the tokens automatically."

If they say yes, detect the project type and follow the appropriate guide below.

---

## Project Type Detection

Look for these indicators:

**Next.js + Tailwind CSS v4:**
- `next.config.*` file exists
- `app/globals.css` or `styles/globals.css` with `@import "tailwindcss"`
- `tailwind.config.*` may or may not exist (v4 uses CSS config)

**Next.js + Tailwind CSS v3:**
- `next.config.*` file exists
- `tailwind.config.js` or `tailwind.config.ts` exists
- `postcss.config.js` exists

**React + Tailwind:**
- `src/index.css` or `src/App.css` with Tailwind directives
- `tailwind.config.js` exists
- No Next.js config

**Astro:**
- `astro.config.*` file exists
- `src/layouts/` directory
- May use Tailwind or vanilla CSS

**SvelteKit:**
- `svelte.config.js` exists
- `src/routes/` directory
- `src/app.css` or `src/app.postcss`

**Vue + Tailwind:**
- `vue.config.js` or `vite.config.js` with Vue plugin
- `src/assets/main.css` or similar

**Vanilla HTML/CSS:**
- `index.html` at root
- No framework config files
- Simple project structure

---

## Integration: Next.js + Tailwind CSS v4

**Files to modify:**
1. `app/globals.css` (or `styles/globals.css`)

**Steps:**

1. Add Google Fonts import at the TOP of globals.css:
```css
/* Design System Fonts */
@import url('https://fonts.googleapis.com/css2?family={FONT_URL}');

@import "tailwindcss";
/* ... rest of imports */
```

2. Add CSS variables to @theme inline block or :root:
```css
@theme inline {
  --font-sans: '{Body Font}', system-ui, sans-serif;
  --font-mono: '{Mono Font}', 'Fira Code', monospace;
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  /* ... map all design system tokens */
}
```

3. Update :root with design system colors:
```css
:root {
  /* Light theme tokens */
  --background: {light-bg};
  --foreground: {light-text};
  --card: {light-surface};
  --primary: {light-accent-1};
  --secondary: {light-accent-2};
  /* ... all tokens */
}

.dark {
  /* Dark theme tokens */
  --background: {dark-bg};
  --foreground: {dark-text};
  /* ... all tokens */
}
```

4. Add utility classes:
```css
@layer base {
  .font-display {
    font-family: '{Display Font}', system-ui, sans-serif;
  }
  
  .section-label {
    font-family: '{Mono Font}', monospace;
    font-size: 10px;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--muted-foreground);
  }
}
```

5. Add responsive spacing overrides:
```css
@media (max-width: 640px) {
  :root {
    /* Reduce spacing scale by 25% for mobile */
    --space-4: 12px;
    --space-6: 18px;
    --space-8: 24px;
    --space-10: 30px;
    --space-12: 36px;
  }
}
```

**Confirmation message:**
> "I've integrated your design system into the Next.js project. I've:
> - Added Google Fonts for {font names}
> - Updated CSS variables in globals.css
> - Set up both light and dark themes
> - Added utility classes for typography
> - Added mobile-responsive spacing overrides
>
> You can now use classes like `font-display`, `text-primary`, `bg-surface` etc."

---

## Integration: Next.js + Tailwind CSS v3

**Files to modify:**
1. `styles/globals.css` (or `app/globals.css`)
2. `tailwind.config.js`

**Steps:**

1. Add to `globals.css`:
```css
@import url('https://fonts.googleapis.com/css2?family={FONT_URL}');

@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  /* All design system CSS variables */
}

.dark {
  /* Dark mode variables */
}

@media (max-width: 640px) {
  :root {
    /* Mobile spacing overrides */
  }
}
```

2. Update `tailwind.config.js`:
```javascript
module.exports = {
  darkMode: 'class',
  theme: {
    extend: {
      fontFamily: {
        display: ['{Display Font}', 'system-ui', 'sans-serif'],
        body: ['{Body Font}', 'system-ui', 'sans-serif'],
        mono: ['{Mono Font}', 'Fira Code', 'monospace'],
      },
      colors: {
        background: 'var(--background)',
        foreground: 'var(--foreground)',
        primary: {
          DEFAULT: 'var(--primary)',
          foreground: 'var(--primary-foreground)',
        },
        /* ... all tokens mapped */
      },
    },
  },
}
```

---

## Integration: Astro

**Files to create/modify:**
1. `src/styles/design-system.css` (new)
2. `src/layouts/Layout.astro` (or base layout)

**Steps:**

1. Create `src/styles/design-system.css` with the full tokens.css content

2. Import in the base layout:
```astro
---
// src/layouts/Layout.astro
---
<html lang="en" data-theme="dark">
<head>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family={FONT_URL}" rel="stylesheet">
</head>
<body>
  <slot />
</body>
</html>

<style is:global>
  @import '../styles/design-system.css';
</style>
```

3. If using Tailwind with Astro, also update `tailwind.config.*` as in the
   Next.js v3 guide above.

4. Add theme toggle as an Astro component or inline script:
```astro
<script is:inline>
  function toggleTheme() {
    const html = document.documentElement;
    const current = html.getAttribute('data-theme');
    const next = current === 'dark' ? 'light' : 'dark';
    html.setAttribute('data-theme', next);
    localStorage.setItem('theme', next);
  }
  // Restore saved theme
  const saved = localStorage.getItem('theme');
  if (saved) document.documentElement.setAttribute('data-theme', saved);
</script>
```

---

## Integration: SvelteKit

**Files to create/modify:**
1. `src/app.css` (or `src/app.postcss`)
2. `src/app.html`
3. Optionally `tailwind.config.js` if using Tailwind

**Steps:**

1. Add Google Fonts to `src/app.html`:
```html
<head>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family={FONT_URL}" rel="stylesheet">
  %sveltekit.head%
</head>
<body data-sveltekit-preload-data="hover" data-theme="dark">
  <div style="display: contents">%sveltekit.body%</div>
</body>
```

2. Add design system tokens to `src/app.css`:
```css
/* Paste full tokens.css content here */

/* Mobile responsive overrides */
@media (max-width: 640px) {
  :root {
    /* Reduced spacing scale */
  }
}
```

3. If using Tailwind, update `tailwind.config.js` as in the Next.js v3 guide.

4. Create a theme toggle store:
```javascript
// src/lib/stores/theme.js
import { writable } from 'svelte/store';
import { browser } from '$app/environment';

const stored = browser ? localStorage.getItem('theme') ?? 'dark' : 'dark';
export const theme = writable(stored);

theme.subscribe((value) => {
  if (browser) {
    document.documentElement.setAttribute('data-theme', value);
    localStorage.setItem('theme', value);
  }
});

export function toggleTheme() {
  theme.update((t) => (t === 'dark' ? 'light' : 'dark'));
}
```

---

## Integration: Vanilla HTML/CSS

**Files to create/modify:**
1. Create `design-system.css` in project root
2. Link it in `index.html`

**Steps:**

1. Create `design-system.css` with complete tokens.css content

2. Add to `<head>` in index.html:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family={FONT_URL}" rel="stylesheet">
<link rel="stylesheet" href="design-system.css">
```

3. Add theme toggle script:
```javascript
// Save this as theme.js
function toggleTheme() {
  const html = document.documentElement;
  const current = html.getAttribute('data-theme');
  const next = current === 'dark' ? 'light' : 'dark';
  html.setAttribute('data-theme', next);
  localStorage.setItem('theme', next);
}
// Restore saved theme
const saved = localStorage.getItem('theme');
if (saved) document.documentElement.setAttribute('data-theme', saved);
```

---

## Integration: React + Tailwind

Same as Next.js + Tailwind v3, but modify:
- `src/index.css` instead of `app/globals.css`
- No Next.js-specific files

---

## Integration: Vue + Tailwind

Same as Next.js + Tailwind v3, but modify:
- `src/assets/main.css` instead of `app/globals.css`
- No Next.js-specific files
- Theme toggle uses Vue's `ref()` from Composition API

---

## Post-Integration Checklist

After integrating, verify:

- [ ] Fonts load correctly (check Network tab)
- [ ] Colors apply in both light and dark modes
- [ ] No CSS conflicts with existing styles
- [ ] Theme toggle works (if implemented)
- [ ] Theme persists across page reload (localStorage)
- [ ] No console errors
- [ ] Text passes contrast check at both themes (inspect with DevTools)
- [ ] Touch targets are ≥44px on mobile
- [ ] Spacing reduces on mobile viewport

**Common issues:**
1. **Fonts not loading** → Check if @import is at the very top, or switch to `<link>` tags
2. **Colors not applying** → Verify CSS variable names match Tailwind config
3. **Conflicts** → Check specificity, use !important sparingly
4. **FOUT (flash of unstyled text)** → Add `font-display: swap` to @font-face or use `<link rel="preload">`
5. **Dark mode not toggling** → Ensure `data-theme` attribute is on `<html>`, not `<body>`

---

## Preserving User's Existing Styles

**IMPORTANT:** Always ask before overwriting:

> "I see you have existing styles in globals.css. Should I:
> 1. Replace them completely with your design system
> 2. Merge them (design system takes precedence for conflicts)
> 3. Create a separate file and you merge manually?"

**Safe merging strategy:**
1. Keep existing custom CSS classes
2. Replace only color/font tokens
3. Comment out conflicting rules with explanation

---

## Integration Files Output

After integration, provide a summary:

```
✅ Design System Integrated!

Modified files:
- app/globals.css (or equivalent)
- tailwind.config.js (if applicable)

Your design system is now active:
- Light theme: {description}
- Dark theme: {description}
- Primary accent: {color}
- Secondary accent: {color}
- All text meets WCAG AA contrast

Next steps:
1. Run your dev server to see the changes
2. Update components to use new tokens
3. Use agent-prompt.md for future projects
```
