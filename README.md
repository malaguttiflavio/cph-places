# CPH Places

Personal map of places to visit in Copenhagen (and beyond) — bars, bakeries, jazz, wine, museums, day trips.

A single-page web app, no build step, no backend:

- **[index.html](index.html)** — the app (Leaflet map, list, filters, "Tonight" random picker).
  The five chip rows — type, area, status, occasion, time — each take any number of picks: choices
  within a row are OR'd, and the rows narrow each other (cafés *or* bakeries, in Nørrebro).
  The first chip in a row ("All", "All areas", …) clears that row.
- **Routes**: `ROUTES` at the bottom of `places.js` — rides and walks, each with a `pts` polyline
  and `stops` (place ids). The **🧭 Routes** tab lists them; tapping one draws it on the map, fits the
  view and fades the pins that aren't on it. Distance is computed from `pts`, never hand-written, and
  labelled "as drawn" because the line is a hand-traced corridor rather than a street-level route.
- **Opening hours**: `hours` on a place uses [OSM `opening_hours`](https://wiki.openstreetmap.org/wiki/Key:opening_hours)
  syntax (`Tu-Su 07:30-17:00; Mo off`), with `hoursSrc`/`hoursChk` recording where it came from and when.
  **[hours.csv](hours.csv)** is the editable source — fill a row there and re-merge. Always evaluated in
  `Europe/Copenhagen`, never device time, so "open now" is right while planning from another timezone.
  Places with no hours are shown as unknown and never guessed open; the counts line says how many.
  "🕐 Open now" filters to known-open, "⏰ Plan a time" scrubs to any day and hour.
- **[places.js](places.js)** — the data: one entry per place (imported from a Google Maps saved list)
- Your personal state (to try ❔ / been 👍👎 / favorite 🎈, notes, category edits, added/deleted places) lives in the browser's localStorage.
  On the map each place is its category's emoji; the ring around it is the status.
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

Categories (a place can have several): `cafe, bakery, bar, wine, jazz, club, restaurant, street, dessert, date, museum, sight, stage, shop, books, grocery, work, trip, spirit, parents, other`.
`date`, `work`, `parents` and `trip` say who or what a place is for rather than what it is, so they get
their own "occasion" chip row instead of appearing in the type row — pick one from each row to combine them.
Category, neighbourhood and name edits made in the app are stored as per-place overrides in localStorage
(tap a place's name in its detail sheet to rename it).
