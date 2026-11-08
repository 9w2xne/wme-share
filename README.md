# WME Smart Search

WME Smart Search is a userscript for the Waze Map Editor (WME). It adds a small one-line search bar that jumps the map to coordinates, Plus Codes and map links, including the share links produced by the Waze app. After each jump it drops a red marker and shows the exact coordinate, so you can compare it with Waze Live Map or Google Maps.

The bar is separate from the WME search box. WME's own search is not changed in any way.

## Features

- **Waze app share links:** paste a `waze.com/ul/h…` link and the script decodes the coordinate from it locally. No network request is made.
- **Coordinate formats:** decimal (`1.3521, 103.8198`), hemisphere letters (`N 1.3521, E 103.8198`) and DMS (`1°21'07.6"N 103°49'11.3"E`). Decimal commas (`1,3521; 103,8198`) and `O` for West are also accepted.
- **Plus Codes:** full codes (`6PH57VP3+PR`) are decoded locally. Short codes (`7VP3+PR`) are resolved relative to the current map center.
- **Map links:** Google Maps, Apple Maps, OpenStreetMap, Bing, Yandex, HERE, `geo:` URIs and Waze links that carry `ll=` or `lat`/`lon` (including Live Map and WME permalinks). A link buried in other pasted text is found too.
- **Short link resolution:** follows `maps.app.goo.gl`, `goo.gl`, `g.co` and `maps.apple` short links to find the coordinates.
- **Coordinate readout:** the result shows the source (for example "Waze share link") and the coordinate to 6 decimals, with **Copy**, **Waze** (Live Map) and **Google** (Google Maps) links.
- **Ambiguous pairs:** two numbers without hemisphere letters or signs (`1.23, 4.56`) are read as `lat, lon`. The **⇄** button, or `Shift+Enter`, reads them as `lon, lat` instead.
- **Clear errors:** anything it cannot read is shown in red in the bar (`Not recognised: …`), and failed short links report there too.

## Installation

1. Install a userscript manager for your browser:
   - [Tampermonkey](https://www.tampermonkey.net/) (Chrome, Edge, Firefox, Safari)
   - [Violentmonkey](https://violentmonkey.github.io/) (Chrome, Edge, Firefox)

   *Recent versions of Chrome and Edge may require you to enable user scripts for the extension (the "Allow User Scripts" toggle, or Developer mode) before any script will run. Your userscript manager's page explains this.*
2. **[Click here to install WME Smart Search](https://raw.githubusercontent.com/dinkaftac/wme-smart-search/main/wme-smart-search.user.js)**
3. Your userscript manager will prompt you to install the script. Click **Install**.
4. Reload WME. The bar appears near the top centre of the page.

The script runs on `waze.com/editor` and `beta.waze.com/editor`. Greasemonkey is not supported.

## Usage

The bar is one row:

```
📍  [ lat, lon • Plus Code • map link ]  [Go]  [⇄]  Waze share link: 3.158376, 101.711361  Copy  Waze  Google
```

**Paste and go**
Paste any supported format or map link into the bar. The map moves immediately and a red marker is dropped.

**Type and press Enter**
Type or edit your input and press `Enter` or click **Go**.

**Swapping latitude and longitude**
If you enter two numbers without N/S/E/W letters or signs, the script assumes `lat, lon`. If the map lands in the wrong place, press `Shift+Enter` or click **⇄** to use the `lon, lat` reading. Pasting jumps immediately, so for an ambiguous pair, paste it and then click **⇄** (the pasted text stays in the bar).

**Moving and collapsing the bar**
- Drag the 📍 at the left end of the bar to move it. You can also drag from any empty part of the bar.
- Click the 📍 without dragging to collapse the bar to just the pin. Click it again to open it.
- The position and the collapsed state are remembered between sessions (stored in your browser's `localStorage` for the Waze site, so clearing site data resets them).
- The bar cannot be dragged off the screen.

**The marker**
The red marker stays on the map until your next jump replaces it, or until you reload WME.

### Supported input examples

- `1.3521, 103.8198`
- `N 1.3521, E 103.8198`
- `1°21'07.6"N 103°49'11.3"E`
- `6PH57VP3+PR` (Plus Code)
- `https://waze.com/ul/hw283fqzyy` (Waze app share link)
- `https://maps.app.goo.gl/...`
- `https://www.google.com/maps/@1.3521,103.8198,17z`
- `geo:1.3521,103.8198?z=17`

A ready-made set of about 90 samples, with the coordinate each one should land on, is in [`wme-smart-search-test-samples.md`](wme-smart-search-test-samples.md).

Zoom is taken from the link when it has one and kept between levels 12 and 22. Waze share links and coordinates open at zoom 17 to 18.

## Waze share links and what the coordinate means

A Waze share link such as `waze.com/ul/hw283fqzyy` contains only a location, encoded as a geohash, and no place name or address. The script decodes that point (about 2 m accurate for a 10-character geohash).

That point is whatever location the Waze app had for the place when it was shared. If the place came from Google's data, the point is Google's pin for it, which can be a few metres or more away from the real entrance or from the Waze venue in WME. So treat the jump as a starting point and confirm it against the imagery and nearby venues.

The result line shows the source ("Waze share link"), and the **Waze** and **Google** links open the same point in Waze Live Map and Google Maps so you can compare the two sources.

Waze links that are **not** supported, because they carry no readable coordinate or use a different form: `ul?preview_venue_id=…` (a venue ID only), `live-map/directions?to=ll.…` and `waze://…`.

## Privacy

Everything is parsed locally in your browser. The only network requests the script makes are to open Google or Apple short links, and those are sent without your cookies. Your userscript manager may ask you to allow these cross-domain requests the first time; choose "Always allow" for the listed domains.

## Troubleshooting

- **No bar appears:** check that your userscript manager is enabled for the page (the icon should show the script running) and that Chrome's "Allow User Scripts" toggle is on. Open the browser console and filter by `WSS`. You should see `[WSS] SDK connected`, `[WSS] panel ready` and `[WSS] ready`.
- **Debug output:** run `localStorage.setItem('wss-debug','1')` in the console and reload. The script then logs what it recognised each time you press Enter or click **Go**. Run `localStorage.removeItem('wss-debug')` to turn it off.
- **The bar is in an awkward place:** drag it where you want it. To reset the position, run `localStorage.removeItem('wme-smart-search:bar-pos')` in the console and reload.
- **Using WME's own search box instead:** the script contains an optional hook for the WME search box, off by default. Set `HOOK_WME_BOX = true` in the script to turn it on. It can conflict with WME selecting its first suggestion on Enter, which is why the separate bar is the default.

## Known limitations

- Decimal coordinates need a decimal point (`1.35, 103.82`). Whole numbers like `1, 103` are not recognised.
- Waze's own `z=` zoom parameter uses a different scale from the map zoom, so it is read as a map zoom and clamped to 12 or more. Use the map to adjust.
- Short Plus Codes only work when the map is near the place, because they are relative to the map center.
- Short link failures show a message in the bar, but the cause (blocked request, expired link) is not distinguished.
- Only the first supported link or token in the pasted text is used.
- The place name and address are not read from any link; the script only moves the map.

## Transparency & Development

I am not a professional software developer. This script was built as a personal project to solve a specific workflow issue in the Waze Map Editor.

The initial code structure, parsing logic and debugging were heavily assisted by Artificial Intelligence (AI). I have tested the script to ensure it works as intended, but please be aware that it was created through a collaborative human-AI effort. Contributions, bug reports and improvements from the community are welcome. Please use the [issue tracker](https://github.com/dinkaftac/wme-smart-search/issues).

## Author

**dinkaftac**
- GitHub: [@dinkaftac](https://github.com/dinkaftac)

## License

This project is licensed under the MIT License.
