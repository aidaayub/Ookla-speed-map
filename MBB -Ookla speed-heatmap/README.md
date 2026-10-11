# Malaysia Mobile Broadband Download Speed Map

Interactive static map built from the supplied `Download Speed.xlsx` and four administrative-boundary TopoJSON files. Covers **2022 Q1 to 2026 Q2**, with State, District, Parliament and DUN selection, year/quarter filters, purple-to-blue choropleth, device counts, and CSV export.

## Run locally

Because the app fetches local JSON, do not double-click `index.html` using a `file://` URL. Instead, from the project folder run:

```bash
python -m http.server 8000
```

Open `http://localhost:8000` in a browser. An internet connection is needed for Leaflet, TopoJSON client and basemap tiles.

## Deploy to Vercel

Upload this folder to a GitHub repository, then in Vercel select **Add New > Project**, import the repository, select **Other** framework and deploy. No build command is needed; output directory is the project root.

## Data notes

- Values are taken from the provided Excel workbook. The map shows administrative-area aggregates, **not Ookla quadkey tiles**.
- All 16 states, 158 districts, 222 parliamentary constituencies and 587 DUN areas were matched to the supplied TopoJSON by names/codes.
- The DUN worksheet contains 555 speed cells stored as numeric text; they were parsed as numbers without changing their values.
- The displayed overall speed is device-weighted from supplied area speeds, for browsing only. It may not exactly match an independently calculated national Ookla statistic.
- Grey indicates missing speed data.
- The supplied administrative boundaries may be dated; review them before official publication.

## Updating data

This version contains preprocessed JSON files in `data/`. To update it, install `openpyxl` and run `python build_data.py "Download Speed.xlsx"` using the updated workbook. This regenerates the four `*-speed.json` files while keeping the existing boundary indices. For later years, update the year options in `index.html` as well.
