# Statpad TCG website: project doc

## Overview
statpadtcg.com is the marketing site for the Statpad TCG iOS app. It is a static site on GitHub Pages (repo `tcgmmeds/statpadtcg.com`) with a custom domain registered at Porkbun. Support email: support@statpadtcg.com.

## Stack and structure
Plain HTML, CSS and JavaScript. No build step; each page holds its own styles and scripts. GitHub Pages publishes `main`.

- `index.html`: landing page with the waitlist form (Mailchimp sign-ups).
- `privacy.html`: Privacy Policy.
- `terms.html`: Terms of Service.
- `reset-password.html`: lets someone set a new password from a reset email (Supabase).
- `delete-account.html`: explains how to request account and data deletion.
- `CNAME`: custom domain for GitHub Pages (`statpadtcg.com`).
- `README.md`: overview, preview instructions, brand notes.
- `assets/logo.png`, `assets/logo-320.png`: logo at full and small size.
- `assets/og-image.png`: 1200x630 link-preview image.
- `favicon.ico`, `favicon.png`, `apple-touch-icon.png`: site and home-screen icons.
- `404.html`: GitHub Pages fallback page. For `/d/<share_id>` it renders a shared deck; anything else shows the normal 404.
- `config.js`: public client config (Supabase URL and publishable key) for `404.html`.
- `cards.json`: card lookup data copied from the app repo (see "Deck share pages").
- `.well-known/apple-app-site-association`: universal-links file for the app.
- `.nojekyll`: makes Pages publish dot-folders like `.well-known`.
- `docs/PROJECT.md`: this file.

## Deck share pages
- URL: `https://statpadtcg.com/d/<share_id>`. It is served through `404.html` (the Pages fallback), so the HTTP status is 404 but the page renders. `share_id` must match `^[A-Za-z0-9_-]{8,32}$`; anything else shows the normal 404.
- The page calls the Supabase RPC `get_shared_deck({ p_share_id })` with the publishable key from `config.js`. Response: `{ name, leader_card_id, cards: [{ card_image_id, quantity }] }`, or `null` ("This deck link doesn't exist or is no longer shared").
- `cards.json` comes from the app repo (`scripts/exportWebCards.js` writes `web-export/cards.json`). Format: `{ generatedAt, fields, cards: { baseId: [name, color, type, cost, set] } }`. Lookup is by exact id, then base id (everything after `_` stripped).
- Layout: text only. Header with deck name, leader, color chips and card count; Character/Event/Stage sections sorted by cost then name. Buttons: Open in Statpad (`statpad://d/<id>`), Get Statpad (homepage, "Coming soon to iOS"), Copy deck list (`1x` leader first, then `NxBASEID` lines).
- Universal links: `/.well-known/apple-app-site-association` with appID `NAJBBUUZ42.com.tcgmmeds.onepiecetcg` for `/d/*`. `.nojekyll` makes Pages publish `.well-known`. Verified live with curl.

## Recurring task
After every new set import in the app: re-run `exportWebCards.js` in the app repo, copy `web-export/cards.json` here, commit and push.

## Rules
- Dark/gold trophy-and-cards branding.
- No straw hat, and no official One Piece art, logos or names.
- Until the App Store release the site says "Coming soon to iOS", with no App Store link and no Android mention.
- The trailer goes up at launch, not before.
- No TestFlight links.
- Only the publishable/anon key ever goes in `config.js`. Never a secret or `service_role` key.
- No official One Piece logos or card art anywhere on the site, including the deck pages.

## TODO
- When v1.0 is live: check that https://apps.apple.com/app/id6759857731 loads, then merge PR #11 (App Store launch). It also edits this file, so resolve any conflict here first.
- After PR #11 is live: on an iPhone, check that the Smart App Banner appears on the homepage and a deck page, and see where its Open button lands.
- At App Store release: email the Mailchimp waitlist (the sign-up success message promises it).
- At launch: add the trailer to the site.
- Link previews: the app repo has a merged Cloudflare Worker for them (`onepiece-tcg-app` PR #88: deck name, leader and colors, with one fixed picture). It is not live yet; follow `cloudflare/link-previews/README.md` there for setup, DNS cutover and testing.
- Test universal links on a device once app build 32 is live.
- Check the waitlist success message in a browser after the TestFlight removal (not needed once PR #11 is merged).
- Review the old `feature/*` and `fix/mailchimp-jsonp` branches on the remote and delete any that are already merged.

## Known issues
- v1.0 is not on the App Store yet: the link returned 404 on 2026-11-27, so PR #11 is waiting.
- Shared deck links get no preview in chat apps: `/d/<share_id>` returns HTTP 404 with no preview tags (checked 2026-11-27).
- In PR #11 (not live yet): the Smart App Banner has no `app-argument`, so its Open button may not open the deck (untested). The banner tag also applies to the normal 404 page.
- Once the Cloudflare Worker is live, it sets the preview tags on `/`, `/privacy`, `/terms` and deck links (per PR #88), so check it when changing preview tags here.

## Session log
- 2026-11-23: Created this project doc.
- 2026-11-23: Removed all TestFlight links and mentions from the site.
- 2026-11-23: Deleted the already-merged `feature/testflight-button` branch from the remote. Updated the TODO.
- 2026-11-25: Built deck share pages (PR #9, merged): `/d/<share_id>` via `404.html`, Supabase `get_shared_deck` RPC, `cards.json` lookup, text-only layout with Open in Statpad / Get Statpad / Copy deck list buttons, universal-links AASA file and `.nojekyll`. Details in "Deck share pages". Added the recurring cards.json refresh task and the new TODOs.
- 2026-11-27: Opened PR #11 (App Store launch), left unmerged until v1.0 is live: App Store badge on the homepage and page footers, email sign-up and "Coming soon to iOS" removed, static Smart App Banner, "Get Statpad" linking to the App Store, new link-preview image and text, OPTCG wording, one shorter homepage disclaimer, README and project doc updates. Decided to keep "One Piece" in the other pages' disclaimers and in the privacy and terms text. Checked locally in headless Chrome, not on an iPhone.
- 2026-11-27: Updated the TODO and known issues.
