# reports_site

Hub for small personal static reports, hosted at `reports.buffingchi.com` behind
Cloudflare Access (Google/email login — private, not public).

Each report is a self-contained static HTML export from its own source project —
this repo never runs any code, never touches a database, and has no upload/write
path of its own. It only ever receives a finished `index.html` from wherever the
report is actually generated (e.g. `scripts/house_2026_races`), committed and
pushed here, which triggers a Render Static Site redeploy.

## Structure

```
site/
  index.html              # landing page listing every published report
  house-2026-races/
    index.html             # published from scripts/house_2026_races/data/report.html
```

## Adding a new report

1. Add a new subfolder under `site/<project-name>/` with its `index.html`.
2. Add a card to `site/index.html` linking to it.
3. Commit and push — Render redeploys automatically.

## Deploy

Render Blueprint (`render.yaml`) — a Static Site, no build step, serves `site/`
directly. Custom domain `reports.buffingchi.com` is proxied through Cloudflare
with a Cloudflare Access policy restricting access to a single allowed email.
