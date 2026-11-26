# Burundi Map

Interactive map of Burundi's new administrative structure: 5 provinces, 42 communes, 451 zones and 3,044 collines and quartiers. The interface is available in English, French and Kirundi.

## Files

| File | Purpose |
|---|---|
| `burundi-geo.json` | Names, IDs, population and coordinates. The map is drawn from this file. |
| `index.html` | The map. |
| `i18n.js` | Interface text in the three languages. |

## Data format

The structure is nested: provinces, communes, zones, then `hills_neighborhoods`.

```json
{
  "id": "BH-C01-Z01-H01",
  "name": "Bisinde",
  "center": { "latitude": -3.501, "longitude": 30.1932 },
  "boundary": [[[[30.0, -3.0], [30.1, -3.0], [30.1, -3.1], [30.0, -3.0]]]]
}
```

The `boundary` in this example is shortened.

| Field | Meaning |
|---|---|
| `id` | Province code (BH, BJ, BR, BT, GT), then commune, zone and colline numbers. |
| `center` | A point inside the area, in WGS84 decimal degrees. |
| `boundary` | A list of polygons. Each polygon is a list of rings (outer ring first, then holes). Each point is `[longitude, latitude]`, as in GeoJSON `MultiPolygon` coordinates. |
| `stats` | Provinces only: counts and population `{value, year}`. |
| `unnamed_areas` | Some communes only: shapes without a named entry (protected areas and similar), drawn in grey. |

Boundaries are simplified for display. Do not use them for surveying or legal purposes.

## Run it

The page loads `burundi-geo.json` from the `main` branch of this repository. If that fails, it tries the copy in the same folder.

To preview locally:

```sh
python -m http.server 8000
```

Then open http://localhost:8000.

To publish with GitHub Pages: **Settings > Pages > Deploy from a branch > `main` / root**. The map will be at https://blixy4.github.io/burundi-map/.

If you rename the repository or the account, update `SOURCES` in `index.html`.

## Sources and licence

- Names and structure: based on [Ijwi-ry-Ikirundi-AI/burundi-geo-data](https://github.com/Ijwi-ry-Ikirundi-AI/burundi-geo-data), which states the data is open for personal, educational and commercial use. Corrections were made using the boundaries below.
- Boundaries and coordinates: [Burundi administrative boundaries (COD-AB), version v02, on HDX](https://data.humdata.org/dataset/cod-ab-bdi), source IGEBU and OCHA, under Creative Commons Attribution for Intergovernmental Organisations (CC BY-IGO). Simplified and rounded for this map.
- Population: 2024 census, province level.
