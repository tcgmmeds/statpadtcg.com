# Statpad TCG website

The website for **Statpad TCG**, served at [statpadtcg.com](https://statpadtcg.com) by GitHub Pages.

It is plain HTML, CSS and JavaScript. There is nothing to install or build: each page is one file that holds its own styles and scripts.

## Pages

| File | Address | What it is |
| --- | --- | --- |
| `index.html` | `/` | Landing page with the waitlist form |
| `privacy.html` | `/privacy` | Privacy Policy |
| `terms.html` | `/terms` | Terms of Service |
| `reset-password.html` | `/reset-password` | Lets someone set a new password from the link in a reset email |

## Other files

| File | What it is |
| --- | --- |
| `CNAME` | The domain GitHub Pages serves the site on (`statpadtcg.com`) |
| `assets/logo.png` | The logo at full size (1024px), copied from the app |
| `assets/logo-320.png` | A small copy of the logo. This is the one the pages load, so they stay fast |
| `favicon.ico`, `favicon.png` | The icon in the browser tab, made from the app icon |
| `apple-touch-icon.png` | The icon used when the site is saved to an iPhone home screen |

## Preview on your computer

From this folder, run:

```bash
npx serve
```

Then open the address it prints (usually <http://localhost:3000>). Press `Ctrl+C` in the terminal to stop it.

Use `npx serve` rather than opening the files by double-clicking: the links between pages are written as `/privacy` and `/terms`, which only work through a server.

## Brand

- Accent: champagne `#D9B65D`
- Background: near-black `#0a0a0b`
- Fonts: DM Sans (text) and Space Mono (logo, labels)
- Contact email: `support@statpadtcg.com`

The colours are set once at the top of each page's `<style>` block.

## Services the site talks to

- **Mailchimp** receives waitlist sign-ups. The form's address is in the script at the bottom of `index.html` (the `list-manage.com` line).
- **Supabase** handles the password reset. The project address and public key are in the script at the bottom of `reset-password.html`. It is the same Supabase project the app uses.

## Publishing

Work on a branch, check it locally, then merge into `main`. GitHub Pages publishes `main`.

## Disclaimer

Statpad TCG is an unofficial fan-made app. It is not affiliated with, endorsed by, or sponsored by Bandai or the One Piece franchise. Card names and images belong to their respective owners.
