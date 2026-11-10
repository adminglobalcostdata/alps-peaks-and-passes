# Peaks, Passes & Viewpoints: DE AT CH FR (OSM+IGN)

[![Apify Actor](https://img.shields.io/badge/Apify-Actor-1f6feb)](https://apify.com/phonic_lily/alps-peaks-and-passes) ![Licence](https://img.shields.io/badge/licence-ODbL_1.0_-blue) ![Records](https://img.shields.io/badge/records-115%2C707-green)

Search about 115,000 summits, mountain passes and viewpoints in Germany, Austria, Switzerland and France from OpenStreetMap, with elevation, prominence, local relief, isolation and IGN altitude. Embedded data, no scraping, pay per record.

## What you get
- **115,707 records**, each carrying its own `license` and `attribution` fields, ready to republish with the required credit.
- A **100-record free sample** in this repository: [`sample.jsonl`](sample.jsonl) and [`sample.csv`](sample.csv) (opens as a table on GitHub).
- The **full dataset** as a filterable API (JSON, CSV, Excel), no scraping, no login: [Peaks, Passes & Viewpoints: DE AT CH FR (OSM+IGN) on Apify](https://apify.com/phonic_lily/alps-peaks-and-passes).

## One record
```json
{
  "id": "n26862792",
  "kind": "peak",
  "name": "Doldenhorn",
  "lat": 46.46856,
  "lon": 7.73496,
  "country": "CH",
  "elevation_m": 3638,
  "ign_elevation_m": null,
  "prominence_m": null,
  "local_relief_m": null,
  "isolation_km": null,
  "isolation_ref": null
}
```

## Quick start
Python:
```python
from apify_client import ApifyClient
client = ApifyClient('<YOUR_APIFY_TOKEN>')
run = client.actor('phonic_lily/alps-peaks-and-passes').call(run_input={'maxResults': 10})
for item in client.dataset(run['defaultDatasetId']).iterate_items():
    print(item)
```
Or from the command line:
```bash
curl -X POST 'https://api.apify.com/v2/acts/phonic_lily~alps-peaks-and-passes/run-sync-get-dataset-items?token=<YOUR_APIFY_TOKEN>' \
  -H 'Content-Type: application/json' -d '{"maxResults": 10}'
```
Pricing is pay-per-record on Apify (see the Actor page); the sample here is free.

## Fields
| Field | Description |
|---|---|
| `id` | OpenStreetMap element id (n=node, w=way, r=relation) or slug; unique within kind. |
| `kind` | peak, col (mountain pass) or viewpoint. |
| `name` | Name as tagged in OpenStreetMap. |
| `lat` | Latitude, decimal degrees. |
| `lon` | Longitude, decimal degrees. |
| `country` | ISO country code when the source gives it (DE, AT, CH, BE); null for records from the French source sites, which carry no country field. |
| `elevation_m` | Elevation in metres as tagged in OSM, null if untagged. |
| `ign_elevation_m` | Elevation from IGN RGE ALTI (Licence Ouverte 2.0), France only. |
| `prominence_m` | Topographic prominence in metres (OSM tag, rarely filled). |
| `local_relief_m` | Local relief within about 2 km in metres (computed by atlas-montagne from a DEM). |
| `isolation_km` | Distance to the nearest higher point in km (computed by atlas-montagne). |
| `isolation_ref` | Name of that nearest higher point. |
| `aspect` | Slope aspect (French cardinal name). |
| `slope_deg` | Local slope in degrees (computed from a DEM). |
| `direction` | Viewing direction tag (viewpoints) or road direction tag (passes). |
| `massif` | Massif tag when present. |
| `wikidata` | Wikidata QID. |
| `wikipedia` | Wikipedia article tag (lang:title). |
| `alt_name` | Alternative name. |
| `old_name` | Former name. |
| `commons` | Wikimedia Commons reference. |
| `sota_ref` | Summits On The Air reference. |
| `sota_points` | Summits On The Air points. |
| `summit_cross` | Summit cross tag. |
| `summit_register` | Summit register tag. |
| `sports` | Sports tagged on the peak. |
| `rock` | Rock type tag. |
| `volcano_status` | Volcano status tag. |
| `is_tower` | Viewpoint is a tower. |
| `tower_type` | Tower type tag. |
| `height_m` | Tower height in metres (viewpoints). |
| `climbs` | Road-climb sides of a pass: list of {side, length_km, ascent_m, grad_avg, grad_max, category} (atlas-montagne). |
| `profile_m` | Local topographic section: 48 elevation samples in metres (atlas-montagne, from a DEM). |
| `source_sites` | Source site(s) of the record, joined with +. |

## Data, licence and attribution
Extracted from OpenStreetMap (Overpass), licence ODbL 1.0, (c) OpenStreetMap contributors. This dataset is a derived database (Derivative Database under the ODbL): if you publish it or a database derived from it, you must credit OpenStreetMap and share it under ODbL 1.0. Personal data (phone numbers, e-mail addresses, operator names, memorial inscriptions) were removed. Null means the source gives no value; it is never 0. Coverage depends on the source sites: alpen-atlas = Germany, Austria, Switzerland; atlas-montagne and resurgence-atlas = France (including overseas), resurgence-atlas also a Belgium/Switzerland extension. Where the same OSM element appears in two source sites, fields are merged (first non-null wins, alpen-atlas first) and source_sites lists both. ign_elevation_m comes from IGN RGE ALTI (Licence Ouverte 2.0, attribution IGN). local_relief_m, isolation_km, aspect, slope_deg and profile_m were computed by atlas-montagne from a DEM.

**Licence:** ODbL 1.0 ; (c) OpenStreetMap contributors

**Attribution:** Contains data from OpenStreetMap, (c) OpenStreetMap contributors, ODbL 1.0 (https://www.openstreetmap.org/copyright). This dataset is a derived database and must be shared under ODbL 1.0 when redistributed. French elevations: IGN RGE ALTI, Licence Ouverte 2.0.

Share-alike: this sample is a derivative database. It stays under the licence above (ODbL 1.0 ; (c) OpenStreetMap contributors); any adapted copy must keep the same terms and credit the source.

Snapshot date: 2026-11. Empty values are `null`, never 0.

## Cite this dataset
GitHub's *Cite this repository* button reads [`CITATION.cff`](CITATION.cff).

## Related
Rankings of French mountain peaks, passes, climbing and via ferrata routes are browsable on [Arete Atlas (arete-atlas.com)](https://arete-atlas.com/).

## Feedback
Found an error or want a field added? Open an issue in this repository.
