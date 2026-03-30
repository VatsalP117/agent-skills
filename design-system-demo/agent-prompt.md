# Design System

Before building anything, read and apply this design system completely.
Make NO design decisions outside of these tokens. You implement; you do not improvise visual language.

## Critical guardrails
Before outputting any color, font-family, border-radius, spacing, or motion value,
verify it comes from the tokens below. If a token does not exist, ask first.

NEVER:
- Use colors outside this palette.
- Use Inter, Roboto, Arial, or system-ui as the primary display/body identity.
- Use framework default color classes without mapping to tokens.
- Use radius values outside the scale.
- Use random spacing values outside the scale.
- Overuse drop shadows.
- Use purple-to-blue gradients.

## Aesthetic brief
Cinematic utility: premium editorial hierarchy in hero zones, high-trust operational clarity in product zones. Borders and typography do the heavy lifting; accents are sparse and intentional.

## Anti-patterns
- Purple/blue gradient hero backgrounds.
- Pill-heavy dashboard controls.
- Thick shadows on every surface.
- Decorative motion over usability.
- Low-contrast tertiary text for key information.
- Random accent colors not in token set.
- Inconsistent border radius between components.
- Tailwind default blues/grays without token mapping.

## Tokens

### Typography
- Display font: Syne
- Body font: DM Sans
- Mono font: JetBrains Mono
- Google Fonts: `https://fonts.googleapis.com/css2?family=Syne:wght@600;700;800&family=DM+Sans:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap`

### Colors - Dark theme
- Page background: `#07090d`
- Card/surface: `#0f131a`
- Elevated surface: `#171d27`
- Text primary: `#f4f7fb` (18.5:1 on base)
- Text secondary: `#b7c3d4` (11.2:1 on base)
- Text muted: `#7f8a99`
- Border subtle: `rgba(255,255,255,0.06)`
- Border default: `rgba(255,255,255,0.12)`
- Accent 1: `#28c4ff`
- Accent 2: `#ff6a3d`
- Success/Warning/Danger: `#32d296` / `#f3b54a` / `#ff5d6c`

### Colors - Light theme
- Page background: `#f6f2ea`
- Card/surface: `#ffffff`
- Elevated surface: `#efe8dc`
- Text primary: `#151a22` (15.6:1 on base)
- Text secondary: `#394555` (8.7:1 on base)
- Text muted: `#667487`
- Border subtle: `rgba(0,0,0,0.06)`
- Border default: `rgba(0,0,0,0.12)`
- Accent 1: `#006e9a`
- Accent 2: `#b6421f`
- Success/Warning/Danger: `#0f8a5f` / `#a76700` / `#b52235`

### Shape & motion
- Card radius: `10px`
- Large panel radius: `14px`
- Dense chip radius: `4px`
- Default transition: `all 100ms ease-out`
- Shadow policy: mixed, borders first

### Spacing scale
`4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96 px`

### Responsive rules
- On mobile (<640px), reduce spacing by ~25% for `space-4` and above.
- Minimum touch target: `44px`.
- Hero display uses clamp and remains fluid.
- Cards become single-column below `md`.

### Implementation rules
1. Theme toggle via `data-theme` on `<html>` or root container.
2. Use CSS custom properties; no hardcoded visual constants in components.
3. Cards default to `1px` subtle border and elevate on hover with border shift.
4. Focus states use accent + 3px subtle accent ring.
5. Keep motion under 150ms for standard interactions.
