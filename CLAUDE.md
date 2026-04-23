# nova-tech.dk

Personal website for Mikey Bruun Andersen — software consultant, Aarhus, Denmark.
Digital business card. One job: give the right person enough to say "let's talk."

## Stack
- Astro 6, `output: 'static'`
- Vanilla CSS — no Tailwind
- Deploy: GitHub Actions → One.com FTP on push to `main`

## Site structure
Single page (`/`). All navigation uses anchor links.

| Component       | Section id  | Background        |
|-----------------|-------------|-------------------|
| Nav.astro       | —           | --color-forest    |
| Hero.astro      | —           | --color-forest    |
| Values.astro    | —           | --color-white     |
| About.astro     | #om-mig     | --color-bg-tint   |
| Contact.astro   | #kontakt    | --color-white     |
| Footer.astro    | —           | --color-forest    |

`EarDecoration.astro` — inlined logomark SVG used as hero background overlay.
`Layout.astro` — HTML shell (head, meta, Google Fonts preconnect).

## Brand tokens  (`src/styles/global.css`)
```
--color-forest:  #004A31   dark green (primary, nav/hero/footer bg)
--color-mint:    #8FE1B0   light green (accents, value bullets)
--color-solar:   #F2C744   yellow (CTAs, "Tech" wordmark)
--color-black:   #121212
--color-bg-tint: #f0faf5   alternating section tint
```
Font: Roboto 300/400/500/700 via `@import` in global.css.

## Assets
- `src/assets/logo.svg` — full horizontal wordmark (582×120)
- `src/assets/logomark.svg` — mark only (the three ear shapes, ~124×124)
- Both are also copied to `public/` for direct URL access

## Contact form
`Contact.astro` currently has `action="#"`. To go live:
1. Sign up at formspree.io (free tier: 50 submissions/month)
2. Create a form → copy the endpoint URL
3. Replace `action="#"` with the endpoint

## Deploy
Push to `main` triggers `.github/workflows/deploy.yml` (SFTP via wlixcc/SFTP-Deploy-Action@v1.2.4).
Required GitHub secrets (Settings → Secrets → Actions):
- `SFTP_HOST`      — One.com Control Panel → Advanced → SSH & SFTP
- `SFTP_USERNAME`  — same section
- `SFTP_PASSWORD`  — set via One.com's password email flow
- `SFTP_PORT`      — 22

Build output (`./dist/*`) is uploaded to `/www` on the server.
