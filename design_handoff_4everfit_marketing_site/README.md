# Handoff: 4EverFit Lifestyle — marketing site (desktop + mobile)

## Overview

4EverFit Lifestyle is a one-on-one **video** personal-training business. Every plan is written across a
four-pillar system — **Nutrition, Strength training, Cardio, Supplementation** — and the site's job is to
make that system legible and drive one action: **take the 4-question pillar assessment** (email capture).

There is no pricing on the page and no booking calendar. The assessment is the only conversion point;
a coach reads each submission and emails a starting plan.

Two designs are included:

| File | Design | Notes |
| --- | --- | --- |
| `4EverFit Landing.dc.html` | Desktop marketing page | Responsive: collapses to 2-up then 1-up at 1040px / 900px / 560px |
| `4EverFit Mobile.dc.html` | Dedicated mobile design | Authored at **402 × 874** (iPhone 16 Pro logical size), shown inside a device frame |

The mobile file is a *separate design*, not the desktop page at a small width. It has its own navigation
(drawer), its own pillar treatment (accordion instead of columns), horizontal carousels, and a sticky
bottom CTA bar. Implement it as the small-breakpoint experience of one responsive site — do not ship two
codebases.

## About the design files

The files in this bundle are **design references created in HTML** — prototypes that show intended look and
behavior. They are **not production code to copy**. They rely on a custom in-house component runtime
(`support.js`, `<sc-for>`, `<sc-if>`, `{{ }}` template holes, `<x-import>`) that will not exist in your codebase.

Your task is to **recreate these designs in the target codebase's own environment** using its established
patterns — React/Next, Vue, Astro, plain HTML+CSS, whatever the project uses. If no codebase exists yet,
pick the framework that fits the project (for a marketing site of this shape, **Astro or Next.js with
Tailwind** is a sensible default) and build the designs there.

Two things you *can* reuse directly:
- `styles.css` — the Modernist design-system stylesheet. It is the source of truth for every color, font,
  and spacing value. Port its `:root` custom properties into your token layer verbatim.
- `image-slot.js` — only a prototyping affordance (drag-and-drop image placeholder). **Do not ship it.**
  Replace every `<image-slot>` with a real `<img>` / `<picture>` / framework image component.

## Fidelity

**High fidelity.** Colors, typography, spacing, rules, and interaction states are final and come from a
bound design system (Modernist). Recreate the UI faithfully — the strong 2px rules, zero corner radius,
flush-left alignment, and grayscale imagery are the identity, not defaults to be softened.

Two things are explicitly *not* final:
- **All photography is placeholder** (seeded picsum.photos URLs). Subject matter is arbitrary; only crop
  ratio and grayscale treatment are intentional.
- **All body copy about the coach, credentials, client names and result numbers is placeholder.** Get real
  content from the client before launch. Structure and character count are what's designed.

---

## Design system: Modernist

The site is built on a bound design system called **Modernist**. Its complete rules:

- Flat and architectural. **Nothing floats, nothing is decorated.** Alignment and the strength of the
  dividers do all the organising.
- **Zero corner radius everywhere.** `--radius-md` is `0` on purpose. Never round a corner.
- **2px rules**, never hairlines. Section boundaries and grid cell edges are `2px solid var(--color-divider)`.
  Do not soften them to 1px and do not replace them with whitespace.
- **Everything flush left** — headings, body copy, and *the labels inside buttons*. A button wider than its
  label starts the text at the left padding edge, never centered. (In this design: every full-width button
  uses `justify-content: flex-start`.)
- **Near-mono palette.** Ink on a light ground, one red accent used sparingly — the primary button, small
  emphasis marks, numerals. The one place red runs as a full field is the closing poster banner.
- **Photography prints pure black and white** via the `.grayscale` wrapper (`filter: grayscale(1)`).
  Never tint or colorize imagery.
- **Type is Archivo throughout** — headings and body. Headings are weight 800, uppercase, with negative
  letter-spacing.
- Interactive states are themed, never browser defaults. Keyboard focus is
  `outline: 2px solid var(--color-accent); outline-offset: 2px`.

### Design tokens

From `styles.css` `:root`. Port these into your token layer as-is.

**Color roles**

| Token | Value | Use |
| --- | --- | --- |
| `--color-bg` | `#f3f2f2` | Page ground |
| `--color-text` | `#201e1d` | Body and heading ink |
| `--color-accent` | `#ec3013` | Primary action, emphasis marks, large numerals, poster field |
| `--color-divider` | `#c9c6c4` | Every 2px rule |
| `--color-surface` | `#fbfbfb` | Raised surface |

**Ramps.** Every role carries a 100–900 tonal ramp generated in OKLCH on a shared perceptual lightness
scale, so the same step of any ramp has equal visual weight. Steps used in these designs:

| Token | Value | Where used |
| --- | --- | --- |
| `--color-neutral-100` | `#f7f6f6` | Assessment card fill; dark-band heading text |
| `--color-neutral-200` | `#eae8e7` | Page ground behind the mobile device frame |
| `--color-neutral-300` | `#dbd9d7` | Inactive progress segment (mobile) |
| `--color-neutral-400` | `#c8c5c2` | Unchecked step marker border (desktop) |
| `--color-neutral-500` | `#b0aca9` | Unchecked radio border |
| `--color-neutral-600` | `#918d8a` | Muted meta text ("Question 1 of 4") |
| `--color-neutral-700` | `#6e6a67` | Label / caption text; dark-band rules |
| `--color-neutral-800` | `#494644` | Body paragraph text |
| `--color-neutral-900` | `#242220` | Dark band background ("How a session runs") |
| `--color-neutral-300` (on dark) | `#dbd9d7` | Body copy inside the dark band |
| `--color-accent-100` | `#fde8e4` | Assessment option hover fill |
| `--color-accent-400` | `#f2705c` | Accent on dark ground (kickers, step numerals in dark band) |
| `--color-accent-700` | `#b41f08` | **Accent at paragraph text size** — kickers, result stats, error text |

> **Accessibility rule, load-bearing:** `--color-accent` against the ground is tuned to ~3:1 — enough for
> icons, large display type and interface chrome, **not for body copy**. Any accent-colored text at
> paragraph size must use `--color-accent-700`. This is followed throughout both designs; preserve it.

**Type**

- Family: **Archivo** for both `--font-heading` and `--font-body`. Load weights 400, 600, 800.
- Headings: weight **800**, `text-transform: uppercase`, `letter-spacing: -0.03em` (tightening to
  `-0.035em` at display sizes), `line-height: 0.98–1.05`.
- Display headings are pulled left by `margin-left: -0.05em` to optically align the uppercase stem with
  the text column below it. Keep this.
- Body: weight 400, `line-height: 26–28px`, `max-width: 46–62ch` on paragraphs.
- Kickers / labels / captions: 11–13px, `letter-spacing: 0.08–0.12em`, uppercase, `--color-neutral-700`.
- Numerals in step indicators use `font-feature-settings: 'tnum' 1`.

Desktop type scale (all `clamp()`, min → max):

| Element | Size |
| --- | --- |
| H1 hero | `clamp(40px, 5.4vw, 78px)` / line-height 1.0 |
| Poster banner H2 | `clamp(34px, 5vw, 72px)` / line-height 1.0 |
| Section H2 | `clamp(28px, 3.6vw, 50px)` / line-height 1.03–1.05 |
| Stat numeral | `clamp(32px, 3.2vw, 46px)` |
| Assessment question H3 | `clamp(22px, 2.2vw, 30px)` |
| Pillar H3 | 22px |
| FAQ / accordion trigger | 18px, heading font, weight 800 |
| Testimonial blockquote | `clamp(18px, 1.5vw, 22px)` / line-height 1.3 |
| Body | 15–17px |
| Kicker / caption | 11–13px |

Mobile type scale (fixed px at 402 wide):

| Element | Size |
| --- | --- |
| H1 hero | 40px / line-height 0.98 |
| Poster banner H2 | 38px / line-height 0.98 |
| Section H2 | 28–30px / line-height 1.02–1.05 |
| Stat numeral | 34px |
| Question H3 | 22px |
| Pillar / FAQ trigger | 17–19px |
| Body | 15–16px |
| Kicker / caption | 9–12px |

**Spacing.** Density 1.00×; use the `--space-*` scale from `styles.css`. Section padding in these designs:

- Desktop vertical: `clamp(48px, 6vw, 88px)`; horizontal gutter: `clamp(20px, 5vw, 72px)`.
- Desktop split-panel padding: `clamp(40px, 5vw, 80px)` vertical.
- Mobile: 20px gutter throughout; 32–40px vertical section padding.

**Radius:** `0` everywhere. **Shadows:** `--shadow-sm/md/lg` exist but **this design uses none** — no
elevation anywhere. Don't add any.

### Component classes used

From `styles.css`, not hand-rolled: `.nav`, `.btn` + `.btn-primary` / `.btn-secondary`,
`.field` + `label` + `.input`, `.tag` + `.tag-outline`, `.grayscale`. Map each to its equivalent in your
component library rather than re-implementing.

Icons, where any are needed: **Lucide** (https://lucide.dev). The current designs use no icons — geometric
marks only (see below).

### The two recurring geometric marks

Learn these; they appear ~25 times across both files and carry the visual identity.

1. **Accent square** — `width: 9–14px; height: 9–14px; background: var(--color-accent); display: block`.
   A flush-left marker before kickers, pillar names, completed steps, and the confirmation state.
2. **Hollow square** — same box, `border: 2px solid var(--color-neutral-400/500)`, no fill. The unselected
   radio and the incomplete step marker. Selecting fills it solid accent. **These are the radio buttons** —
   square, not circular, no check glyph.

---

## Screens / Views

### DESKTOP — `4EverFit Landing.dc.html`

One continuous page, 12 bands, each separated by a 2px rule. Order matters — it's a funnel.

#### 1. Sticky nav
- `.nav`, `position: sticky; top: 0; z-index: 20`, ground background, 2px bottom rule.
- Padding `18px clamp(20px, 5vw, 72px)`; flex row, `gap: 28px`.
- Left: wordmark **4EverFit** (heading font, 800, 20px, uppercase, `-0.03em`) + **Lifestyle** tagline
  (10px, `0.18em` tracking, uppercase, `--color-accent-700`), baseline-aligned, `gap: 10px`.
- Right group (`margin-left: auto`, `gap: 22px`): text links *Pillars · How it works · Coach · Results*
  (12px, `0.08em`, uppercase) then `.btn.btn-primary` **"Take the assessment"** (12px, `11px 16px`).
- Below 760px the text links hide; the primary button remains.

#### 2. Hero — asymmetric split
- Grid `minmax(0,7fr) minmax(0,5fr)`, 2px rule between columns, 2px bottom rule.
- **Left** (`clamp(40px,6vw,96px)` top padding, vertically centered): H1 in four hard-broken lines —
  "Train with a" / "coach on camera." / **"No guesswork."** (this line in `--color-accent`).
  Then a 17px/28px lede at `max-width: 46ch`. Then two buttons in a `gap: 12px` flex row: primary
  **"Take the 4-pillar assessment"**, secondary **"See how a session runs"** (both `16px 22px`).
  Then an accent-square + reassurance line: *"4 questions · 90 seconds · no card"*.
- **Right**: full-bleed grayscale portrait, `min-height: 520px`, `object-fit: cover`.
- Below 900px: stacks to one column, image cell `min-height: 340px`.

#### 3. Stat row — 4 equal cells
- `grid-template-columns: repeat(4, 1fr)`, 2px rules between cells and below.
- Each cell: numeral (heading 800, `clamp(32px,3.2vw,46px)`, `--color-accent`) over an
  11–12px uppercase caption in `--color-neutral-700`.
- Content: **1:1** "Every session live on camera" · **4** "Pillars in every plan we write" ·
  **45min** "Per session, start to cooldown" (the "min" is `0.45em`) · **0** "Copy-paste programs handed out".
- First cell carries the page gutter as left padding; interior cells `clamp(16px,3vw,40px)`.

#### 4. Four pillars — the centerpiece
Section intro: kicker *"The four-pillar system"* (`--color-accent-700`), H2
**"Pull one out and the whole thing falls over."** (`max-width: 22ch`), then a 56ch paragraph.

Then **4 equal ruled columns**, inset from the page edge by the gutter as *margin* (not padding), with 2px
rules top, bottom, and between columns. Each column: accent square + zero-padded index (`01`–`04`, tabular),
then H3 pillar name (22px uppercase), a 15px/26px paragraph, then three 13px uppercase list items.

| # | Pillar | Sub-items |
| --- | --- | --- |
| 01 | Nutrition | Macro targets · Weekly check-ins · Eating-out playbook |
| 02 | Strength training | Live form coaching · Logged progression · Home or full gym |
| 03 | Cardio | Zone 2 base · Interval blocks · Recovery tracking |
| 04 | Supplementation | Cabinet audit · Evidence-only stack · Dose timing |

> **Breakpoint gotcha, already solved — preserve the fix.** This row and the stat row (#3) collapse to 2-up
> at 1040px and 1-up at 560px. Because the two rows carry their gutter differently (stat row = cell padding,
> pillar row = section margin), they need *different* padding resets when a cell becomes first-in-row. In the
> reference they are tagged `data-r4="bleed"` and `data-r4="inset"` and reset separately. If you collapse
> them with one shared rule you will get either a stray rule at the page edge or pillar headings that no
> longer align with the section heading above them.

An alternative **"ruled rows"** treatment exists behind a prop (`pillarLayout: "columns" | "rows"`): a
`80px / 320px / 1fr` grid per pillar — index, name, description — stacked with 2px rules. Build the columns
version; keep the rows version in mind as the tablet fallback if 2-up columns feel cramped.

#### 5. Dark band — "How a session runs"
The only inverted section. `background: var(--color-neutral-900)`, text `--color-neutral-100`.
- Grid `minmax(0,5fr) minmax(0,7fr)`: grayscale session photo left (`min-height: 460px`, 2px right rule in
  `--color-neutral-700`), content right.
- Kicker in `--color-accent-400` (the on-dark accent step), H2
  **"45 minutes. Camera on. Nothing to figure out."**
- Three steps, each a `64px / 1fr` grid separated by 2px `--color-neutral-700` rules: accent-400 index,
  17–18px uppercase title, `--color-neutral-300` body.
  1. **Warm-up and check-in** 2. **Coached work, rep by rep** 3. **The week, written down**

#### 6. Assessment — the conversion point
Grid `minmax(0,4fr) minmax(0,7fr)`, `gap: clamp(28px,5vw,80px)`, `align-items: start`.
- **Left rail:** kicker *"The 4-pillar assessment"*, H2 **"Four questions. One per pillar."**,
  a 42ch paragraph, and an accent-square reassurance: *"No card. No calls you didn't ask for."*
- **Right — the card:** `border: 2px solid var(--color-text)`, fill `--color-neutral-100`, **no radius, no shadow**.

**Progress header:** 4 equal cells divided by 2px rules, one per pillar (*Nutrition · Strength · Cardio ·
Supplements*). Each shows the hollow square → solid accent square when that pillar is answered, plus an
11px uppercase label.

**Three states** in the card body:

1. **Asking** (steps 0–3) — kicker *"Pillar 0N — <Name>"*, question H3, then 4 full-width option rows.
   Each row: `display: flex; gap: 16px; padding: 18px 8px`, 2px bottom rule, transparent background,
   hollow-square marker, 16px label. **Hover fills `--color-accent-100`.** Selecting a row **advances
   immediately** — no Next button. Footer: **Back** (`.btn-secondary`, hidden on step 0) and
   *"Question N of 4"* right-aligned in `--color-neutral-600`.
2. **Capturing** (step 4) — kicker *"Last step"*, H3 **"Where should we send the plan?"**, a 46ch
   reassurance line, then `.field` + `.input` for **First name** (placeholder "Jordan") and **Email**
   (placeholder "you@work.com"), `max-width: 460px`, inputs `padding: 14px`, `font-size: 16px`.
   Actions: primary **"Send my plan"**, secondary **Back**, and an inline error slot in `--color-accent-700`.
3. **Submitted** — accent square, H3 *"Thanks, {name}."* (falls back to *"Your assessment is in."* when the
   name is blank), a 46ch confirmation paragraph, and a secondary **"Start over"**.

**Validation:** email only, on submit, against `/^[^\s@]+@[^\s@]+\.[^\s@]+$/`. Failure sets the inline
message **"Enter a valid email"**; it clears on any navigation. Name is optional.

Questions and options (verbatim):

| Pillar | Question | Options |
| --- | --- | --- |
| 01 Nutrition | How would you describe your eating right now? | Dialed in and tracked · Mostly clean, but no real plan · Fine on weekdays, gone by Friday · Honestly, no idea |
| 02 Strength training | Where are you with lifting? | Training 3+ days, want progression · On and off for years · Brand new to the barbell · Coming back from an injury |
| 03 Cardio | How is your conditioning? | Running or riding every week · Walks, and that's about it · Winded on the stairs · Competitive — I want more engine |
| 04 Supplementation | What are you taking today? | A full stack — audit it · Protein and that's it · A cabinet full of guesses · Nothing yet |

#### 7. Coach
Grid `minmax(0,5fr) minmax(0,7fr)` — grayscale portrait left (`min-height: 520px`), content right.
Kicker *"Your coach"*, H2 **"One coach. Your whole file."**, two 52ch paragraphs, then a **2×2 credential
grid** with 2px rules: each cell a 13px uppercase title over a 12px `--color-neutral-700` gloss —
*NSCA-CSCS* · *Precision Nutrition L2* · *15 years* · *400+ clients*. **All placeholder.**

#### 8. Results gallery
Kicker *"Results"*, H2 **"Twelve weeks of doing the boring things."** (`max-width: 24ch`).
Three cards, `repeat(3, minmax(0,1fr))`, `gap: clamp(20px,3vw,40px)`. Each card is a **before/after pair**:
a `minmax(0,1fr) minmax(0,1fr)` grid with `gap: 2px` over a `--color-text` background — the ink shows
through as the 2px seam between the two photos. Each photo `aspect-ratio: 3/4`, grayscale, cover.
Caption row below: client + duration left, result stat right in `--color-accent-700`.
*Marcus · 16 weeks / −31 lb · +90 lb squat* — *Priya · 12 weeks / First 5 pull-ups* — *Dev · 20 weeks / Back to sprinting*. **All placeholder.**

> **Gotcha, already solved:** these pair grids **must** use `minmax(0, 1fr)`, not `1fr`. A bare `1fr` keeps
> an `auto` minimum, and a wide image's min-content width blows the track past its card.

#### 9. Testimonials
Three equal cells, 2px rules between, no top/bottom padding trickery — `clamp(32px,4vw,56px)` vertical.
Each: a **heading-font** blockquote (800, `clamp(18px,1.5vw,22px)`, line-height 1.3) using curly quotes,
then a 12px uppercase attribution in `--color-neutral-700`: *Marcus T. · Gym regular*,
*Priya N. · Operations director*, *Dev R. · Masters sprinter*. **Placeholder.**

#### 10. FAQ
Grid `minmax(0,4fr) minmax(0,8fr)`. Left: kicker *"Questions"* + H2 **"Before you book."**
Right: accordion, 2px rule between rows. Trigger = full-width button, heading font 800/18px, question left
and a **+ / – sign** right in `--color-accent` (body font, 20px). Hover turns the label
`--color-accent-700`. Answer: 16px/28px, `max-width: 62ch`. **Single-open**; desktop opens item 1 by
default, mobile opens none. Five items: *Do I need a gym?* · *What does a session actually look like?* ·
*Is nutrition a separate service?* · *How often do the four pillars get revisited?* ·
*What happens after I take the assessment?*

#### 11. Poster banner
Full-bleed `background: var(--color-accent)`, text `--color-bg`.
`clamp(48px,6vw,96px)` vertical padding. H2 in three hard-broken lines — **"Four pillars." / "One coach." /
"Starting Monday."** — at `clamp(34px,5vw,72px)`, line-height 1.0, `margin-left: -0.05em`.
Then an inverted button (ground fill, ink label) **"Take the assessment"** and a 12px uppercase
*"4 questions · 90 seconds"*. This is the one place red runs as a field — keep it loud and keep it last.

#### 12. Footer
36px padding, 2px top rule, single flex row: wordmark + Lifestyle tagline, and right-aligned
*"Nutrition · Strength · Cardio · Supplementation"* in 13px `--color-neutral-700`.

---

### MOBILE — `4EverFit Mobile.dc.html`

Authored at **402 × 874**. 20px gutter, 44px minimum tap target, 48–60px on primary controls.
Same content and same funnel order; different mechanics.

1. **Sticky header** — 20px gutter, 2px bottom rule. Wordmark + tagline left; a **hamburger** right
   (44×44 tap area, three bars, the third 16px wide and in `--color-accent`).
2. **Full-screen drawer** — opens over the page in **solid `--color-accent`**. Four links at
   **30px heading-800 uppercase** in `--color-bg`, each with a 2px `--color-bg` top rule
   (*Pillars · Sessions · Coach · Results*), then an inverted full-width CTA. A text **Close** at top right.
   > Implementation note: in the prototype the drawer is `position: sticky; top: 0; height: 874px;
   > margin-bottom: -874px` — a workaround for pinning inside a scroll container. In a real app use
   > `position: fixed; inset: 0` and lock body scroll while open.
3. **Hero, stacked** — accent square + *"One-on-one video coaching"*, H1 in **four** hard-broken lines
   (40px), 16px/26px lede, then a **full-width** primary button (`justify-content: flex-start` — label stays
   flush left). Photo follows *below* the text as a 420px band with 2px rules top and bottom.
4. **Stat block — 2×2 grid** with 2px rules; 34px accent numerals, 11px captions.
5. **Pillars — accordion, not columns.** Intro line becomes *"Tap a pillar to see how we run it."*
   Each row: 64px min-height trigger with accent square + index + name + `+`/`–` sign. Open body: 15px/26px
   paragraph plus the three sub-items as **`.tag.tag-outline` chips** in a wrapping flex row.
   Single-open, **pillar 01 open by default** so the pattern is discoverable.
6. **Dark band** — photo first (300px), then kicker, H2, three ruled steps.
7. **Assessment** — full-bleed card (2px top/bottom rules only, no side borders).
   Progress becomes **four 6px bars** with 9px labels (*Nutrition · Strength · Cardio · Supps*) — accent when
   done, `--color-neutral-300` when not. One question per view; option rows are 60px min-height, edge-to-edge,
   16px labels, 16px markers. Inputs 48px min-height, **`font-size: 16px`** (prevents iOS zoom-on-focus).
   Submit is a full-width 52px primary button; Back and the error message sit on the row below.
8. **Coach** — portrait (420px) above copy; credentials become a **2×2** grid with shortened labels
   (*NSCA-CSCS* · *PN Level 2* · *15 years* · *400+ clients*).
9. **Results — horizontal carousel.** `overflow-x: auto`, `scroll-snap-type: x mandatory`, 280px cards,
   `scroll-snap-align: start`, 20px inline padding, scrollbar hidden. A 12px *"Swipe →"* affordance sits under
   the heading. Same 2px-seam before/after pair; shortened stats (*−31 lb*).
10. **Testimonials — carousel** of 320px cells with 2px left rules, same snap behavior.
11. **FAQ** — same accordion, 17px triggers, 60px min-height, **none open** by default.
12. **Poster banner** — 38px three-line H2, full-width inverted button.
13. **Footer** — stacked wordmark/tagline and pillar line.
14. **Sticky bottom CTA bar** — `position: sticky; bottom: 0`, ground fill, **2px `--color-text` top rule**
    (heavier than a divider on purpose), `padding: 12px 20px 40px` (the 40px clears the home indicator).
    A flex-1 primary button **"Take the assessment"** plus a 74px-wide 10px caption *"4 questions · 90s"*.

**Desktop responsive collapse** (in the desktop file, via media queries):

| Breakpoint | Change |
| --- | --- |
| ≤ 1040px | 4-col rows → 2-up; first-in-row cells drop `border-left` and reset padding per row type |
| ≤ 900px | All 2-col splits → 1 column; side borders removed; image cells `min-height: 340px` |
| ≤ 760px | Nav text links hide; primary button stays |
| ≤ 560px | 4-col rows → 1-up; 3-col rows → 1-up |

---

## Interactions & behavior

- **Assessment quiz.** Linear, 4 steps + capture + confirmation. Picking an option records the answer **and
  advances in the same action**. Back steps one view and clears any error. Answers persist when navigating
  back, and the previously chosen option renders selected. `Start over` resets everything.
- **Accordions.** Single-open (FAQ, mobile pillars). Clicking the open item closes it. Sign toggles `+` → `–`.
- **Nav.** In-page anchor links with `scroll-behavior: smooth`, guarded by
  `@media (prefers-reduced-motion: reduce) { scroll-behavior: auto }`.
- **Carousels (mobile).** Native scroll-snap only — no JS, no dots, no arrows. Scrollbars hidden via
  `scrollbar-width: none` + `::-webkit-scrollbar { display: none }`.
- **Hover.** Assessment options tint `--color-accent-100`; FAQ triggers shift label to `--color-accent-700`;
  buttons take the design system's built-in ramp hover. No transforms, no lifts, no scale.
- **Motion.** Deliberately almost none. This system is static and architectural — accordions and state
  changes are instant. Do not add reveal-on-scroll, parallax, or entrance animations.
- **Focus.** `:focus-visible { outline: 2px solid var(--color-accent); outline-offset: 2px }` from the
  design system. Never suppress it.

### Accessibility work still to do

The prototypes use plain `<button>` elements without ARIA. In production:
- Accordions: `aria-expanded` + `aria-controls`, panel `id`s, and the `+`/`–` marked `aria-hidden`.
- Quiz options: a `radiogroup` with `aria-checked`, or radio inputs styled as the square markers, and
  arrow-key navigation within the group.
- Progress header: `aria-current` on the active pillar; announce step changes via a polite live region.
- Validation error: `aria-live="polite"`, `aria-describedby` on the email input, `aria-invalid` on failure.
- Mobile drawer: focus trap, `Esc` to close, `aria-expanded` on the trigger, return focus on close.
- Give every image real `alt` text; the decorative accent squares must be `aria-hidden`.

## State management

Local to the page — no server state, no router. Both designs use the same shape:

```
step:       0..4      // 0-3 = question index, 4 = email capture
answers:    [4 × string | null]
name:       string
email:      string
submitted:  boolean
error:      string    // "" or "Enter a valid email"
openFaq:    number    // index, -1 = none. Desktop defaults 0, mobile -1
openPillar: number    // mobile only, defaults 0
menuOpen:   boolean   // mobile only
```

Derived, not stored: `asking = step < 4 && !submitted`, `capturing = step >= 4 && !submitted`,
`canGoBack = step > 0 && !submitted`, `progressLabel = "Question " + (min(step,3)+1) + " of 4"`,
`thanksTitle = name ? "Thanks, " + name + "." : "Your assessment is in."`, and per-step
`done = !!answers[i]`.

**Backend work required — currently stubbed.** `submit` only flips `submitted: true`. To ship:
1. `POST` `{ name, email, answers: [4 strings] }` to your endpoint or CRM/ESP.
2. Add pending and failure states to the submit button (the design has neither — a disabled 45%-opacity
   state exists in the system, and the inline error slot in `--color-accent-700` can carry a network error).
3. Send the coach a notification and the lead a confirmation email.
4. Consider a spam guard (honeypot or token) — there is no captcha in the design and adding a visible one
   would break the card's rhythm.

Analytics worth instrumenting: assessment start, per-step completion (to find the drop-off pillar),
capture-view reach, and submit success.

## Assets

**All photography is placeholder** — seeded `picsum.photos` URLs, wired into the prototype's drag-and-drop
`<image-slot>` elements. Replace all of them and delete `image-slot.js`.

Slots to fill, with intended crop:

| Slot id (desktop / mobile) | Subject | Ratio |
| --- | --- | --- |
| `hero-portrait` / `m-hero` | Hero — athlete mid-lift | Portrait ~3:4 (desktop fills a 5/12 column ≥520px tall; mobile a 420px band) |
| `session-photo` / `m-session` | A live one-on-one video session | Landscape-ish (desktop 5/12 col ≥460px; mobile 300px band) |
| `coach-portrait` / `m-coach` | The coach | Portrait ~3:4 |
| `res-{1,2,3}-{before,after}` / `m-res-…` | Client before/after, 3 pairs | **3:4 each, shot consistently** — same framing, distance and lighting per pair, or the comparison reads as a trick |

Delivery notes: supply at ≥2× the CSS box, export WebP/AVIF with JPEG fallback, lazy-load everything below
the hero, and set explicit `width`/`height` to avoid layout shift. Do **not** pre-desaturate the files —
grayscale is a CSS filter so the client can revisit the treatment later.

**Fonts:** Archivo (400/600/800). Self-host via `@font-face` with `font-display: swap` rather than a
third-party CDN.

**Icons:** none used. Lucide if any become necessary.

**Logo:** there is no logo file — the mark is set type ("4EverFit" in Archivo 800 uppercase with the
"Lifestyle" tagline). If the client has a real logo, it replaces the wordmark in the nav, mobile header,
drawer and footer.

## Files in this bundle

| File | What it is |
| --- | --- |
| `4EverFit Landing.dc.html` | Desktop design reference (responsive) |
| `4EverFit Mobile.dc.html` | Mobile design reference (402×874) |
| `styles.css` | **Modernist design system stylesheet — the token source of truth. Port this.** |
| `ds-readme.md` | The Modernist design system guide in full |
| `theme.json` | Machine-readable record of the theme parameters |
| `image-slot.js` | Prototyping-only image placeholder. **Do not ship.** |
| `ios-frame.jsx` | Prototyping-only device bezel around the mobile design. **Do not ship.** |
| `support.js` | The prototype's component runtime. **Do not ship.** Reference only. |

### Reading the reference files

They are single-file components: a `<x-dc>` template plus a `class Component extends DCLogic`.
Translating to a normal framework:

| In the reference | Means |
| --- | --- |
| `{{ value }}` | Interpolation |
| `<sc-if value="{{ x }}">` | Conditional render |
| `<sc-for list="{{ xs }}" as="x">` | List render; `$index` in scope |
| `onClick="{{ handler }}"` | Event binding |
| `renderVals()` | Returns everything the template reads — read it first to understand a screen |
| `style-hover="…"` | A `:hover` rule |
| `<image-slot>` | Where an `<img>` goes |
| `hint-*` attributes | Prototype streaming hints — ignore entirely |

All styling is inline in the reference (a constraint of the prototyping runtime). **Do not carry that
forward** — extract to classes, utilities, or styled components as your codebase does, driven by the tokens
in `styles.css`.

## Suggested build order

1. Port tokens and load Archivo; verify radius 0 and the 2px rule weight render correctly.
2. Build primitives: Button (3 variants, flush-left label), Input/Field, Tag, Accordion, RuledGrid, Figure.
3. Static desktop page top to bottom; get the rules and the collapse behavior right before any JS.
4. The assessment component with full state, validation and a11y.
5. Mobile: drawer, pillar accordion, carousels, sticky CTA bar.
6. Wire the form to a real endpoint; add pending/error states.
7. Swap in real photography and real copy.
