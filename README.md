# HR Monitor

A lightweight, zero-dependency Progressive Web App (PWA) for real-time heart rate monitoring over Web Bluetooth (BLE), zone tracking, workout history, and activity export.

## Features

- **Web Bluetooth (BLE) Support**: Connects directly to standard Bluetooth Heart Rate sensors (`heart_rate` service / `heart_rate_measurement` characteristic, supporting both 8-bit and 16-bit BPM values).
- **Demo Mode**: Simulates live heart rate readings once per second (`48%–98%` of `HR max`) so you can test all features without a sensor.
- **Heart Rate Card**: Four-quadrant live display showing **Current HR**, **% of HR max**, **Average HR**, and **Max HR**, with the card background dynamically colored by the active heart rate zone.
- **Stats & Zone Pie Chart**: Tracks elapsed workout time, calories burned (Keytel formula using sex, weight, age, and heart rate), sample count, and an SVG pie chart with legend showing time and percentage spent in each zone.
- **Live Heart Rate Chart**: HTML5 `<canvas>` chart plotting heart rate over workout duration across color-coded zone bands.
- **Customizable Profile & Zones**: Configure `HR max` (`100–240 BPM`), sex, weight (`30–250 kg`), age (`10–100`), and 5 heart rate zones in either `% HR max` or nominal `BPM` mode. Settings persist automatically in `localStorage`.
- **Workout Controls & History**: Choose the workout type (`Running`, `Walking`, `Cycling`, `Indoor cycling`, `Strength training`, `Cardio / Fitness`, `Hiking`, `Other`), then start, pause/resume, finish, and reset workouts. Completed workouts are saved in `localStorage` with their type badge and can be previewed or deleted at any time.
- **Activity Export**: Export any saved workout from history as **CSV**, **TCX** (Garmin Training Center XML v2 with mapped `Sport` attribute), or **GPX** (with `<type>` and `TrackPointExtension` heart rate data).
- **Bilingual UI (`PL` / `EN`)**: Switch between Polish and English directly from the header; the selected language is saved in `localStorage`.
- **PWA, Fullscreen & Wake Lock**: Installable via `manifest.json` and `sw.js` (network-first caching), with fullscreen workout view, Screen Wake Lock support, and responsive layouts for desktop, mobile portrait, and mobile landscape.

## Requirements

- **Web Bluetooth**: Requires a supported browser such as Chrome, Edge, or Opera.
- **Secure Context**: Web Bluetooth and Service Workers require **HTTPS** or **`localhost`** (do not open `index.html` via `file://`).

## Running Locally

Serve the repository folder with any static HTTP server and open `http://localhost:8080`:

```bash
# Python
python -m http.server 8080

# Node.js
npx serve .
```

## Project Structure

| File | Description |
| --- | --- |
| `index.html` | Single-file application containing the UI, responsive styles, i18n (`PL`/`EN`), BLE client, chart rendering, and exports |
| `manifest.json` | Web app manifest for PWA installation |
| `sw.js` | Service worker with network-first caching (`hr-monitor-v2`) |
| `icon.svg` | Application icon |

## Local Storage Keys

- `ble_hr_user_settings_v1` — language, `HR max`, profile attributes, zone mode, and zone thresholds
- `ble_hr_workout_history_v1` — saved workouts and recorded heart rate samples
