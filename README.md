# ExigentHR website (Cloudflare build)

Static site, no build step. Pages live in `public/`. Config is `wrangler.jsonc`.

## Fill in before deploying
- The logo, explainer video and video poster currently load from GoDaddy's image servers. Before cancelling GoDaddy, download them from the live site, add them to an `assets/` folder in `public/`, and update the three URLs.
- Find and replace `[[INFO-EMAIL]]` (general contact address) and `[[RECRUITER-EMAIL]]` (recruiting contact) across `public/`.
- The contact forms open the visitor's email app. To capture leads directly, swap them for a HubSpot form embed.

## Deploy to a temporary Cloudflare address (GoDaddy untouched)
1. Cloudflare dashboard > Workers & Pages > Create > Import a repository (GitHub), or run `npx wrangler deploy` from this folder.
2. You get a `*.workers.dev` URL. Review every page there. No DNS changes are needed.

## Cutover later
- Confirm email DNS records (MX, SPF, DKIM, autodiscover) stay as they are at GoDaddy.
- Change only the `@` and `www` records at GoDaddy to point at Cloudflare. Leave nameservers alone.
- `public/_redirects` already 301s the old `/payroll-&-benefits` URL.
