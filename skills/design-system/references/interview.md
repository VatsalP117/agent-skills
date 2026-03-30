# Interview Reference

Full question bank and guidance for conducting the design system interview.

---

## Quick Mode (3 turns — use by default)

Quick Mode captures 80% of the signal in 20% of the time. Ask all three
questions in a single message:

```
I need three things to build your design system:

1. **What are you building?**
   Dashboard, SaaS app, landing page, dev tool, mobile app, e-commerce,
   docs site — or something else?

2. **Pick 3-5 words that describe how you want it to feel:**
   Precise · Warm · Serious · Playful · Dense · Airy · Fast · Calm ·
   Sophisticated · Raw · Friendly · Clinical · Human · Focused · Trustworthy

3. **Share 1-2 UIs you love the look of** (URLs, app names, or Dribbble shots).
   For each: what specifically draws you to it?
```

From these three answers:
- Project type → informs component choice and density defaults
- Feeling words → map to aesthetic direction (see mapping below)
- References → extract signals using the extraction guide

### Feeling-word-to-aesthetic mapping

| Dominant words | Map to |
|---|---|
| Precise, serious, dense, focused, clinical | Technical / utilitarian |
| Warm, friendly, human, calm | Minimal / refined (warm variant) |
| Sophisticated, calm, airy, trustworthy | Minimal / refined |
| Playful, raw, fast | Bold / loud |
| Sophisticated + dense | Editorial / expressive |

Use this mapping to auto-fill the aesthetic direction that would normally
come from a Deep Mode question. If the mapping is ambiguous, pick the
direction that best matches the inspiration references.

### Auto-fill from Quick Mode

Fill in the Deep Mode answers the user didn't explicitly give:

| Deep Mode question | How to auto-fill |
|---|---|
| Color mood | Infer from references (mostly dark → dark, mostly light → light) |
| Aesthetic direction | Use feeling-word mapping above |
| Things to never see | Derive from aesthetic direction (see anti-pattern derivation below) |
| Color strategy | Count accent colors in references; default to one accent |
| Motion style | Default to 100ms snappy unless references show deliberate animation |
| Border radius | Measure from references; default to 8px if unclear |
| Typography feel | Identify from references; use font pairing guide below |

If you can't confidently auto-fill something critical, ask ONE follow-up
question — don't expand into the full Deep Mode interview.

---

## Deep Mode (7-10 turns — opt-in)

Use Deep Mode when the user explicitly asks for a thorough process, or says
they have strong opinions they want to capture.

### Pass 1 — Core questions

Present these as interactive choices where possible (multi-select, single-select).
Use a conversational tone — this is a discovery session, not a form.

#### Project types (multi-select)
- Dashboards / data tools
- Landing pages / marketing
- SaaS / web apps
- Dev tools / CLIs
- Mobile apps
- E-commerce
- Documentation / content sites

#### Color mood (single-select)
- Dark / moody
- Light / airy
- High contrast / stark
- I vary per project

#### Aesthetic direction (single-select)
- Minimal / refined — less is more, whitespace as a tool
- Editorial / expressive — typography-forward, magazine-like
- Technical / utilitarian — functional, information-dense
- Bold / loud — strong color, high energy, opinionated

#### Things to never see (multi-select + open text)
Pre-set options:
- Purple/blue gradients
- Excessive border radius (pill buttons, bubbly cards)
- Drop shadows everywhere
- Pastel / muted color schemes
- Skeuomorphic effects (fake textures, 3D buttons)
- Neon / glow effects
- Comic sans or novelty fonts
- Animation-heavy / distracting motion

Always follow up with: "Anything else that immediately makes you think 'no'?"

#### Feeling words (multi-select, pick 3-5)
- Precise
- Warm
- Serious
- Playful
- Dense
- Airy
- Fast
- Calm
- Trustworthy
- Sophisticated
- Raw
- Friendly
- Clinical
- Human
- Focused

#### Color strategy (single-select)
- One strong accent (everything else neutral)
- Two complementary accents
- Monochrome only
- Brand colors I'll specify

#### Motion style (single-select)
- Instant / snappy (75-100ms) — UI responds, doesn't perform
- Subtle / quick (150-200ms) — gentle but present
- Deliberate / smooth (300-400ms) — considered, intentional
- Minimal — almost no animation

#### Border radius (single-select)
- Sharp / 0px — brutalist, raw
- Almost sharp / 2px — minimal softening
- Slightly rounded / 4px — structured, professional
- Rounded / 8-10px — approachable, modern
- Very rounded / 12-16px — friendly, Airbnb-style
- Full pill — bubbly (note: often contradicts professional aesthetics)

#### Typography feel (single-select)
- Monospace / terminal — code-like, technical
- Geometric sans — clean, precise (Futura, DM Sans)
- Humanist sans — warm, readable (Nunito, Source Sans)
- Transitional serif — editorial, authoritative
- Display / expressive — high personality
- No strong preference

---

### Pass 2 — Inspiration deep-dive (always ask this)

Say to the user:
> "Now the most important question: share 3-5 UIs, websites, or apps you genuinely
> love the look of. Can be anything — Dribbble shots, products you use, company
> sites. For each one, tell me *what specifically* draws you to it."

For each reference provided, extract signals using the guide below.

---

## Signal extraction guide (used in both Quick and Deep mode)

For every inspiration reference the user provides, extract:

### Typography signals
- Is the display type large and dramatic, or restrained?
- Is body text light weight (300) or regular (400)?
- Are there condensed/tight tracked headlines?
- Is monospace used for data / metadata?
- What's the approximate font family category?

### Color signals
- How many distinct colors are in use?
- Is the accent color used sparingly or liberally?
- Are backgrounds warm-tinted or cool/neutral?
- Does color encode meaning or is it decorative?

### Density signals
- Is whitespace generous (Apple) or tight (Bloomberg)?
- Are elements packed close or given room to breathe?
- How much content is visible without scrolling?

### Component signals
- What's the approximate border radius on cards?
- Are shadows present, and if so, how heavy?
- Are borders used, and at what weight?
- Do interactive elements feel snappy or smooth?

### What makes it non-generic
- What's the one thing you'd remember about this UI?
- What would you immediately copy if starting a new project?

### Synthesis

After extracting signals from all references, identify:
1. **Shared signals** — things that appear in 2+ references. These are the user's core taste.
2. **Contradictions** — if references conflict (one is airy, one is dense), ask the user to pick.
3. **The gap** — compare what the user *said* in Pass 1 (or Quick Mode) vs what their
   references *show*. If there's a gap, go with the references. Words are often
   inaccurate about taste.

Example gaps:
- User says "minimal" but references are actually editorial and expressive → go editorial
- User says "4px radius" but all references have rounded Airbnb-style cards → go 12px
- User says "dark" but shows mostly light references → ask which they actually want

---

## Extract Mode interview (for existing projects)

When the user has an existing project, the interview is shorter because the
code provides most of the signal. After scanning the project (Step 0 in SKILL.md),
ask only what you can't determine from the code:

1. **Are you happy with your current colors, or do you want to change direction?**
2. **What about typography — keep the current fonts or pick something with more character?**
3. **Share 1 UI you wish your project looked more like** (optional)

Use the extracted values as defaults. Only change what the user explicitly
asks to change.

---

## Font pairing guide

Match font pairs to aesthetic direction. Never use Inter as a display font.

### Technical / utilitarian
- Display: Geist, IBM Plex Sans, Syne, Space Grotesk
- Body: DM Sans, IBM Plex Sans, Outfit, Geist
- Mono: JetBrains Mono, IBM Plex Mono, Geist Mono, Fira Code

### Editorial / expressive
- Display: Fraunces, Playfair Display, Cormorant, Syne, Instrument Serif
- Body: DM Sans, Libre Franklin, Source Sans 3, Newsreader
- Mono: JetBrains Mono (for data only)

### Minimal / refined
- Display: Syne, Plus Jakarta Sans, Figtree, Satoshi (via Fontshare)
- Body: DM Sans, Nunito Sans, Inter (body only, not display), Outfit
- Mono: JetBrains Mono, Fira Code

### Bold / loud
- Display: Bebas Neue, Space Grotesk, Anton, Bricolage Grotesque
- Body: DM Sans, Barlow, Outfit
- Mono: JetBrains Mono

### Apple-inspired
- Display: Syne or Plus Jakarta Sans at heavy weight, tight tracking
- Body: Inter at 300-400 weight, generous leading
- Note: Apple uses SF Pro which isn't on Google Fonts — Syne is the closest available match

### Airbnb-inspired
- Display: Syne or Plus Jakarta Sans
- Body: DM Sans or Nunito Sans (warm, slightly rounded feel)
- Note: Airbnb uses Cereal which isn't on Google Fonts

### Vercel-inspired
- Display: Geist or Syne
- Body: Geist or DM Sans
- Mono: Geist Mono or JetBrains Mono (used heavily for data)

### Variable font recommendations
When performance matters (large apps, mobile-first), prefer variable fonts
that reduce HTTP requests:
- **Inter** (body) — one file, full weight range
- **DM Sans** (body) — variable available
- **Plus Jakarta Sans** (display/body) — variable available
- **Space Grotesk** (display) — variable available
- **Outfit** (body) — variable, very light file weight

Note font file sizes when recommending — a 300KB display font on a dashboard
that loads 50 times a day is fine; on a landing page competing for Core Web
Vitals, it matters. Suggest `font-display: swap` in all cases.

---

## Anti-pattern derivation

After the interview, always derive an explicit anti-pattern list for TASTE.md.
These are things the agent must never do in this user's projects.

Base anti-patterns (always include):
- Never use Inter, Roboto, Arial, or system-ui as the display/headline font
- Never use purple-to-blue gradients as a background or hero treatment
- Never use drop shadows as a primary depth mechanism — use borders instead
- Never hardcode color values — always use CSS custom properties / tokens

Derive from aesthetic direction:
- Minimal/refined → no decorative illustrations, no background patterns, no excessive color
- Editorial → no symmetrical layouts, no cookie-cutter card grids
- Technical → no rounded pill buttons, no pastel color schemes, no playful illustrations
- Bold → no timid neutral palettes, no thin/light typography

Derive from feeling words:
- Serious + precise → no bounce animations, no playful microcopy, no emoji in UI
- Warm + human → no cold blues as primary, no clinical white backgrounds
- Dense + focused → no excessive whitespace, no single-column sparse layouts

Derive from references:
- If Apple referenced → no heavy drop shadows, no busy backgrounds
- If Vercel referenced → no colorful gradients, no decorative elements
- If Airbnb referenced → no sharp 0px radius, no clinical spacing
- If Linear referenced → no airy generous spacing in data areas

Always ask: "Anything else that would immediately make you think 'wrong direction'?"
