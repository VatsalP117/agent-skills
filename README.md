# Design System Skill

Generate personalized design systems through an intelligent interview process. Go from "generic AI UI" to a unique visual identity you can reuse across projects.

---

## Installation

```bash
npx skills add VatsalP117/design-system-skill
```

**Important**: Use your exact repo name after you rename it. If you rename to `design-system-skill`, the command above is correct.

Once installed, tell your agent: *"I want to create a design system"* or *"Make my UI look less generic"*.

---

## What You Get

After running the skill, you will have four concrete files:

1. **TASTE.md** — Your aesthetic philosophy in plain language (the *why*)
2. **tokens.json** — Complete design tokens with light and dark themes, spacing, typography, motion (the *what*)
3. **tokens.css** — CSS custom properties ready to drop into any project (the *how*)
4. **agent-prompt.md** — A snippet to paste at the start of any AI conversation to maintain consistency

Plus a live preview in your browser showing your tokens applied to real components.

---

## How It Works

The skill runs an interview process, then generates and iterates until your design system feels right.

### Four Modes

**Quick Create (default)** — Best for starting fresh or getting results fast. Three questions:
- What are you building?
- How do you want it to feel?
- Show me 1-2 UIs you love

**Deep Create** — Best when you have strong opinions or want thorough personalization. Full interview covering color mood, typography preferences, motion style, and a deep-dive into your inspiration references.

**Extract** — Best when you already have a project with styles you like. The agent scans your existing CSS, Tailwind config, or component files and formalizes them into a proper design system.

**Iterate** — Best when you already have a design system but want to tweak it. Make targeted changes without starting over.

### The Process

1. **Interview** — Share what you are building and what you like
2. **Derive** — The agent extracts signals from your references (what you show matters more than what you say)
3. **Render** — See a live preview with light/dark toggle and real components
4. **Iterate** — Give feedback until it feels right
5. **Output** — Get your four files plus optional integration into your current project

### Key Features

- **References over words**: When you say "slightly rounded" but show Airbnb, the agent notices and pushes toward 12px radius
- **Live preview**: See your design system applied to real components before committing
- **Accessible by default**: WCAG contrast ratios checked and adjusted automatically
- **Framework support**: Auto-detects Next.js, React, Vue, Svelte, Astro, or vanilla projects
- **AI handoff**: The agent-prompt.md constrains future AI conversations to your system

---

## Example Workflows

**"I need a design system for my SaaS dashboard"**

The agent asks what you are building and how you want it to feel. You mention Linear, Vercel, and Stripe as references. The agent extracts signals (dense data tables, monospace for technical values, subtle motion, true blacks for dark mode) and generates tokens. You see a live preview with a sidebar task list, metric cards, and a data table styled like your references. After a few iterations on the accent color and card radius, you lock in the system.

**"My project looks like generic AI slop"**

The agent runs the quick interview, discovers you want something "warm and sophisticated," and generates a system with a distinctive display font, warm off-whites for the light theme, and thoughtful spacing. The live preview shows you immediately that this feels different, more considered, less template-y.

**"I love how Airbnb looks — make mine feel like that"**

The agent extracts design signals from Airbnb's style (generous spacing, rounded cards with soft shadows, warm photography-forward aesthetic) and applies them to your project type. You get the feel without copying the exact colors.

---

## File Structure

```
design-system-skill/
├── SKILL.md                  # Skill definition (agent instructions)
├── README.md                 # This file
└── references/
    ├── interview.md          # Full question bank and font pairings
    ├── renderer.md           # Component library spec
    ├── outputs.md            # File formats and templates
    └── integration.md        # Per-framework integration guides
```

---

## FAQ

**Q: Can I use this without installing anything?**
A: The skill needs to be installed into your agent's skills directory. Use the `npx skills add` command above.

**Q: Will this overwrite my existing styles?**
A: The agent always asks before overwriting. You can choose to replace completely, merge (design system takes precedence), or create a separate file for manual merging.

**Q: Can I export to Figma?**
A: Not directly. The skill generates code-ready tokens. You can manually input the color values and typography scales into Figma if needed.

**Q: What if I do not like the first result?**
A: That is expected. The skill is built for iteration. Tell the agent what feels off — "too dark," "type feels wrong," "cards look cheap" — and they will adjust and re-render.

**Q: Can I use this for client work?**
A: Yes. The output files are yours. Use them in personal projects, client work, commercial products, whatever you need.

---

## Contributing

Found an issue or have a suggestion? Open an issue or submit a PR.

---

## License

MIT
