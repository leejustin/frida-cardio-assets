# Frida Cardio street tiles

Walkable-street map tiles used by the Frida Cardio app to plan running
routes that draw shapes. Each tile is a zoom-13 Web Mercator square (about
4 km across at Bay Area latitudes), stored as gzipped JSON. The app downloads
the few tiles around the runner, caches them, and plans routes on the phone.

Tiles are published as **GitHub release assets** (free static hosting, no
server). A release holds one region: `manifest.json` plus `13-<x>-<y>.json.gz`
files. The app reads them from
`https://github.com/leejustin/frida-cardio/releases/download/<tag>/`.

## Licence

Map data © OpenStreetMap contributors, available under the
[Open Database License (ODbL)](https://www.openstreetmap.org/copyright).
These tiles are a derived database and are offered under the same licence.

## Build a region

Needs Node 20+ and osmium-tool (`brew install osmium-tool`). From the app
repository:

```sh
curl -L -o .tiles-cache/norcal-latest.osm.pbf \
  https://download.geofabrik.de/north-america/us/california/norcal-latest.osm.pbf
node --max-old-space-size=8192 tools/tiles/build-tiles.cjs \
  --pbf .tiles-cache/norcal-latest.osm.pbf \
  --bbox -122.75,37.15,-121.55,38.35 --name bay-area
```

This writes `tiles-out/bay-area/`. The Bay Area is 858 tiles, 38 MB.

## Publish

```sh
gh release create tiles-bay-area-YYYY-MM tiles-out/bay-area/* \
  --repo leejustin/frida-cardio --target tiles \
  --title "Street tiles: Bay Area (YYYY-MM)" --notes "..."
```

Then set `TILE_SOURCES` in `src/map-data.ts` to the new tag. A release holds
at most ~1000 files; split larger areas into several regions/releases.

## Check routes on real streets

```sh
node tools/tiles/bench-routes.cjs --km 1.6,5,8,11 --svg /tmp/routes
```

Plans every shape from a few Bay Area start points and writes SVG drawings.
