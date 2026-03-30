# TASTE.md - Personal Design Brief
_v1.0.0 - Updated March 30, 2026_

## Project context
Primarily building: AI SaaS dashboard + premium marketing surfaces.

## Aesthetic direction
The system is cinematic utility: editorial at the top of the page, operational in the body. Headlines should feel intentional and premium, while product surfaces stay fast, clear, and unambiguous.

Visual noise is aggressively removed. Borders carry structure, spacing carries rhythm, and color carries meaning. Accent color is used as signal, not decoration.

## Inspiration references
- **Apple product pages** - large display type, disciplined whitespace, premium confidence -> signals: oversized hero typography, calm contrast, minimal chrome.
- **Linear** - dense information that still feels clean -> signals: compact rows, precise 1px separators, low-friction interactions.
- **Stripe dashboard/docs** - trustworthy information design -> signals: clear form hierarchy, restrained semantic color, practical readability.

## Shared signals across references
- Typography-driven hierarchy with strong headline presence.
- Tight, clean border systems instead of heavy drop shadows.
- Controlled, high-contrast neutrals with selective accent usage.

## Color
- Mood: Dark-first with a warm light counterpart.
- Strategy: One dominant accent plus one supporting accent.
- Never: Purple gradients, washed-out pastels, low-contrast gray-on-gray text.

## Typography
- Display: Syne - modern geometric character with editorial punch.
- Body: DM Sans - practical, readable, neutral under load.
- Mono: JetBrains Mono - technical metadata and tabular data.
- Never: Inter/Roboto/Arial as primary identity fonts.

## Shape & form
- Border radius: 10px cards, 14px large surfaces, 4px dense utility chips.
- Borders: rgba opacity tiers as primary depth model.
- Shadows: Mixed policy; subtle ambient shadows only on hero and overlays.

## Motion
- Duration: 100ms default for UI responsiveness.
- Easing: ease-out for enter/state transitions.
- Never: Slow ornamental motion, bounce-heavy or distracting choreography.

## Density
Medium-dense. Interfaces should show enough operational context without feeling cramped. Marketing zones can breathe; product zones stay compact and legible.

## Responsive behavior
- Mobile spacing: reduce by 25% for space-4 and above.
- Mobile typography: clamp-based display scale, body drops one step.
- Touch targets: 44px minimum.

## The gap (words vs references)
The requested feel was "impressive"; references clarified that impressive means precision and restraint, not decorative complexity. This system leans premium and sharp instead of flashy.

## Anti-patterns
Things an agent must NEVER do when building with this design system:
- Add purple-to-blue hero gradients.
- Use pill-shaped controls for core dashboard UI.
- Apply large soft shadows to every card.
- Introduce random accent colors outside token set.
- Use low-contrast tertiary text for important labels.
- Over-animate page transitions above 300ms.
- Mix inconsistent border radius values.
- Default to framework color presets without token mapping.

## What makes this memorable
Cinematic headline energy on top of a brutally clear, high-trust product skeleton.
