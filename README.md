# WME Smart Search 🗺️

**WME Smart Search** is a lightweight userscript for the Waze Map Editor (WME) that supercharges the default search box. 

Instead of failing when you paste map links or specific coordinate formats, WME Smart Search intercepts your input and instantly jumps the map to the correct location, dropping a temporary pin so you know exactly where it went.

## ✨ Features

- **Multiple Coordinate Formats:** Supports standard decimal (`1.234, 5.678`), Hemisphere letters (`N 1.234 W 5.678`), and DMS (`1°14'02.4"N 5°40'40.8"W`).
- **Plus Codes:** Paste a Google Plus Code (e.g., `6PH57VP3+PR`) and it will decode it locally.
- **Auto-Follow Short Links:** Paste a `goo.gl/maps` or `maps.apple` short link, and the script will automatically follow it to find the hidden coordinates.
- **Multi-Platform URL Support:** Simply paste a link from Google Maps, Apple Maps, Waze, OpenStreetMap, Bing, Yandex, or HERE.
- **Ambiguous Coordinate Fix:** Typed `1.23, 4.56` but the map went to the wrong place? Just press **Shift+Enter** to swap the latitude and longitude and try again.

## 🚀 Installation

1. Install a userscript manager for your browser:
   - [Tampermonkey](https://www.tampermonkey.net/) (Chrome, Edge, Safari, Firefox)
   - [Violentmonkey](https://violentmonkey.github.io/) (Chrome, Edge, Firefox)
   - [Greasemonkey](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/) (Firefox)
2. **[Click here to install WME Smart Search](https://raw.githubusercontent.com/9w2xne/wme-share/main/wme-smart-search.user.js)** *(Update this link to match your exact GitHub branch and filename)*.
3. Your userscript manager will prompt you to install. Click **Install**.

## 🛠️ How to Use

There are no new buttons or menus to learn. Just use the standard Waze search box at the top of the screen.

**Method 1: Paste and Go**
Simply paste **any** supported format or map URL into the search box. The script will automatically parse it, move the map, and drop a red pin.

**Method 2: Type and Press Enter**
Type or paste your coordinates and press **Enter**.

**Method 3: The Swap Trick**
If you enter coordinates without N/S/E/W letters (like `1.234, 5.678`), the script has to guess which is Latitude and which is Longitude. 
If it guesses wrong, simply press **Shift+Enter** to swap them instantly.

### Supported Input Examples:
- `1.3521, 103.8198`
- `N 1.3521, E 103.8198`
- `1°21'07.6"N 103°49'11.3"E`
- `6PH57VP3+PR` (Plus Code)
- `https://maps.app.goo.gl/...`
- `https://www.google.com/maps/@1.3521,103.8198,17z`

## 👨‍💻 Author

**9w2xne**
- GitHub: [@9w2xne](https://github.com/9w2xne)

## 📄 License

This project is licensed under the MIT License.
