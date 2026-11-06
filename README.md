# WME Smart Search

WME Smart Search is a userscript designed for the Waze Map Editor (WME) that enhances the default search box. 

By default, the WME search box only handles basic text searches. This script intercepts user input to support a wide variety of map links, coordinate formats, and location codes. When a valid format is detected, the script centers the map on the location and drops a temporary marker to indicate the parsed destination.

## Features

- **Multiple Coordinate Formats:** Supports standard decimal (`1.234, 5.678`), Hemisphere letters (`N 1.234 W 5.678`), and DMS (`1°14'02.4"N 5°40'40.8"W`).
- **Plus Codes:** Paste a Google Plus Code (e.g., `6PH57VP3+PR`) and the script will decode it locally.
- **Short Link Resolution:** Automatically follows shortened URLs from Google Maps (`goo.gl`) and Apple Maps to find the hidden coordinates.
- **Multi-Platform URL Support:** Extracts coordinates from links pointing to Google Maps, Apple Maps, Waze, OpenStreetMap, Bing, Yandex, or HERE.
- **Ambiguous Coordinate Swapping:** If you input coordinates without cardinal directions (e.g., `1.23, 4.56`) and the map centers on the wrong spot, press `Shift+Enter` to swap the latitude and longitude.
- **Autofill Protection:** Built-in safeguards prevent the script from accidentally triggering on standard text inputs, usernames, or passwords.

## Installation

1. Install a userscript manager for your browser:
   - [Tampermonkey](https://www.tampermonkey.net/) (Chrome, Edge, Safari, Firefox)
   - [Violentmonkey](https://violentmonkey.github.io/) (Chrome, Edge, Firefox)
   - [Greasemonkey](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/) (Firefox)
2. **[Click here to install WME Smart Search](https://raw.githubusercontent.com/9w2xne/wme-share/main/wme-smart-search.user.js)** 
   *(Note: Ensure this URL matches your repository branch and file name)*.
3. Your userscript manager will prompt you to install the script. Click **Install**.

## Usage

The script integrates directly into the existing Waze search box. No additional buttons or menus are added.

**Method 1: Paste and Go**
Paste any supported format or map URL directly into the search box. The script will automatically parse the input, move the map, and drop a red marker.

**Method 2: Type and Press Enter**
Type or paste your coordinates and press `Enter`.

**Method 3: The Swap Trick**
If you enter coordinates without N/S/E/W letters, the script must guess the order. If it guesses incorrectly, simply press `Shift+Enter` to swap the latitude and longitude instantly.

### Supported Input Examples:
- `1.3521, 103.8198`
- `N 1.3521, E 103.8198`
- `1°21'07.6"N 103°49'11.3"E`
- `6PH57VP3+PR` (Plus Code)
- `https://maps.app.goo.gl/...`
- `https://www.google.com/maps/@1.3521,103.8198,17z`

## Transparency & Development

I am not a professional software developer. This script was built as a personal project to solve a specific workflow issue in the Waze Map Editor. 

To make this tool a reality, the initial code structure, parsing logic, and debugging were heavily assisted by Artificial Intelligence (AI). I have tested the script to ensure it works as intended, but please be aware that it was created through a collaborative human-AI effort. Contributions, bug reports, and improvements from the community are always welcome!

## Author

**9w2xne**
- GitHub: [@9w2xne](https://github.com/9w2xne)

## License

This project is licensed under the MIT License.
