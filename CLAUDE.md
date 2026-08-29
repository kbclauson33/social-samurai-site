# Social Samurai — promo site

Promotional + purchase website for Social Samurai, the live team game
(one big screen, phones as controllers, a "sensei" hosts). This repo is the
marketing site only — the game/backend lives in `social-samurai`.

## Commands

No build step, plain static files. Preview locally:

```bash
python3 -m http.server 8000
```

## Where things live

- `index.html` — the whole landing page (styles + purchase logic inline)
- `privacy.html`, `terms.html` — legal drafts (marked Draft until counsel pass)
- `docs/PLAN.md` — domain decision, billing plan, legal checklist, launch checklist

## Decisions and constraints

- **Static, no build step, forever if possible** — same philosophy as the game;
  it's why margins and deploys stay trivial.
- **Pricing is the teardown Rev. 2 ladder** ($299 / $900 / $4,800 / $15k+).
  Don't change numbers on the page without changing the teardown thinking.
- **Purchasing = Stripe Payment Links** pasted into the `TIERS` object at the
  bottom of `index.html`. Empty link → button opens the email-fallback dialog
  (intentional: no dead buttons pre-Stripe). `?checkout=success` shows the
  thanks banner.
- **Brand**: washi paper / sumi ink / hanko seal-red (`--seal`), Shippori Mincho
  display + IBM Plex Sans/Mono. Light and dark both supported via tokens.
- Contact email is `hello@socialsamurai.io` — if the domain decision changes,
  replace it in all three HTML files.

## Gotchas

- The game was built on Base time — **IP ownership must be settled in writing
  before the first sale** (see docs/PLAN.md §4).
- Legal pages carry a visible "Draft" box on purpose. Remove only after counsel.
