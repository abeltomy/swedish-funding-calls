# Vinnova Open Funding Calls

A GitHub Pages website that tracks active funding calls from [Vinnova](https://www.vinnova.se/en/apply-for-funding/find-the-right-funding/) — updated daily via GitHub Actions.

## What it does

- **Daily at 06:00 UTC**, a GitHub Action fetches all calls for applications from Vinnova's public API
- It filters for open/active calls only and saves them to `data.json`
- The static `index.html` reads `data.json` and renders a searchable, filterable card grid
- Search by keyword, sort by deadline, filter by urgency (closing soon / rolling)

## Setup (5 minutes)

### 1. Create the repo

```bash
# Option A: Use this as a template on GitHub
# Option B: Push manually
git init
git add .
git commit -m "init"
git remote add origin https://github.com/YOUR_USERNAME/vinnova-funding.git
git push -u origin main
```

### 2. Enable GitHub Pages

1. Go to your repo → **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: `main` / root (`/`)
4. Click **Save**

Your site will be live at `https://YOUR_USERNAME.github.io/vinnova-funding/`

### 3. Run the Action for the first time

1. Go to **Actions** tab in your repo
2. Click **Fetch Vinnova Funding Data**
3. Click **Run workflow** → **Run workflow**

After ~30 seconds, `data.json` will be populated and the site will show live data.

After that, it runs automatically every day at 06:00 UTC. You can also trigger it manually anytime.

## File structure

```
├── index.html                        # The website
├── data.json                         # Auto-generated: open calls (committed by Action)
├── data_raw.json                     # Auto-generated: full raw API response
└── .github/
    └── workflows/
        └── fetch.yml                 # Daily scheduled Action
```

## API source

Data comes from Vinnova's open data API (no API key required, CC0 license):

- `https://data.vinnova.se/api/ansokningsomgangar/` — all calls for applications

Vinnova's full open data documentation: https://www.vinnova.se/en/about-us/about-the-website/open-data/

## Customisation

- **Change the schedule**: Edit the `cron` line in `.github/workflows/fetch.yml`
- **Show closed calls too**: Modify the filter logic in the Python script in `fetch.yml`
- **Add more fields**: Extend the `open_calls.append({...})` dict in the Python block
