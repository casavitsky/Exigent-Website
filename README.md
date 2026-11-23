# ExigentHR website (Cloudflare build)

Static site, no build step. Pages live in `public/`. Config is `wrangler.jsonc`.

## Fill in before deploying
- Find and replace `[[INFO-EMAIL]]` (general contact address) and `[[RECRUITER-EMAIL]]` (recruiting contact) across `public/`.
- Paste the original text into the pages marked TODO (Payroll & Benefits, HR Services, Exigent Insurance, Privacy Policy), then remove `noindex` from the privacy page.
- Add the contact form embed (HubSpot or similar) and the 60-second video.

## Deploy to a temporary Cloudflare address (GoDaddy untouched)
1. Cloudflare dashboard > Workers & Pages > Create > Import a repository (GitHub), or run `npx wrangler deploy` from this folder.
2. You get a `*.workers.dev` URL. Review every page there. No DNS changes are needed.

## Cutover later
- Confirm email DNS records (MX, SPF, DKIM, autodiscover) stay as they are at GoDaddy.
- Change only the `@` and `www` records at GoDaddy to point at Cloudflare. Leave nameservers alone.
- `public/_redirects` already 301s the old `/payroll-&-benefits` URL.
