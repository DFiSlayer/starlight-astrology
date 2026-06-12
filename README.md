# ✦ Starlight Astrology

**Version:** 1.0.0 RC1 — June 2026  
**Author:** Lorenzo Antonio Perez (DFiSlayer)  
**Live:** https://DFiSlayer.github.io/starlight-astrology  
**App ID:** com.starlightastrology.app

---

## What It Is

Starlight Astrology is a full-featured western astrology progressive web app (PWA) that runs entirely in a single HTML file with no server, no backend, no external dependencies beyond Google Fonts. Every calculation happens locally in the browser using Meeus astronomical algorithms. Your chart data never leaves your device.

---

## Features

### Western Astrology
- Natal chart wheel with Placidus house system
- Sun, Moon, Mercury, Venus, Mars, Jupiter, Saturn, Uranus, Neptune, Pluto
- North Node, South Node, Lilith (Mean), Chiron
- Ascendant, Midheaven, Descendant, Imum Coeli
- Tropical zodiac
- Day / Night chart detection (sect)
- Chart shape detection (Bundle, Stellium, Bowl, Bucket, Locomotive, See-Saw, Splash, Splay)

### Houses
- Full Placidus house calculation
- Validated against CafeAstrology to within 0.5° for all 12 cusps
- House rulers and occupants
- Expandable house cards with sign on cusp, ruler placement, and planetary interpretations
- Handles morning births (lower-hemisphere MC), high-latitude charts, southern hemisphere

### Planets & Points
- Essential dignities: Domicile, Exaltation, Detriment, Fall, Peregrine
- Dignity scores (+5 to -4)
- Retrograde detection with ℞ symbol
- Dispositor chain and Almuten
- Chart sect analysis

### Aspects
- Major: Conjunction, Opposition, Trine, Square, Sextile
- Minor: Quincunx, Semi-square, Sesquiquadrate
- Aspect grid with orb display
- Scrollable table with nature classification (Flowing, Challenging, Mixed)

### Lots & Arabic Parts
- Lot of Fortune (day/night formula)
- Lot of Spirit
- Lot of Manifestation
- Lot of Eros
- Lot of Necessity
- Lot of Courage
- Lot of Victory
- Lot of Nemesis
- Color-coded by planetary ruler

### Correspondences
- Four sub-tabs: Mythology, Tarot, Numerology, Material
- Covers all 12 signs across traditions

### BaZi — Four Pillars of Destiny
- Year, Month, Day, Hour pillars
- Heavenly Stems and Earthly Branches
- Hidden stems for each branch
- Day Master identification and strength
- Ten Gods / relationships (Proper Wealth, Indirect Wealth, etc.)
- Validated against traditional BaZi references

### Numerology
- Life Path number
- Expression (Destiny) number
- Soul Urge (Heart's Desire) number
- Master numbers 11, 22, 33 preserved

### Astrocartography
- 40 lines: MC, IC, AC, DC for all 10 planets
- Domain-based key lines: Wealth, Health, Love, Career, Growth, Challenge, Creativity, Spirituality
- Region descriptions for each line
- Interpretations for each planet/line type combination

### Synastry
- Cross-chart aspect comparison
- Supports any two saved charts

---

## Technical Details

### Architecture
- **Single file:** One HTML file contains all CSS, JavaScript, and markup — no build step, no bundler, no framework
- **No external APIs:** All ephemeris calculations run locally using Meeus Series algorithms
- **PWA:** Installable on Android and iOS via browser, works offline after first load
- **Storage:** localStorage with schema versioning (v3), export/import as JSON
- **Geocoding:** Nominatim (OpenStreetMap) for city-to-coordinates lookup

### Ephemeris Engine
- Planetary positions accurate to ±0.5° for inner planets
- Outer planets (Uranus, Neptune, Pluto) accurate to ±1° — Meeus algorithm ceiling
- Placidus house cusps validated to ±0.5° against Swiss Ephemeris references
- Handles dates from 1800 to 2099
- Historical timezone database included for accurate UTC conversion

### Validated Reference Charts
- **Lorenzo:** Dec 11 1982, 17:47, Los Angeles — Sun Sag 19°43', Moon Sco 12°41', ASC Can 5°26', MC Pis 17°59'
- **BaZi Lorenzo:** 壬戌 · 壬子 · 戊辰 · 辛酉 (Yang Earth Dragon Day Master)
- **Numerology Lorenzo:** Life Path 7, Expression 2, Soul Urge 4

### Test Coverage
213 automated checks across 25 test suites — 0 failures:
- Planet signs and longitudes (±0.5° tolerance)
- Angles and house cusps (12 Placidus cusps, 8 time/location combos)
- Data integrity and NaN prevention
- No-time handling (null ASC/MC/houses when birth time unknown)
- BaZi pillars verified for 4 reference charts
- Numerology with master number preservation
- Astrocartography: 40 lines, coordinate validity, known line positions
- Chart storage round-trip
- Export/Import with 5MB size guard
- Timezone edge cases: Newfoundland, Nepal, India, Adelaide
- Stress test: 100 charts in 43ms build / 55ms load / 1MB storage
- Abuse testing: corrupt JSON, emoji names, 500-char names, NaN coordinates, future/past dates, invalid times

---

## File Structure

```
starlight-release/
├── index.html                  The entire application (246KB)
├── README.md                   This file
└── icons/
    ├── starlight-icon.svg      Master icon — vector, scalable to any size
    ├── favicon.png             32×32 browser tab
    ├── icon-16x16.png          Favicon fallback
    ├── icon-32x32.png          Favicon standard
    ├── icon-48x48.png          Windows taskbar
    ├── icon-72x72.png          Android ldpi
    ├── icon-96x96.png          Android mdpi
    ├── icon-120x120.png        iOS (iPhone legacy)
    ├── icon-128x128.png        Chrome Web Store
    ├── icon-144x144.png        Windows tile / Android xhdpi
    ├── icon-152x152.png        iPad (legacy)
    ├── icon-167x167.png        iPad Pro
    ├── icon-180x180.png        iOS home screen (apple-touch-icon)
    ├── icon-192x192.png        Android home screen / PWA manifest
    ├── icon-256x256.png        High-DPI desktop
    └── icon-512x512.png        PWA splash screen / Google Play Store
```

---

## Deployment

### GitHub Pages (Web App)

1. Create a new public repository named `starlight-astrology` on GitHub
2. Click **uploading an existing file**
3. Drag `index.html` and the entire `icons/` folder into the upload area
4. Commit with message: `Starlight Astrology v1.0.0 RC1`
5. Go to **Settings → Pages → Source → Deploy from branch → main / root**
6. Click **Save**

Live in ~60 seconds at:
```
https://DFiSlayer.github.io/starlight-astrology
```

### PWA — Install on Android

1. Open the live URL in Chrome on Android
2. Tap the three-dot menu → **Add to Home Screen**
3. App installs with icon, runs fullscreen, works offline

### PWA — Install on iOS

1. Open the live URL in Safari on iPhone or iPad
2. Tap the **Share** button → **Add to Home Screen**
3. App installs with icon

### Android APK (Capacitor)

**Requirements:** Node.js 18+, Android Studio, Java 21+

```bash
npm install
npm run build
npx cap add android
npx cap sync android
npx cap open android
```

In Android Studio:
**Build → Build Bundle(s)/APK(s) → Build APK(s)**

The APK will be at:
`android/app/build/outputs/apk/debug/app-debug.apk`

**For a signed release APK (Google Play Store):**
**Build → Generate Signed Bundle/APK → APK → create keystore → release**

**App details:**
- App ID: `com.starlightastrology.app`
- Minimum SDK: Android 5.0 (API 21)
- Target SDK: Android 14 (API 34)

---

## How to Use

### Adding a Chart

1. Tap **+** (top bar on mobile, sidebar footer on desktop)
2. Fill in:
   - **Name** — person or event name
   - **Birth Date** — MM/DD/YYYY format
   - **Birth Time** — leave blank if unknown (ASC/MC/houses will be omitted)
   - **Birth City** — type to geocode automatically
3. Tap **Save Chart**

Chart calculates instantly. All tabs update automatically.

### Navigating Tabs

| Tab | Content |
|---|---|
| ⊙ Wheel | Natal chart wheel with planets, houses, aspect lines |
| ☿ Planets | Full planet table with signs, degrees, houses, dignity |
| ⌂ Houses | Placidus cusps with rulers and occupants |
| △ Aspects | All aspects with orb and nature |
| ♄ Dignities | Essential dignity table, sect, dispositor chain |
| ✦ Lots | Arabic parts with formulas and house placements |
| ⊕ Corr. | Correspondences — Mythology, Tarot, Numerology, Material |
| ☯ BaZi | Four Pillars with stems, branches, hidden stems, Ten Gods |
| 🌍 Astro | Astrocartography key lines by life domain |
| ♡ Synastry | Cross-chart aspect grid |

### Editing a Chart

Tap **✎** (pencil icon) → change any field → **Save Chart**

### Exporting / Backing Up

Desktop sidebar → **Export** → saves `starlight-charts.json`  
To restore: **Import** → select the JSON file

### Relocating a Chart

Edit modal → **Relocate** → enter a new city → saves as a separate relocated chart alongside the natal

---

## Known Limitations

- **Uranus longitude:** ±0.73° systematic error vs Swiss Ephemeris due to Meeus algorithm ceiling for outer planets. Within acceptable tolerance for natal interpretation.
- **House system:** Placidus only. Whole sign, Equal, Koch not implemented.
- **Outer planet dignities:** Uranus, Neptune, Pluto follow traditional rulers (Saturn, Jupiter, Mars). Modern rulerships not applied.
- **No predictive techniques:** Natal charts only. No progressions, solar returns, or transits.
- **Offline fonts:** Cinzel and Crimson Pro load from Google Fonts. App functions offline but falls back to system serif fonts.
- **localStorage limit:** ~5MB. Supports approximately 100 full natal charts before approaching browser storage limits. Use Export to back up and clear.

---

## Icon Design

The icon is a custom zodiac wheel built entirely in SVG:

- **12 segments** colored by element:
  - Fire (Aries, Leo, Sagittarius) — neon orange `#ff6030`
  - Earth (Taurus, Virgo, Capricorn) — neon gold `#ffd700`
  - Air (Gemini, Libra, Aquarius) — neon cyan `#00f5ff`
  - Water (Cancer, Scorpio, Pisces) — neon violet `#bf5fff`
- **Custom SVG sigils** for each sign — hand-drawn paths, no font rendering, no background bleed
- **Abbreviated sign names** in element color around the outer ring
- **Interconnected aspect lines** in the center:
  - Gold — Oppositions (180°)
  - Cyan — Grand Trine (120°)
  - Violet — Sextile Star hexagon (60°)
  - Rose — Quincunx lines (150°)
- **The Primal Star** at center — an 8-pointed star representing 8 divination traditions, built from two overlapping polygons with interconnected spoke lines in app colors
- **Background** — deep space radial gradient `#0e0a28` → `#04040f`

---

## Credits

Built over multiple sessions with Claude (Anthropic).  
Ephemeris algorithms based on Jean Meeus, *Astronomical Algorithms* (2nd ed.).  
Geocoding via Nominatim / OpenStreetMap contributors.

---

## License

Personal project — Lorenzo Antonio Perez © 2026.  
All rights reserved. Not for redistribution without permission.

---

*ST★RLIGHT ASTROLOGY — v1.0.0 RC1 — June 2026*
