---
name: design-system
description: >
  Build, render, and iteratively refine a personal design system with the user.
  Use this skill whenever the user wants to: create a design system, define their
  visual style or design tokens, iterate on UI aesthetics, improve the look of
  their AI-built projects, set up a tokens.json or CSS variables file, generate
  a live design renderer, discuss what makes their UI feel generic, or reference
  design inspiration like specific websites or apps they admire. Also trigger when
  the user says things like "my UI looks like AI slop", "help me nail my aesthetic",
  "create tokens for my project", "let's iterate on my design", "extract my design
  system from my project", "quick design system", or "make this look less generic".
  This skill runs a structured interview (quick or deep), produces
  tokens.json + tokens.css + TASTE.md + agent-prompt.md, renders everything live
  in the browser so the user can see and react, supports ongoing iteration,
  and can automatically integrate the design system into the user's current project
  (Next.js, React, Vue, Svelte, Astro, or vanilla HTML/CSS). It can also extract
  and formalize a design system from an existing project's styles.
---

# Design System Skill

This skill helps users go from zero (or "generic AI UI") to a personal, opinionated
design system they own and reuse across projects. The output is a set of files the
user keeps and hands to any agent at the start of a new project.

## What this skill produces

1. **TASTE.md** — plain-language aesthetic brief (the *why*)
2. **tokens.json** — structured design decisions (the *what*)
3. **tokens.css** — ready-to-paste CSS custom properties (the *how*)
4. **agent-prompt.md** — a snippet to paste at project start to inject the system
5. **A live renderer** — interactive HTML that shows all tokens applied to real components, toggleable light/dark
6. **Optional: Automatic integration** — detects your project type (Next.js, React, Vue, Svelte, Astro, vanilla) and applies the design system directly

Read `references/interview.md` for the full question bank and how to run the interview.
Read `references/renderer.md` for the live renderer spec and component library.
Read `references/outputs.md` for exact file formats and the agent prompt template.
Read `references/integration.md` for project-specific integration guides.

---

## Choose the right entry point

Before starting, determine which mode fits:

| Signal | Mode | What happens |
|--------|------|--------------|
| User wants a design system and has no existing project, OR has a blank project | **Create (Quick)** | 3-question interview → derive → render → iterate → output |
| User wants a thorough, deeply personalized system | **Create (Deep)** | Full 9-question interview + reference deep-dive → derive → render → iterate → output |
| User has an existing project with styles they want to formalize | **Extract** | Scan existing CSS/config → propose tokens → render → iterate → output |
| User already has tokens/TASTE.md and wants changes | **Iterate** | Load existing files → targeted changes → render → output |

Default to **Quick** unless the user explicitly asks for a thorough process or says
they have strong opinions. You can always upgrade from Quick to Deep mid-flow
if the user wants to go deeper.

---

## Step 0 — Extract (only if user has an existing project)

Use this when the user says things like "extract my design system", "formalize my
styles", or "I have a project — systematize it."

1. **Scan the project** for style files:
   - CSS files (`*.css`, `globals.css`, `index.css`)
   - Tailwind config (`tailwind.config.*`)
   - Theme files, CSS-in-JS theme objects
   - Component files with inline styles

2. **Extract patterns** from what you find:
   - Color values (hex, rgb, hsl) → group by role (background, text, accent, semantic)
   - Font families → categorize as display/body/mono
   - Spacing values → map to a consistent scale
   - Border radius values → identify the dominant philosophy
   - Transition/animation durations
   - Shadow patterns

3. **Present findings** to the user:
   > "I found these patterns in your project:
   > - Colors: 4 background shades, 2 accent colors, 3 semantic colors
   > - Typography: Inter for body, no display font set
   > - Radius: mostly 8px, some 4px on inputs
   > - No consistent spacing scale
   >
   > I suggest formalizing these into tokens. Want me to keep your current values
   > and fill in the gaps, or use this as a starting point for refinement?"

4. Proceed to **Step 2 (Derive)** using the extracted values as the baseline.
   Run a shortened interview (Quick Mode questions) to fill in gaps — e.g., if
   there's no display font, ask about typography feel.

---

## Step 1 — Interview

### Quick Mode (default — 3 turns)

Ask these three questions in a single message — let the user answer naturally:

1. **What are you building?** (dashboard, SaaS, landing page, dev tool, etc.)
2. **Pick the words that describe how you want it to feel** (offer: precise, warm,
   serious, playful, dense, airy, fast, calm, sophisticated, raw, friendly, focused)
   — pick 3-5
3. **Share 1-2 UIs you love the look of** — what specifically draws you to them?

From these three answers, you have enough to derive a complete token set. Extract
signals from the reference(s) following the guide in `references/interview.md`.

### Deep Mode (opt-in — 7-10 turns)

Run the full two-pass interview. See `references/interview.md` for all questions.

**Pass 1 — Core questions (always ask these):**
- Project types (dashboards, landing pages, SaaS, dev tools, etc.)
- Color mood (dark/moody, light/airy, high contrast, varies)
- Aesthetic direction (minimal/refined, editorial/expressive, technical/utilitarian, bold/loud)
- Things they NEVER want to see (ask as multi-select + open text)
- Typography feel preference
- Words that describe the desired feeling (pick 3-5)
- Color strategy (one accent, two accents, monochrome)
- Motion style (snappy 100ms, subtle 200ms, deliberate 300ms, minimal)
- Border radius philosophy (sharp 0-2px, slight 4px, rounded 8px+)

**Pass 2 — Inspiration deep-dive (always ask this):**
Ask the user for 3-5 UIs, websites, or apps they genuinely love the look of.
For each one they provide, ask: *what specifically draws you to it?*

Then, for each reference, extract concrete design signals:
- Typography choices (weight, size, tracking, font families if identifiable)
- Color logic (how many colors, what role they play)
- Spacing density (generous / neutral / tight)
- Component style (border radius, shadow use, border weight)
- Motion feel
- What makes it feel non-generic

Synthesize across references: identify the 2-3 things *all* references share.
These shared signals are the core of the user's actual taste — not what they said
in Pass 1, but what they're consistently drawn to visually.

See `references/interview.md` for the full question bank, extraction guide, and
font pairing reference.

---

## Step 2 — Derive tokens

Translate interview results into concrete token values. Use `references/outputs.md`
for the exact token schema.

Key derivation rules:
- Start from the shared signals extracted from inspiration references — these override
  what the user said in words if there's a conflict
- Dark theme: true blacks (#000-#0a0a0a) for premium feel, not charcoal
- Light theme: warm off-whites (#faf9f7-#f5f4f0), never pure #ffffff as page base
- Borders: rgba-based opacity (rgba(0,0,0,0.08) light / rgba(255,255,255,0.08) dark)
  rather than flat hex — they adapt better across surface layers
- Accents in dark mode need to be ~15% brighter than light mode equivalents for contrast
- Radius: if references include Airbnb/Apple-style cards, push to 10-14px even if user
  said "slightly rounded" — their references reveal truer preference than their words
- Motion: default to 100ms ease-out unless references suggest otherwise
- Font families: never Inter, Roboto, Arial, or system-ui as the primary display font.
  Pick something with character. See `references/interview.md` for font pairing guide.

### Accessibility check (mandatory)

After deriving colors, verify WCAG contrast ratios:
- **Text on backgrounds**: minimum 4.5:1 for body text, 3:1 for large text (≥18px bold or ≥24px)
- **Interactive elements**: minimum 3:1 against adjacent colors
- **Test these pairs**: text-primary on bg-base, text-secondary on bg-base,
  text-primary on surface, accent on bg-base, inverse text on accent

Use this formula to approximate contrast ratio:
- Relative luminance L = 0.2126×R + 0.7152×G + 0.0722×B (where R/G/B are linearized 0-1)
- Contrast ratio = (L1 + 0.05) / (L2 + 0.05) where L1 is the lighter color

If any pair fails, adjust the failing color:
- Lighten text on dark backgrounds, darken text on light backgrounds
- For accents, try shifting lightness before changing hue
- Note any adjustments made: "Bumped text-secondary from #666 to #595959 for 4.5:1 contrast"

Always produce both light and dark themes. Shared tokens (spacing, typography,
radius, motion) live outside the theme blocks.

### Responsive considerations

When deriving tokens, include responsive modifiers:
- Spacing scale reduces by ~25% on mobile (below `sm` breakpoint)
- Display type should use `clamp()` for fluid sizing
- Minimum touch target: 44px for interactive elements on mobile
- Consider whether the design needs tighter density on mobile or just smaller type

---

## Step 3 — Render live

Build an interactive HTML file and save it to the user's project or a temp location.
See `references/renderer.md` for the full component spec.

### Rendering approach (in priority order)

1. **Write an HTML file** to the user's project directory (e.g., `design-system-preview.html`)
   and open it in the browser. This is the most reliable cross-agent approach.
2. If a Visualizer/widget tool is available in your environment, you may use it instead.

The renderer must include:
- Light/dark toggle (instant switch, no page reload)
- Color swatches for all background layers + accents + semantic colors,
  **with WCAG contrast ratio displayed on each swatch** (e.g., "4.7:1 ✓" or "2.8:1 ✗")
- Full typography scale with actual font families loaded from Google Fonts
- At minimum these component previews: navigation bar, metric cards, listing/content
  cards, data table, buttons (primary/default/ghost/destructive), badges/tags,
  text inputs, toast/notification, modal dialog
- A hero/editorial section that shows the display type at large size
- Motion demo (hover states that demonstrate the timing)
- A mobile-width preview section (max-width: 375px container) showing how cards
  and typography adapt

Model the component previews after the user's inspiration references:
- If they cited Airbnb → include a listing card grid with image placeholder + metadata
- If they cited Vercel → include a deployment/data table with monospace values
- If they cited Apple product pages → include a full-bleed hero with large display type
- If they cited Linear → include a dense sidebar-style task list
- If they cited Stripe → include a form with clean inputs and a summary panel

The renderer is the primary feedback mechanism. Show it before asking for feedback.

---

## Step 4 — Iterate

After showing the renderer, ask:
> "How does this feel? Tell me anything — a color that's off, the type feeling
> wrong, cards too tight or too airy, anything."

Take each piece of feedback and:
1. Identify which token(s) it affects
2. State what you're changing and why
3. Re-render with the change applied
4. Show a brief diff of what changed (e.g., "border-radius: 4px → 12px on cards")

Keep iterating until the user says they're happy or ready to lock it.

Common iteration patterns:
- "Feels cold" → warm up background base by 5-10% toward yellow/red, loosen spacing
- "Too dark / oppressive" → raise surface from #0a0a0a to #111, add more layer separation
- "Feels generic still" → push typography harder (bigger display, tighter tracking),
  make accent color more distinctive
- "Cards feel cheap" → increase padding, add subtle border, bump radius
- "Too much going on" → reduce to one accent, mute secondary text further
- "Type feels wrong" → swap font family, adjust weight, change tracking
- "Can't read the text" → check contrast ratios, adjust text/bg lightness

---

## Step 5 — Lock and output

When the user is satisfied, produce all output files. See `references/outputs.md`
for exact formats.

Files to produce:
1. `TASTE.md` — the aesthetic brief with references, anti-patterns, and philosophy
2. `tokens.json` — full token set with version, changelog, both themes, and contrast metadata
3. `tokens.css` — CSS custom properties, ready to paste into any project
4. `agent-prompt.md` — the project-start injection snippet with anti-slop guardrails

Present all four files. Then say:

> "To use this in a new project, paste the contents of agent-prompt.md at the
> start of your conversation with the agent. It gives the agent your full design
> system as a constraint — they implement, they don't design."

---

## Step 5b — Integrate into current project (Optional)

**ONLY if the user is in an active project context and wants to apply the design system immediately.**

Read `references/integration.md` for project-specific integration guides.

Ask the user:
> "Would you like me to integrate this design system into your current project? I can detect the project type and apply the tokens automatically."

**If YES:**

1. **Detect project type** by looking for config files:
   - Next.js: `next.config.*` exists
   - Tailwind v4: `@import "tailwindcss"` in CSS
   - Tailwind v3: `tailwind.config.js` exists
   - React: `src/` folder, no Next.js config
   - Vue/Svelte: framework-specific configs
   - Astro: `astro.config.*` exists
   - Vanilla: `index.html` at root

2. **Check for existing styles** before overwriting:
   > "I see you have existing styles in {file}. Should I:
   > - Replace them completely
   > - Merge them (design system takes precedence)
   > - Create a separate file for manual merging?"

3. **Apply the integration** following the appropriate guide from `references/integration.md`:
   - Add Google Fonts import
   - Insert CSS variables
   - Update Tailwind config (if applicable)
   - Add utility classes
   - Preserve existing custom styles when possible

4. **Clean up**: Remove the `design-system-preview.html` file if it was created
   during the render step.

5. **Provide confirmation summary:**
   > "✅ Design system integrated! I've:
   > - Added Google Fonts: {font names}
   > - Updated CSS variables in {file}
   > - Set up light/dark themes
   > - Added utility classes (font-display, section-label, etc.)
   >
   > Run your dev server to see the changes!"

**If NO or not in a project context:**
Skip to Step 6. The files are ready for manual use in future projects.

---

## Step 6 — Future iteration

The user can return at any time and say things like:
- "I want to tweak my design system"
- "Update my tokens — I want to try a warmer light theme"
- "I found a new reference I love, help me incorporate it"
- "My dark theme feels off, let's fix it"

When this happens:
1. Load their existing tokens.json if they share it, or re-run a short interview
2. Make targeted changes rather than rebuilding from scratch
3. Show a before/after diff of changed tokens
4. Re-render to confirm
5. Output updated files with bumped version number and changelog entry

Never throw away previous decisions unless explicitly asked to.
