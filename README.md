# CPH Places

Personal map of places to visit in Copenhagen (and beyond) — bars, bakeries, jazz, wine, museums, day trips.

A single-page web app, no build step, no backend:

- **[index.html](index.html)** — the app (Leaflet map, list, filters, "Tonight" random picker)
- **[places.js](places.js)** — the data: one entry per place (imported from a Google Maps saved list)
- Your personal state (want to go / been 👍👎 / favorite, notes, category edits, added/deleted places) lives in the browser's localStorage.
  Use **Tonight → Export my data** to back it up, **Import** to restore.
- **Device sync** (optional): Tonight → ☁️ Set up device sync. State syncs through the private repo
  `cph-places-data` (file `user-state.json`) using a fine-grained GitHub token scoped to only that repo
  (Contents: read/write). Pulls on open and on returning to the app; pushes ~1.5s after any change.

## Run locally

```bash
python3 -m http.server 8000
```

then open http://localhost:8000.

## On iPhone

Open the hosted URL in Safari → Share → **Add to Home Screen**. Runs fullscreen like an app.

## Adding places

Two ways:

1. **In the app**: tap **＋ Add place** — categories, address search (OpenStreetMap geocoder) or current location. Saved to the phone's localStorage and included in Export backups.
2. **In the data**: edit `places.js` — each entry:

```js
{ id: "p106", name: "…", cats: ["wine", "jazz"], area: "Nørrebro", address: "…", lat: 55.68, lng: 12.55, rating: 4.5, price: "100–200 kr", note: "…" }
```

Categories (a place can have several): `cafe, bakery, bar, wine, jazz, club, restaurant, street, dessert, date, museum, sight, stage, shop, books, grocery, work, trip, spirit, other`.
Category, neighbourhood and name edits made in the app are stored as per-place overrides in localStorage
(tap a place's name in its detail sheet to rename it).
