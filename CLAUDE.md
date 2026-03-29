# Clientwork — Deployment Guide

## Owner
Doug Buckle (doug.buckle@gmail.com) — Head of Product / CPO type, not a developer. Keep things practical and non-technical.

## Hard Rules
- Never use emojis as icons. Always use Google Material Icons via `https://fonts.googleapis.com/icon?family=Material+Icons` with `<span class="material-icons">icon_name</span>` syntax.

## Stack
- **Source code**: This repo (`dougnose-pers/Clientwork`) at `/Users/douglasbuckle/Documents/Clientwork/`
- **Hosting**: Cloudflare Pages (auto-deploys on push to `main`)
- **Domain**: `dougbuckle.com` managed by Cloudflare (Doug.buckle@gmail.com account)
- **Pages URL**: `clientwork.pages.dev`
- **Custom domains**: `clienthark.dougbuckle.com`, `clientwork.dougbuckle.com`

## Cloudflare API Access
- API token stored in `.env` file in this repo (gitignored)
- Load with: `source .env`
- Account ID: `6233d1df23c32252da00b1bed71cb08e`
- Pages project name: `clientwork`

### Useful API commands
```bash
# Verify token
curl -s -X GET "https://api.cloudflare.com/client/v4/user/tokens/verify" -H "Authorization: Bearer $CLOUDFLARE_API_TOKEN"

# List Pages projects
curl -s -X GET "https://api.cloudflare.com/client/v4/accounts/6233d1df23c32252da00b1bed71cb08e/pages/projects" -H "Authorization: Bearer $CLOUDFLARE_API_TOKEN"

# Add custom subdomain (replace SUBDOMAIN)
curl -s -X POST "https://api.cloudflare.com/client/v4/accounts/6233d1df23c32252da00b1bed71cb08e/pages/projects/clientwork/domains" -H "Authorization: Bearer $CLOUDFLARE_API_TOKEN" -H "Content-Type: application/json" --data '{"name":"SUBDOMAIN.dougbuckle.com"}'
```

## Deployment Workflow
1. Edit/add HTML files in this repo
2. `git add . && git commit -m "description" && git push`
3. Cloudflare auto-deploys within ~30 seconds
4. Site is live at custom domains

## Current Pages
- `/sasha-kb/` — SASHA Platform Migration Knowledge Base (password protected: HARKMEDICAL01)

## Password Protection Pattern
Pages can be password-gated using client-side JS. The pattern used:
- SHA-256 hash of password stored in page
- Content base64-encoded in the HTML
- Login screen styled to match Hark branding
- On correct password, content is decoded and rendered

## Adobe Portfolio
`dougbuckle.com` (root domain) still points to Doug's Adobe Portfolio site. DO NOT change the root domain DNS records. Only add subdomains.

## Other Repos
- `dougbuckle-site` — personal site at `dougbuckle-site.pages.dev` (separate Pages project)
