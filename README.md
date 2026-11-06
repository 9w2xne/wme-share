# WME Smart Search

WME Smart Search is a userscript for the Waze Map Editor (WME) that enhances the default search box.

By default, the WME search box only handles plain text searches. This script watches what you paste or type into it and, when it recognises coordinates, a Plus Code or a map link, it centers the map there and drops a red marker on the spot. Anything it doesn't recognise goes to the normal WME search as usual.

## Features

- **Coordinate formats:** decimal (`1.3521, 103.8198`), hemisphere letters (`N 1.3521, E 103.8198`) and DMS (`1°21'07.6"N 103°49'11.3"E`). Decimal commas (`1,3521; 103,8198`) and `O` for West are also accepted.
- **Plus Codes:** full codes (`6PH57VP3+PR`) are decoded locally. Short codes (`57VP3+PR`) are resolved relative to the current map center.
- **Short link resolution:** follows `maps.app.goo.gl`, `goo.gl`, `g.co` and `maps.apple` short links to find the coordinates.
- **Map URL support:** extracts coordinates from Google Maps, Apple Maps, OpenStreetMap, Bing, Yandex and HERE links, `geo:` URIs, and any link carrying `ll=`, `q=`, `lat`/`lon` style parameters (this includes Waze Live Map and WME permalinks). A link buried in other pasted text is found too.
- **Ambiguous coordinate swapping:** if you enter two numbers without hemisphere letters or signs (e.g. `1.23, 4.56`), press `Shift+Enter` to read them as `lon, lat` instead of `lat, lon`.
- **Leaves normal searches alone:** only the WME search box is hooked. Text with spaces and no digits is ignored, and anything that isn't recognised falls through to the regular WME search.

## Installation

1. Install a userscript manager for your browser:
   - [Tampermonkey](https://www.tampermonkey.net/) (Chrome, Edge, Firefox, Safari)
   - [Violentmonkey](https://violentmonkey.github.io/) (Chrome, Edge, Firefox)

   *Recent versions of Chrome and Edge may require you to enable user scripts for the extension (the "Allow User Scripts" toggle, or Developer mode) before scripts will run. Your userscript manager's page explains this.*
2. **[Click here to install WME Smart Search](https://raw.githubusercontent.com/9w2xne/wme-share/main/wme-smart-search.user.js)**
3. Your userscript manager will prompt you to install the script. Click **Install**.
4. Reload WME. The browser console will show `[WSS] ready` once the script has loaded.

The script runs on `waze.com/editor` and `beta.waze.com/editor`. Greasemonkey is not supported.

## Usage

No buttons or menus are added. The script works inside the existing search box.

**Paste and go**
Paste any supported format or map URL into the search box. The map moves immediately and a red marker is dropped.

**Type and press Enter**
Type your coordinates and press `Enter`.

**Swapping latitude and longitude**
Without N/S/E/W letters or minus signs the script assumes `lat, lon`. If the map lands in the wrong place, type the pair into the search box again and press `Shift+Enter` to use the `lon, lat` reading. Note that pasting jumps immediately, so for an ambiguous pair, typing it (or adding hemisphere letters) is the way to use this.

The marker stays on the map until your next jump replaces it, or until you reload WME.

### Supported input examples

- `1.3521, 103.8198`
- `N 1.3521, E 103.8198`
- `1°21'07.6"N 103°49'11.3"E`
- `6PH57VP3+PR` (Plus Code)
- `https://maps.app.goo.gl/...`
- `https://www.google.com/maps/@1.3521,103.8198,17z`
- `geo:1.3521,103.8198?z=17`

Zoom is taken from the link when it has one, and kept between levels 12 and 22.

## Privacy

Everything is parsed locally in your browser. The only network requests the script makes are to open short links (Google or Apple), and those are sent without your cookies. Your userscript manager may ask you to allow these cross-domain requests the first time; choose "Always allow" for the listed domains.

## Known limitations

- Decimal coordinates need a decimal point (`1.35, 103.82`). Whole numbers like `1, 103` are not recognised.
- Failures are only reported in the browser console (look for lines starting with `[WSS]`), not on screen.
- Only the first supported link or token in the pasted text is used.

## Transparency & Development

I am not a professional software developer. This script was built as a personal project to solve a specific workflow issue in the Waze Map Editor.

The initial code structure, parsing logic and debugging were heavily assisted by Artificial Intelligence (AI). I have tested the script to ensure it works as intended, but please be aware that it was created through a collaborative human-AI effort. Contributions, bug reports and improvements from the community are welcome. Please use the [issue tracker](https://github.com/9w2xne/wme-share/issues).

## Author

**9w2xne**
- GitHub: [@9w2xne](https://github.com/9w2xne)

## License

This project is licensed under the MIT License.
