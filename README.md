# Burundi Map

Interactive map of Burundi's new administrative structure: 5 provinces, 42 communes, 451 zones and 3,044 collines and quartiers. The interface is available in English, French and Kirundi.

## Files

| File | Purpose |
|---|---|
| `burundi-geo.json` | Names, IDs, population and coordinates. The map is drawn from this file. |
| `water.json` | Lakes and rivers. |
| `roads.json` | National roads (RN1 to RN22 and RN24). |
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

## Map layers

- **Lakes and rivers:** from OpenStreetMap, clipped to Burundi and simplified.
- **National roads:** OpenStreetMap ways tagged RN1 to RN24 (no RN23 was tagged). Lines may have gaps.

## Run it

The page loads each data file from the `main` branch of this repository. If that fails, it tries the copy in the same folder.

To preview locally:

```sh
python -m http.server 8000
```

Then open http://localhost:8000.

To publish with GitHub Pages: **Settings > Pages > Deploy from a branch > `main` / root**. The map will be at https://blixy4.github.io/burundi-map/.

If you rename the repository or the account, update `REPO` in `index.html`.

## Sources and licence

- Names and structure: based on [Ijwi-ry-Ikirundi-AI/burundi-geo-data](https://github.com/Ijwi-ry-Ikirundi-AI/burundi-geo-data), which states the data is open for personal, educational and commercial use. Corrections were made using the boundaries below.
- Boundaries and coordinates: [Burundi administrative boundaries (COD-AB), version v02, on HDX](https://data.humdata.org/dataset/cod-ab-bdi), source IGEBU and OCHA, under Creative Commons Attribution for Intergovernmental Organisations (CC BY-IGO). Simplified and rounded for this map.
- Population: 2024 census, province level.
- `water.json` and `roads.json`: © [OpenStreetMap contributors](https://www.openstreetmap.org/copyright), from Humanitarian OpenStreetMap Team exports and Overpass, under the [Open Database License (ODbL)](https://opendatacommons.org/licenses/odbl/). These two files remain under ODbL.
