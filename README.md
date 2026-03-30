# Agent Skills Collection

A curated set of skills for AI coding agents. Each skill provides reusable instructions and workflows to help agents deliver more consistent, high-quality results for specific tasks.

Currently includes: **Design System Skill** — generate personalized design systems with live preview.

---

## Quick Start

Install the design system skill into your AI coding agent:

```bash
npx skills add VatsalP117/agent-skills
```

Once installed, tell your agent: *"I want to create a design system"* or *"Make my UI look less generic"*.

---

## What's Included

### Design System Skill

Transforms "generic AI UI" into a personal, opinionated design system you own and reuse across projects. This skill guides you through a structured interview process, generates design tokens, and produces production-ready files.

#### What You Get

1. **TASTE.md** — Your aesthetic philosophy in plain language
2. **tokens.json** — Structured design decisions with both light and dark themes
3. **tokens.css** — CSS custom properties ready to drop into any project
4. **agent-prompt.md** — A snippet to paste at the start of any project to maintain consistency
5. **Live Preview** — Interactive HTML showing your design tokens applied to real components
6. **Auto-Integration** — Optionally apply the system directly to your current project

#### How It Works

The skill offers four modes depending on your situation:

**Quick Create (default)**
Perfect when you're starting fresh or want results fast. Three questions:
- What are you building?
- How do you want it to feel? (pick from: precise, warm, serious, playful, dense, airy, sophisticated, raw, focused...)
- Show me 1-2 UIs you love

From your answers, the agent derives a complete token set, renders a live preview, and iterates with you until it feels right.

**Deep Create**
For when you have strong opinions or want a thoroughly personalized system. Includes a full interview covering color mood, typography preferences, motion style, border radius philosophy, and a deep-dive into your inspiration references. The agent extracts concrete design signals from each reference and synthesizes what makes your taste unique.

**Extract**
Already have a project with styles you like? The agent scans your existing CSS, Tailwind config, or component files, identifies the patterns you've been using, and formalizes them into a proper design system. Perfect for "I've been winging it, now I want to do this right."

**Iterate**
Already have a design system but want to tweak it? The agent loads your existing tokens and lets you make targeted changes without starting over. Adjust the color palette, try a warmer light theme, incorporate a new reference you discovered — whatever you need.

#### Example Workflows

**"I need a design system for my SaaS dashboard"**

The agent asks what you're building and how you want it to feel. You mention Linear, Vercel, and Stripe as references. The agent extracts signals (dense data tables, monospace for technical values, subtle motion, true blacks for dark mode) and generates tokens. You see a live preview with a sidebar task list, metric cards, and a data table styled like your references. After a few iterations on the accent color and card radius, you lock in the system.

**"My project looks like generic AI slop"**

The agent runs the quick interview, discovers you want something "warm and sophisticated," and generates a system with a distinctive display font, warm off-whites for the light theme, and thoughtful spacing. The live preview shows you immediately that this feels different — more considered, less template-y.

**"I love how Airbnb looks — make mine feel like that"**

The agent extracts design signals from Airbnb's style (generous spacing, rounded cards with soft shadows, warm photography-forward aesthetic) and applies them to your project type. You get the feel without copying the exact colors.

---

## Installation

Install globally to use across all projects:

```bash
npx skills add VatsalP117/agent-skills -g
```

Or install to a specific agent or project:

```bash
npx skills add VatsalP117/agent-skills
```

The skill will be available to agents that support the skills protocol (OpenCode, Claude Code, Cursor, and others).

---

## Framework Support

The design system skill detects your project type and handles integration automatically:

- **Next.js** — Updates globals.css, configures Tailwind v3/v4
- **React** — Injects CSS variables into your style entry point
- **Vue / Svelte** — Applies to framework-specific CSS
- **Astro** — Updates global styles
- **Vanilla HTML/CSS** — Creates a clean CSS file with your tokens

You can also use the tokens manually in any project by copying the generated files.

---

## What Makes This Different

Most design system generators give you tokens and call it done. This skill focuses on **iteration and taste discovery**:

1. **Your references matter more than your words** — When you say "slightly rounded" but show Airbnb references, the agent notices and pushes toward 12px radius. Your inspiration reveals truer preferences than your descriptions.

2. **Live preview is the primary feedback loop** — You don't review JSON. You see your design system applied to real components in a browser, toggle light/dark instantly, and spot issues immediately.

3. **Designed for AI handoff** — The `agent-prompt.md` file is specifically crafted to paste at the start of any project conversation. It constrains the agent to your system so they implement, not redesign.

4. **Accessible by default** — Every color combination is checked against WCAG contrast ratios. The agent adjusts values that don't meet standards and tells you what changed.

---

## Project Structure

```
skills/
└── design-system/
    ├── SKILL.md                  # Main skill definition
    └── references/
        ├── interview.md          # Full question bank and font pairings
        ├── renderer.md           # Component library spec
        ├── outputs.md            # File formats and templates
        └── integration.md        # Per-framework integration guides
```

---

## Contributing

Found an issue or have a suggestion? Open an issue or submit a PR. Skills are meant to evolve based on real usage patterns.

---

## License

MIT

---

## Questions?

**Q: Can I use this without installing anything?**
A: The skill needs to be installed into your agent's skills directory. Use the `npx skills add` command above.

**Q: Will this overwrite my existing styles?**
A: The agent always asks before overwriting. You can choose to replace completely, merge (design system takes precedence), or create a separate file for manual merging.

**Q: Can I export to Figma?**
A: Not directly. The skill generates code-ready tokens. You can manually input the color values and typography scales into Figma if needed.

**Q: What if I don't like the first result?**
A: That's expected. The skill is built for iteration. Tell the agent what feels off — "too dark," "type feels wrong," "cards look cheap" — and they'll adjust and re-render.

**Q: Can I use this for client work?**
A: Yes. The output files are yours. Use them in personal projects, client work, commercial products — whatever you need.
