# 4Ever Fit Lifestyle — marketing site

Astro + Tailwind. Structure, copy and the assessment-quiz/drawer engineering carry forward from the
original design handoff (`../4EverFit Landing.dc.html` / `../4EverFit Mobile.dc.html`), but the **visual
system was fully redesigned** around the client's actual badge logo — see `../PRODUCT.md` and
`../DESIGN.md` at the project root for the full rationale, palette, and type system ("Cast Bronze").
The original flat, zero-radius "Counted Weight" system documented lower in git history was built around a
different, since-abandoned logo direction and no longer applies.

## Commands

| Command | Action |
| --- | --- |
| `npm install` | Install dependencies |
| `npm run dev` | Dev server at `localhost:4321` |
| `npm run build` | Production build to `./dist/` |
| `npm run preview` | Preview the production build locally |

## What's implemented

- **Cast Bronze design system** in `src/styles/global.css` — dark warm ground (`--color-bg`), a light
  "paper" surface used only for the assessment card / result cards / credential chips, and one bronze
  accent lifted from the badge logo. Mapped into Tailwind via `@theme inline`. See `../DESIGN.md`.
- The client's actual badge logo (`public/logo/4everfit-badge.png`) via `src/components/Logo.astro` — a
  small icon next to a Fraunces wordmark at nav/footer sizes, full-size with a one-time bronze sheen sweep
  in the hero.
- Three AI-generated mood photographs (`public/img/*.jpg`, via Higgsfield) standing in for hero, "how a
  session runs," and coach imagery — matched to the Cast Bronze palette so the page reads as intended
  before real photography exists. **Replace with real photography before launch**, same as the
  results/testimonial picsum.photos placeholders.
- One responsive page (`src/pages/index.astro`) containing **two** parallel layout trees — a desktop tree
  (`hidden sm:block`) and a dedicated mobile tree (`sm:hidden`), same architecture as the original build.
- The assessment quiz (`src/scripts/assessment.ts`) — unchanged logic, restyled. Its **confirmation state
  now hands off to the app** instead of promising a follow-up email: "get the app to see your plan," with
  App Store / Google Play badge links (currently `href="#"` placeholders — wire up real store links before
  launch). This reflects the updated purpose in `../PRODUCT.md`: the assessment is the on-ramp to the app,
  not a stand-alone lead-gen form.
- Mobile drawer nav (`src/scripts/drawer.ts`) — unchanged, focus trap/Esc/scroll-lock all still wired.
- Reveal-on-scroll (inline script at the bottom of `index.astro`) — staggered per section/card, enhances an
  already-visible default (content isn't hidden if JS fails or `prefers-reduced-motion` is set), fully
  reduced-motion safe.

## Known gaps before this ships

- **Fonts are loaded from Google Fonts** (Fraunces + Inter), not self-hosted — swap for self-hosted
  `@font-face` in `src/layouts/Layout.astro` before launch.
- **AI-generated placeholder photography** (hero/session/coach) and **picsum.photos placeholder
  photography** (results) — both need replacing with real client photography before launch, along with all
  placeholder body copy, credentials, client names/results, and FAQ answers.
- **The submit handler POSTs to `/api/assessment`, which doesn't exist yet** — no backend in this static
  build; the fetch failure is swallowed so the confirmation state still shows. Wire up a real endpoint (or
  CRM/ESP) before launch.
- **App Store / Google Play links are `href="#"` placeholders** in the assessment's confirmation state —
  point them at the real app listings once published.
- This sandbox couldn't run a headless browser for a final visual QA pass (no system deps, no sudo) — the
  production build (`npm run build`) completes cleanly and was checked structurally, but run `npm run dev`
  and eyeball all four lockups (desktop nav/footer, mobile header/footer) and both breakpoints for real
  before shipping.
