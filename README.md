# Poppyhill: Website

A one-page site for Poppyhill, which provides Solo and self-directed 401(k) plan support from an
office in Los Angeles, California. It's static with no dependencies, built with Node and hosted on
**Cloudflare** (Workers static assets via `wrangler.jsonc`, or Pages).

## Quick start

```bash
node build.mjs          # builds ./dist; checks internal links; lists missing info
STRICT=1 node build.mjs # pre-launch check (fails while placeholders remain)
```

## Deploy to Cloudflare

**Workers (current setup):** Workers & Pages → Create → Import a repository → this repo.
Build command `npm run build`, deploy command `npx wrangler deploy`. `wrangler.jsonc` serves `./dist`.
Every push to the branch redeploys automatically.

**Pages (alternative):** Build command `node build.mjs`, output directory `dist`.

Security headers and redirects live in `src/static/_headers` and `src/static/_redirects`, which
are copied into `dist/` and applied by Cloudflare. After the first deploy, set `site.url` in
`site.config.mjs` to the live address (or custom domain) so canonicals, the sitemap and the form's
thank-you redirect are correct.

## Contact form (n8n)

The meeting form posts to an **n8n Webhook**, and the n8n workflow routes each submission
(email, sheet, CRM) and redirects the visitor to `/thank-you/`. Put the webhook's production URL
in `form.webhookUrl` in `site.config.mjs`. Until then the form shows a "not connected yet" notice
and won't send. Setup steps: `docs/N8N-FORM-SETUP.md`.

## Office

**835 Wilshire Blvd, Los Angeles, CA 90017** (storefront office). Phone: **(424) 901-0458**.

## Structure

The homepage (`/`) holds every section, each reachable from the menu and the sticky section bar:
Services · How it works · Who does what · 401(k) basics · FAQ · About · Visit & contact (meeting form).
`/privacy-policy/`, `/terms/` and `/disclosures/` are separate pages under California law,
plus `/thank-you/` and `404.html`.

## Design

- **Palette:** chaparral green `#2E3A2F`, poppy orange `#BF4A14` (buttons, white text), golden hour `#F2A541`, sand `#F7D9B0`, hill green `#5E7340`, cream `#FBF7F0`
- **Type:** Andada Pro (display) and Readex Pro (text), both self-hosted
- **Logo:** a ringed round badge with a California poppy on rolling green hills (`src/brand.mjs`)
- **Hero:** slow-zoom photo of downtown Los Angeles below the snow-capped San Gabriel Mountains

See `docs/` for the launch checklist, media sources, Search Console and Google Business Profile steps.
