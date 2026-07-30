# CPH Places

Personal map of places to visit in Copenhagen (and beyond) — bars, bakeries, jazz, wine, museums, day trips.

A single-page web app, no build step, no backend:

- **[index.html](index.html)** — the app (Leaflet map, list, filters, "Tonight" random picker)
- **[places.js](places.js)** — the data: one entry per place (imported from a Google Maps saved list)
- Your personal state (want to go / been / favorite + notes) lives in the browser's localStorage.
  Use **Tonight → Export my data** to back it up, **Import** to restore.

## Run locally

```bash
python3 -m http.server 8000
```

then open http://localhost:8000.

## On iPhone

Open the hosted URL in Safari → Share → **Add to Home Screen**. Runs fullscreen like an app.

## Adding places

Edit `places.js` — each entry:

```js
{ id: "p106", name: "…", cat: "wine", area: "Nørrebro", address: "…", lat: 55.68, lng: 12.55, rating: 4.5, price: "100–200 kr", note: "…" }
```

Categories: `cafe, bakery, bar, wine, jazz, club, restaurant, street, museum, sight, stage, shop, trip, other`.
