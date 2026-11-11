# Alpha Trophies: Victoria local pages

41 static pages for alphatrophies.com.au, one combined trophies, medals and awards page per location.

| Tier | URL pattern | Pages |
|---|---|---|
| State hub | `/trophies/victoria/` | 1 |
| Melbourne hub | `/trophies/victoria/melbourne/` | 1 |
| Melbourne suburbs | `/trophies/victoria/melbourne/<suburb>/` | 19 |
| Victorian towns | `/trophies/victoria/<town>/` | 20 |

NSW (57 pages) is live and lives in its own repo. Albury-Wodonga is built under NSW.

## Layout

```
trophies/victoria/     the pages (folders match the live URLs)
assets/                css, js, logo (product images load from the live site)
scripts/               build_vic.py, build_nav.py, scrape_vic_products.py, check_unique.py (+ build_nsw.py helpers it imports)
data/victoria/         vic_locations.json (copy, drive data), vic_products.json (live products), draft-backup/ (chrome source)
data/shared/           menu.json, sports.json
data/nsw/              nsw_locations.json (only needed because build_vic imports build_nsw)
docs/victoria/         VICTORIA-UNIQUENESS.md
sitemaps/              sitemap-victoria.xml
```

## Rebuild

```bash
python scripts/scrape_vic_products.py   # optional: refresh live products and prices
python scripts/build_vic.py             # writes the 41 pages and the sitemap
python scripts/build_nav.py             # Trophies/Medals menu
python scripts/check_unique.py          # uniqueness report
python -m http.server 8765              # preview at /trophies/victoria/
```

## Facts used
- Drive data: Google Maps, fastest route from Thomastown (11/8-20 Brock St, -37.68788, 145.0257629), 11 Nov 2026 about 4:30pm, so times are afternoon-traffic times.
- Delivery: standard $9.90 flat, express $25 flat, Fast Track 4 days ($40 + 10%, cap $300), Priority Rush 3 days ($50 + 15%, cap $300), pickup at Thomastown (standard 5 working days, Priority Rush pickup from day 3). No same-day pickup.
- Population and growth: ABS June 2025 via the Top towns and suburbs spreadsheet.

## Confirm with Tom before publishing
1. Local clubs and schools per location (only Reservoir Primary School is used).
2. The general-knowledge local facts, council areas and sport mix in `data/victoria/vic_locations.json`.
3. Re-run the scraper right before go-live to refresh prices and stock.
4. Go-live: 301 `/buy-trophies-in-melbourne` to `/trophies/victoria/melbourne/`, submit `sitemaps/sitemap-victoria.xml`, request indexing in Search Console.

## Deployment note
This repo contains build scripts, data and docs as well as the pages. Do not deploy the whole repository as a public site (the NSW repo's Pages workflow uploads `.`). If a Pages workflow is added, publish only `trophies/` and `assets/`.
