# UNOPOS Lead Filter

Internal tool for filtering Florida business filings (SUNBIZ) into restaurant leads for the South Florida and Jacksonville territories.

## What it does
- Accepts raw SUNBIZ `.txt` flat-file exports
- Filters by restaurant keywords (pizza, grill, café, etc.) and exclusion keywords (realty, salon, etc.)
- Filters by county: Broward, Palm Beach, Duval, Clay, St. Johns, Nassau, Baker
- Exports CSV by region (All / SoFla / JAX)

## Deployment (Vercel)
1. Push this repo to GitHub
2. Import in [vercel.com/new](https://vercel.com/new)
3. Framework preset: **Other** (no build step needed)
4. Click Deploy — done

Every push to `main` auto-redeploys.

## Local use
Just open `index.html` in any browser. No server required.

## Team usage
1. Download today's SUNBIZ filing file (format: `MMDDYYYYf.txt`)
2. Go to the Vercel URL
3. Drop the file, confirm counties, click **Run Filter**
4. Download the CSV for your region
