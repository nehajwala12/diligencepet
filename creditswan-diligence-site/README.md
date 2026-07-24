# CreditSwan.AI — Fetch Pet Insurance Diligence Dashboard

Static, single-page interactive briefing. No build step, no dependencies to install.

## Deploy

1. Create a new **private** GitHub repository.
2. Upload every file in this folder, preserving the `vendor/` subfolder.
3. In Vercel: **Add New → Project → Import** the repo.
4. Leave all build settings at their defaults — Framework Preset: **Other**, no build command, no output directory. Vercel serves `index.html` from the root.
5. Deploy.

Deploys in well under a minute. The CLI equivalent, from this folder:

```bash
npx vercel        # preview
npx vercel --prod # production
```

## ⚠️ This is a confidential document on a public URL

A default Vercel deployment is **publicly reachable by anyone with the link**. The footer of this document says "confidential — not for external distribution," so before sharing the URL, do one of the following in **Project → Settings → Deployment Protection**:

- **Vercel Authentication** — restricts access to your Vercel team members (available on all plans for preview deployments; production requires Pro).
- **Password Protection** — a shared password on the deployment (Pro plan).
- **Trusted IPs** — allowlist by IP (Enterprise).

`robots.txt` and the `X-Robots-Tag` header block search-engine indexing, but **that is not access control** — it only asks crawlers not to list the page. Anyone with the URL can still read it.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The entire dashboard — markup, styles, chart logic |
| `vendor/chart.umd.min.js` | Chart.js 4.4.1, vendored locally so there is no CDN dependency and the CSP can stay strict |
| `vercel.json` | Security headers, `noindex`, cache policy |
| `robots.txt` | Crawler exclusion |
| `favicon.svg` | Swan mark |

## Updating the chart data

Chart series are **directional reconstructions** consistent with the figures cited in the prose, not the original tool exports. Every dataset lives in the `<script>` block at the bottom of `index.html`, grouped by tab under comment headers (`── Market ──`, `── Search ──`, and so on). Replace the arrays with your Semrush / SE Ranking exports before circulating for committee use, and update the caveat in the footer once you do.

## Branding

Colors are CSS custom properties in the `:root` block at the top of `index.html` — change them there and every chart follows, since the JavaScript reads the same hex values (declared at the top of the script block). The current palette is an interpretation, not extracted from creditswan.ai.

| Token | Value | Role |
| --- | --- | --- |
| `--ink` | `#0f1b2d` | Deep navy — headings, dark surfaces |
| `--gold` | `#2e7d8f` | Teal accent — rules, emphasis, primary series |
| `--gold-lt` | `#93bcc6` | Pale teal — secondary series |
| `--bg` | `#f6f4ef` | Warm paper background |
| `--card` / `--card2` | `#e9e4da` / `#fdfcf8` | Panel surfaces |
| `--red` / `--green` | `#b0413a` / `#3f6e4e` | Bear / bull, down / up |

The `--gold` token names are retained from the original stylesheet so existing selectors keep working; the values are teal.

## Print

`Ctrl/Cmd + P` expands all seven tabs onto separate pages and hides the tab navigation — use this to produce a PDF.
