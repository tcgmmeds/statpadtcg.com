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
- `docs/PROJECT.md`: this file.

## Rules
- Dark/gold trophy-and-cards branding.
- No straw hat, and no official One Piece art, logos or names.
- Until the App Store release the site says "Coming soon to iOS", with no App Store link and no Android mention.
- The trailer goes up at launch, not before.
- No TestFlight links.

## TODO
-

## Known issues
-

## Session log
- 2026-11-23: Created this project doc.
