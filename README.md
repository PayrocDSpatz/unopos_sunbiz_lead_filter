# UNOPOS Lead Filter

Internal tool for filtering Florida business filings (SUNBIZ) into restaurant leads for the South Florida and Jacksonville territories, with AI-powered lead enrichment.

## What it does

**Step 1–3 (Filter)**
- Accepts raw SUNBIZ `.txt` flat-file exports
- Filters by restaurant keywords (pizza, grill, café, etc.) and exclusion keywords (realty, salon, etc.)
- Filters by county: Broward, Palm Beach, Duval, Clay, St. Johns, Nassau, Baker
- Exports CSV by region (All / SoFla / JAX)

**Step 4 (AI Enrichment — NEW)**
- Runs each lead through Claude AI with web search
- Finds phone number, website, confirms address, identifies business type (franchise vs. independent)
- Adds sales notes: owner name, new filing vs. DBA rebrand, first-mover flags
- Enriched columns added to the table live as each lead completes
- Download CSV includes enriched data when available

## Deployment (Vercel)

### First-time setup

1. Push this repo to GitHub
2. Import in [vercel.com/new](https://vercel.com/new)
3. Framework preset: **Other** (no build step needed)
4. Before deploying, add your Anthropic API key:
   - Go to **Settings → Environment Variables**
   - Add: `ANTHROPIC_API_KEY` = `sk-ant-...`
5. Click **Deploy** — done

Every push to `main` auto-redeploys.

### Adding the API key to an existing Vercel project

1. Go to your project in [vercel.com](https://vercel.com)
2. **Settings → Environment Variables**
3. Add variable:
   - Name: `ANTHROPIC_API_KEY`
   - Value: your key from [console.anthropic.com](https://console.anthropic.com)
   - Environment: Production ✓ (add Preview/Development if you want)
4. **Redeploy** the project (Settings → Deployments → Redeploy)

> The API key lives only in Vercel's environment — it is never in the repo or sent to the browser.

## Project structure

```
/
├── index.html        # Main app (runs in browser)
├── api/
│   └── enrich.js     # Vercel serverless function — proxies Anthropic API calls
├── vercel.json       # Vercel config
└── README.md
```

## Local development

For local testing of the enrichment feature, you need the Vercel CLI:

```bash
npm i -g vercel
vercel env pull .env.local   # pulls your env vars from Vercel
vercel dev                   # runs at localhost:3000
```

Without the CLI, the filter (Steps 1–3) works by just opening `index.html` in any browser. The enrichment step (Step 4) requires the serverless function and won't work from a plain file open.

## Team usage

1. Download today's SUNBIZ filing file (format: `MMDDYYYYf.txt`) from sftp.floridados.gov → Public → doc → fic
2. Go to the Vercel URL
3. Drop the file, confirm counties, click **Run Filter**
4. Optionally click **Enrich Leads with AI** — waits ~10–15 sec per lead
5. Download the CSV for your region (includes enriched data if step 4 was run)
