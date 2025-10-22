# Bunge Global Shares Outstanding — Viewer

This repository contains a single-page viewer (index.html) that fetches the SEC XBRL JSON for EntityCommonStockSharesOutstanding and extracts the maximum and minimum common shares outstanding for fiscal years after 2020.

Files included in this submission:
- index.html — interactive page that fetches the SEC data, computes min/max, and exposes a downloadable `data.json`.
- uid.txt — included in the repository as provided.

Quick start (open locally)
1. Open `index.html` in a modern browser (Chrome, Firefox, Edge).
2. On load the page will fetch the SEC endpoint for Bunge Global (CIK 0001144519) and display:
   - Entity name (in the page title and <h1 id="share-entity-name">)
   - Max/min share values and fiscal years in elements with IDs:
     - share-max-value, share-max-fy, share-min-value, share-min-fy
3. A `Download data.json` button lets you save the computed JSON:
   {"entityName": "...", "max": {"val": ..., "fy": "..."}, "min": {"val": ..., "fy": "..."}}

Using alternate CIKs
- To load another company, open the page with a 10-digit CIK query parameter:
  index.html?CIK=0001018724
- For alternate CIKs the page will fetch via a public proxy to avoid CORS issues and update the title/H1 and all required IDs dynamically without a full-page reload.

Notes and behavior
- The page will attempt to fetch the SEC endpoint:
  https://data.sec.gov/api/xbrl/companyconcept/CIK0001144519/dei/EntityCommonStockSharesOutstanding.json
  and will log useful diagnostics to the console (which URL used, keys found, ignored entries).
- If required data or DOM elements are missing, the page displays a visible error box and logs details to the console.
- The code attempts to follow SEC guidance by adding a descriptive User-Agent header; due to browser restrictions this header cannot always be set from client-side JavaScript — the page handles such failures gracefully.

License
- This project is available under the MIT License. See LICENSE in the repository for full text.
