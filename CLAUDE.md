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

- `index.html` — landing page: live self-playing game demo (hero), Meet
  dual-control mock, plans, FAQ, login + buy dialogs. All inline.
- `premium.html` — premium features, paid tiers, comparison matrix.
  Its `TIERS` object must stay in sync with index.html's.
- `privacy.html`, `terms.html` — legal drafts (marked Draft until counsel pass)
- `docs/PLAN.md` — domain decision, billing plan, legal checklist, launch checklist

## The design system is the GAME's, not ours

Every token, face and motif on this site is copied verbatim from
`social-samurai/web/game/styles.css` and `app.js`. Do not invent a new visual
language here — if the game changes, this site follows it.

- Tokens: `--bg #141114`, `--stage #0f0c0e`, `--ink #ede4d3`, `--paper #e9dfcc`,
  `--red #a8232a` (+ red-2/3/4), `--gold #e8c063`, belts array.
- Faces: Palatino serif display (wide tracking), Hiragino Mincho for kanji
  (Noto Serif JP webfont fallback), system sans for labels.
- Motifs: the ensō drawn with the game's `#brush` feTurbulence filter, the
  paper-grain `.ss-noise` overlay, giant faint kanji ghosts, 「corner brackets」
  on codes, tiny wide-tracked uppercase micro-labels.
- `kamon()` and the GRADS/BELTS arrays are **ported verbatim** from `app.js`, so
  the crests here are the same crests the game draws. Re-copy rather than edit.
- Committed dark. There is no light theme — the dojo has one light.

Vocabulary is the game's: dojo, sensei, samurai, THE SCROLL 巻物 (Strike /
Gauntlet / Unfurling), THE COUNCIL 評定 (Your Pick 心 / The Crowd 衆),
HONOUR 誉, standings 名誉, belts, Shogun.

## The hero stage

A scripted replay of a real dojo using the real phases: lobby → scroll →
strike → honour struck → council → standings. Prompts come from the game's
`questions.js`. Pauses off-screen, resets scores each loop, reduced-motion safe.
`PLAY_URL` (index.html) routes "Try for Free" to the hosted free dojo when live.

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
