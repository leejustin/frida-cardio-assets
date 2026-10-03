# Frida Cardio street tiles

Walkable-street map tiles used by the Frida Cardio app to plan running
routes that draw shapes. Each tile is a zoom-13 Web Mercator square (about
4 km across), stored as gzipped JSON.

Tiles are published as **GitHub release assets** (free static hosting, no
server), one release per metro region, named `tiles-<region>-YYYY-MM`. A
release holds two files: `<region>.tiles`, all of the region's gzipped
tiles back to back, and `manifest.json`, which lists each tile's byte
offset and length. A phone fetches the region's manifest once (2–40 KB),
then reads only the tiles around the runner with HTTP range requests and
caches them, so it never downloads a whole region.

Files live under
`https://github.com/leejustin/frida-cardio-assets/releases/download/<tag>/`.

## Regions

- San Francisco Bay Area — `tiles-bay-area-YYYY-MM`
- Sacramento and Davis — `tiles-sacramento-YYYY-MM`
- Los Angeles and Orange County — `tiles-los-angeles-YYYY-MM`
- San Diego — `tiles-san-diego-YYYY-MM`
- Santa Barbara — `tiles-santa-barbara-YYYY-MM`
- New York City and nearby New Jersey — `tiles-new-york-YYYY-MM`
- Philadelphia — `tiles-philadelphia-YYYY-MM`
- Pittsburgh — `tiles-pittsburgh-YYYY-MM`
- Buffalo — `tiles-buffalo-YYYY-MM`
- Hartford — `tiles-hartford-YYYY-MM`
- Boston — `tiles-boston-YYYY-MM`
- Providence — `tiles-providence-YYYY-MM`
- Chicago — `tiles-chicago-YYYY-MM`
- St. Louis — `tiles-st-louis-YYYY-MM`
- Kansas City — `tiles-kansas-city-YYYY-MM`
- Washington, D.C. — `tiles-washington-dc-YYYY-MM`
- Baltimore — `tiles-baltimore-YYYY-MM`
- Richmond — `tiles-richmond-YYYY-MM`
- Seattle — `tiles-seattle-YYYY-MM`
- Tacoma — `tiles-tacoma-YYYY-MM`
- Portland, Oregon — `tiles-portland-YYYY-MM`
- Denver and Boulder — `tiles-denver-YYYY-MM`
- Colorado Springs — `tiles-colorado-springs-YYYY-MM`
- Austin — `tiles-austin-YYYY-MM`
- Dallas and Fort Worth — `tiles-dallas-YYYY-MM`
- Houston — `tiles-houston-YYYY-MM`
- San Antonio — `tiles-san-antonio-YYYY-MM`
- El Paso — `tiles-el-paso-YYYY-MM`
- Atlanta — `tiles-atlanta-YYYY-MM`
- Phoenix — `tiles-phoenix-YYYY-MM`
- Tucson — `tiles-tucson-YYYY-MM`
- Minneapolis and Saint Paul — `tiles-minneapolis-YYYY-MM`
- Miami and Fort Lauderdale — `tiles-miami-YYYY-MM`
- Orlando — `tiles-orlando-YYYY-MM`
- Tampa and St. Petersburg — `tiles-tampa-YYYY-MM`
- Jacksonville — `tiles-jacksonville-YYYY-MM`
- Las Vegas — `tiles-las-vegas-YYYY-MM`
- Reno — `tiles-reno-YYYY-MM`
- Salt Lake City — `tiles-salt-lake-city-YYYY-MM`
- Nashville — `tiles-nashville-YYYY-MM`
- Memphis — `tiles-memphis-YYYY-MM`
- Charlotte — `tiles-charlotte-YYYY-MM`
- Raleigh and Durham — `tiles-raleigh-durham-YYYY-MM`
- Charleston — `tiles-charleston-YYYY-MM`
- Columbus — `tiles-columbus-YYYY-MM`
- Cleveland — `tiles-cleveland-YYYY-MM`
- Cincinnati — `tiles-cincinnati-YYYY-MM`
- Louisville — `tiles-louisville-YYYY-MM`
- Indianapolis — `tiles-indianapolis-YYYY-MM`
- Detroit and Ann Arbor — `tiles-detroit-YYYY-MM`
- Grand Rapids — `tiles-grand-rapids-YYYY-MM`
- Milwaukee — `tiles-milwaukee-YYYY-MM`
- Madison — `tiles-madison-YYYY-MM`
- New Orleans — `tiles-new-orleans-YYYY-MM`
- Albuquerque — `tiles-albuquerque-YYYY-MM`
- Oklahoma City — `tiles-oklahoma-city-YYYY-MM`
- Omaha — `tiles-omaha-YYYY-MM`
- Des Moines — `tiles-des-moines-YYYY-MM`
- Birmingham — `tiles-birmingham-YYYY-MM`
- Boise — `tiles-boise-YYYY-MM`
- Honolulu — `tiles-honolulu-YYYY-MM`
- Anchorage — `tiles-anchorage-YYYY-MM`
- Toronto — `tiles-toronto-YYYY-MM`
- Ottawa — `tiles-ottawa-YYYY-MM`
- Montreal — `tiles-montreal-YYYY-MM`
- Vancouver — `tiles-vancouver-YYYY-MM`
- Calgary — `tiles-calgary-YYYY-MM`
- Mexico City — `tiles-mexico-city-YYYY-MM`
- London — `tiles-london-YYYY-MM`
- Dublin — `tiles-dublin-YYYY-MM`
- Paris — `tiles-paris-YYYY-MM`
- Berlin — `tiles-berlin-YYYY-MM`
- Amsterdam — `tiles-amsterdam-YYYY-MM`
- Madrid — `tiles-madrid-YYYY-MM`
- Barcelona — `tiles-barcelona-YYYY-MM`
- Tokyo — `tiles-tokyo-YYYY-MM`
- Sydney — `tiles-sydney-YYYY-MM`
- Melbourne — `tiles-melbourne-YYYY-MM`

## Licence

Map data © OpenStreetMap contributors, available under the
[Open Database License (ODbL)](https://www.openstreetmap.org/copyright).
These tiles are a derived database and are offered under the same licence.

## Building and publishing

The tools live in the app repository under `tools/tiles`: `regions.json`
lists each region's bounds and Geofabrik extracts, and
`publish-regions.cjs` builds and releases every region not yet published
for the month, paced so downloads and uploads don't burst.
