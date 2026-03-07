# Peak 10 Energy — Historical Strip Analysis Tool

> EIA NYMEX futures strip analysis dashboard for hedge timing and decision-making.
> Companion tool to the Peak 10 Hedge Compliance Dashboard.

---

## What This Does

Pulls live NYMEX WTI crude oil and Henry Hub natural gas futures data directly from the U.S. Energy Information Administration (EIA) API — back to January 2010 — and provides six analytical views:

| Tab | Purpose |
|-----|---------|
| **① Overview** | Full 15-year history of 12-month strip averages with current level marked |
| **② Time Machine** | Compare any historical date's forward curve against today; P&L since that hedge |
| **③ Percentile** | Where today's strip ranks vs 2010–present; distribution, box plots, era comparison |
| **④ Seasonality** | Which calendar months historically offer the richest hedge entry; 3-month drift |
| **⑤ Strip Decay** | How a target delivery year's strip has evolved over time; optimal entry window |
| **⑥ Scorecard** | Synthesized hedge signals with gate-style pass/fail vs historical benchmarks |

---

## Deployment (Netlify)

### One-time setup
1. Push this repo to GitHub
2. Log into [netlify.com](https://netlify.com)
3. **Add new site → Import from Git → GitHub → select this repo**
4. Build settings are auto-detected from `netlify.toml`:
   - **Publish directory:** `public`
   - **Build command:** *(none — pure static)*
5. Click **Deploy site**

### Auto-deploy
Every push to `main` triggers a redeploy automatically. No manual steps needed.

### Custom domain (optional)
In Netlify dashboard → **Domain settings → Add custom domain** (e.g. `strip.peak10energy.com`)

---

## EIA API Key

The API key is embedded in `public/index.html`. If you need to rotate it:

```html
<!-- public/index.html, line ~200 -->
const KEY = 'YOUR_NEW_KEY_HERE';
```

To get a new key: [https://www.eia.gov/opendata/](https://www.eia.gov/opendata/)

> **Note:** The EIA API is free with no rate limits for typical usage. The tool
> fetches 24 series on page load (~15–30 seconds on first visit; cached by browser thereafter).

---

## Why Netlify (not file://)

The EIA API requires requests from a real HTTP/HTTPS origin. Opening the HTML file
directly from your desktop (`file://`) causes CORS errors. Netlify's HTTPS domain
resolves this — no proxy needed.

---

## Repo Structure

```
peak10-strip-analysis/
├── netlify.toml          ← Netlify build & header config
├── README.md             ← This file
└── public/
    └── index.html        ← The entire app (self-contained, no build step)
```

---

## Related

- **Hedge Compliance Dashboard** — separate Netlify site / repo (GRC Holdings + Brown Pony I MTM, compliance, scorecard, CF@Risk)
- Both tools share the same visual language (IBM Plex Mono, dark navy theme, Peak 10 branding)
