# Design

## Name

Cast Bronze

## Summary

A boutique training studio at dusk, not a SaaS dashboard: warm dark ground, one cast-bronze accent lifted
straight from the client's badge logo, and a light "paper" surface used only where something needs to read
as a tactile, framed object (the assessment card, the credential grid, result cards) — everywhere else stays
dark so the badge and the paper cards are the things that visually lift off the page, not everything at once.

Supersedes the site's original "Counted Weight" system (flat, zero-radius, red accent, no shadows), which
was built around a different, abandoned logo direction. See `PRODUCT.md` → Anti-references.

## Color

Strategy: **Committed** — one saturated brand color (bronze) carries real surface weight via buttons, marks,
and the badge itself; the dark ground is a true near-black warm neutral, not a tinted-cream default.

| Token | Value | Use |
| --- | --- | --- |
| `--color-bg` | `#17130f` | Page ground (default surface) |
| `--color-bg-raised` | `#221b14` | Cards/panels sitting on the dark ground (dark band, coach section) |
| `--color-paper` | `#efe6d8` | Deliberate light surface — assessment card, credential grid, result/testimonial cards only |
| `--color-paper-muted` | `#e2d5bf` | Hover/pressed fill on paper |
| `--color-ink` | `#1c150e` | Text on paper |
| `--color-cream` | `#efe6d8` | Text on dark ground |
| `--color-cream-muted` | `#b8a98e` | Secondary text on dark ground |
| `--color-muted` | `#6b5c46` | Secondary text on paper |
| `--color-brass` | `#b6893f` | Icons, dividers, large numerals (≥28px), button fills — not body text on paper |
| `--color-brass-bright` | `#d9ac66` | Hover/focus state |
| `--color-brass-deep` | `#7c5a24` | Accent-colored body text **on paper** (5.1:1) |
| `--color-brass-deep-ondark` | `#e7c483` | Accent-colored body text **on dark ground** (11.1:1) |

Contrast verified: cream/bg 14.9:1 · ink/paper 14.6:1 · brass-deep/paper 5.1:1 · brass-deep-ondark/bg 11.1:1 ·
ink/brass (button label) 5.7:1. Plain `--color-brass` fails body-text contrast on paper (2.6:1) — reserved
for large/graphical use.

## Typography

Contrast-axis pairing (serif display + humanist sans body — deliberately not two geometric sans):

- **Display / headings:** Fraunces, weight 600, `letter-spacing: -0.01em`, sentence case (not forced
  uppercase — the previous system's all-caps-everywhere reads as shouting; this brand is "confident and
  calm," per PRODUCT.md).
- **Body:** Inter, weight 400/500.
- **Eyebrows/labels only** (used on a handful of sections, never every section): 12px Inter, uppercase,
  `0.1em` tracking.

Hero H1 ceiling: `clamp(2.5rem, 5vw, 4.5rem)` — stays under the 6rem/-0.04em bans.

## Layout & Components

- Radius: `--radius-sm 8px / --radius-md 14px / --radius-lg 24px / --radius-full 999px` — the badge is
  dimensional, the interface around it is allowed to be too (in contrast to the old zero-radius rule).
- Shadow: warm-tinted (`color-mix` off near-black, not pure black), `--shadow-sm/md/lg` plus `--shadow-brass`
  for the primary CTA's focused/hover state — a small nod to the badge's metal glint, used only on the one
  button that matters most.
- Dividers are 1px (down from the old system's structural 2px rules) and low-opacity — texture, not armor.
- `.mark` is a small filled brass dot (was a hard-edged square); `.mark-hollow` a ringed circle that fills
  brass when a step/pillar is complete — softer geometry to match the badge's circular form instead of the
  old system's squares.

## Motion

Ease-out-quart/expo, no bounce. One deliberate signature move: a slow bronze sheen sweep (`.badge-sheen`,
7s loop) on the hero badge only — "the badge earns its keep once," not on every metallic-adjacent element.
Section reveals are staggered per-item, not a uniform fade applied everywhere. All motion has a
`prefers-reduced-motion` fallback (instant/no animation).

## Imagery

Grayscale photography treatment is replaced with a lighter desaturation (`saturate(0.82) contrast(1.05)`) —
full grayscale belonged to the old flat system; a boutique-warm brand keeps a little color in its
photography. Coach/session photography should read as candid and current, not stock-gym-poster.
