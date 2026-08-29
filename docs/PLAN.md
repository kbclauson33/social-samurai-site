# Social Samurai — site, billing & legal plan

Working plan for everything around the website. Written 2026-08-29.
The game itself (backend rebuild) is a separate track in the `social-samurai` repo.

---

## 1. Domain — decision needed (one question)

Checked live on GoDaddy, 2026-08-29:

| Domain | Status | Price |
|---|---|---|
| **socialsamurai.io** ← recommended | Available | $89.99/yr (promo: $179.99 for 3 yrs today) |
| playsocialsamurai.com | Available | $22.99/yr ($45.99 for 3 yrs today) |
| socialsamurai.games | Available | $9.99 first yr, $51.99 renewal |
| socialsamurai.co | Available | $59.99/yr ($119.99 for 3 yrs today) |
| samurai.social | Premium resale | $100 once + ~$35/yr renewal |
| socialsamurai.com | Premium resale | $9,995 (or lease $479.76/mo) — skip |

**Recommendation: buy `socialsamurai.io`** (exact brand name, standard SaaS TLD,
credible to a People Ops buyer), and optionally add `playsocialsamurai.com`
($23) as a redirect so the .com pronunciation of the pitch still lands somewhere.

To buy (Kaben, ~3 minutes, phone works):
1. Open godaddy.com and sign in.
2. Search `socialsamurai.io`.
3. Add to cart → decline the upsells (no website builder, no email bundle; free WHOIS privacy is included).
4. Check out. Done.

All email links in the site currently use `hello@socialsamurai.io` — if a
different domain is chosen, search-and-replace across `index.html`,
`privacy.html`, `terms.html`.

## 2. Site — what's built and what's next

**Built (v1, this repo):** static, no build step — same philosophy as the game.
- `index.html` — landing page: hero, how-it-works, features, pricing ladder, agency comparison, FAQ, footer.
- `privacy.html`, `terms.html` — full drafts (marked draft, counsel review before first sale).
- Menus: How it works · Pricing · For companies · FAQ, plus footer legal links.

**Positioning on the page** (from the Aug 26 commercial teardown): sell against
the $320 hosted agency session — "$299 tonight, and nobody has to schedule a stranger."
Pricing ladder is the teardown Rev. 2 ladder: $299 event / $900 Team /
$4,800 Company (highlighted) / $15k+ Enterprise.

**Next content upgrades (in order of impact):**
1. Three customer logos + one verbatim quote from a game night (teardown Q13/Q15).
2. 20–30s screen recording of the intro sequence + a reveal round in the hero.
3. A free sample of 10 questions as a lead magnet (content route B from the teardown).

## 3. Billing — how we take money

**Phase A — now (no backend needed, matches the current static site):**
1. Create a Stripe account (Kaben — identity + bank details, ~15 min).
2. In the Stripe dashboard create 3 products / 4 prices:
   - Single Event — $299 one-time
   - Team — $900/yr recurring
   - Company — $4,800/yr recurring
   - (Enterprise stays "talk to us" — invoiced manually via Stripe Invoicing.)
3. Create a **Payment Link** for each (dashboard button, no code).
   Set the after-payment redirect to `https://<domain>/?checkout=success`.
4. Paste the three URLs into the `TIERS` object at the bottom of `index.html`.
   That's the whole integration — buttons then go straight to Stripe Checkout.
5. Turn on **Stripe Tax** in the dashboard so sales tax/VAT is handled automatically.
6. Turn on the email receipt setting.

Until the links are pasted, every Buy button opens a dialog that falls back to
a pre-filled email — no dead ends, every click capturable from day one.

**Fulfillment in Phase A is manual by design** (mirrors teardown Phase 1
"sell it before you build it"): Stripe emails you on each purchase → you reply
within one business day to schedule the night / set up the team. Fine below
~10 sales/week.

**Phase B — when accounts/orgs exist (game repo Phase 3):**
- Replace Payment Links with server-created Stripe Checkout Sessions tied to an org.
- Webhooks: `checkout.session.completed` → provision org/seats;
  `customer.subscription.deleted` / `invoice.payment_failed` → downgrade.
- Customer Portal (dashboard toggle) for self-serve card changes + cancellation.
- Keep Enterprise on invoicing.

**Refund policy (already on the site, honor it):** technical failure kills a
paid night → full refund; Single Event refundable up to 48h before; annual
plans cancel anytime, run to end of year.

## 4. Legal — checklist before first paid customer

- [ ] **IP ownership** — the game was built during Base work sessions in a Base
      repo. Read the employment agreement; get written confirmation from Base
      before taking a dollar. (Teardown flags this as the one thing that can
      invalidate everything else. Cleanest resolution: Base as first customer.)
- [ ] Counsel pass on `privacy.html` and `terms.html` (both marked Draft).
- [ ] Entity + governing law: terms currently say Texas — confirm, and decide
      whether to form an LLC before revenue (recommended; ~$300 in TX).
- [ ] DPA template for Company/Enterprise buyers (only needed once game
      history ships; EU customers will ask).
- [ ] Subprocessor list page (Stripe, Supabase, host) — stub exists in privacy policy.
- [ ] Stripe Tax registration thresholds — Stripe surfaces these; no action until sales exist.

## 5. Hosting

Static files → GitHub Pages (free, this repo, custom domain + HTTPS) or
Cloudflare Pages. Recommendation: **GitHub Pages** — Kaben's flow is
GitHub-first and there's no build step. DNS: point the GoDaddy A/CNAME records
at Pages, flip on HTTPS. 10 minutes.

## 6. Launch checklist

- [ ] Buy domain (§1) — **the one blocking decision**
- [ ] Enable GitHub Pages on this repo + connect domain
- [ ] Stripe account + 3 Payment Links pasted into `TIERS` (§3)
- [ ] Set up `hello@` mailbox (GoDaddy forward or Google Workspace) — buttons already point at it
- [ ] IP ownership answer in writing (§4)
- [ ] Counsel pass on legal pages
- [ ] Logos + quote on the page
- [ ] Run 5 paid $299 nights by hand (teardown Phase 1) before building more software
