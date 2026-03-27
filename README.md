# Eastern Mediterranean Warship Tracker — March 2026

**OSINT maritime intelligence: NATO and allied warships deployed around Cyprus during the Iran-Israel-US conflict.**

🔗 **[Live Interactive Map](https://yourusername.github.io/eastern-med-warship-tracker/index.html)** ← *Update this URL after enabling GitHub Pages*

![Status](https://img.shields.io/badge/status-active_monitoring-brightgreen)
![Data](https://img.shields.io/badge/data-AIS_%2B_OSINT_fusion-blue)
![Last Updated](https://img.shields.io/badge/last_updated-27_Mar_2026-orange)

---

## Context

On **28 February 2026**, military conflict escalated between Iran, Israel, and the United States. Following drone strikes on Cyprus (including near RAF Akrotiri), multiple European nations deployed naval assets to defend the island and provide air/missile defence coverage across the Eastern Mediterranean.

This repository tracks those deployments using **AIS vessel data** fused with **open-source intelligence** (OSINT) from defence publications, government announcements, and military aviation/naval tracking communities.

---

## Warship Deployment Table

### Confirmed deployed — March 2026

| Vessel | Hull # | Flag | Class | MMSI | IMO | AIS Status | Last AIS Position |
|--------|--------|------|-------|------|-----|------------|-------------------|
| **FS Languedoc** | D653 | 🇫🇷 France | Aquitaine (FREMM ASW) | `227999300` | 0 | ⚠️ Stale (Oct 2025) | 43.04°N, 5.96°E (Toulon) |
| **Charles de Gaulle** | R91 | 🇫🇷 France | Nuclear CVN | `228711555` | 1112234 | ⚠️ Stale (Aug 2018!) | 43.11°N, 5.90°E (Toulon) |
| **SPS Cristóbal Colón** | F-105 | 🇪🇸 Spain | Álvaro de Bazán (Aegis) | `225920870` | 0 | 🔴 Dark | — |
| **ITS Federico Martinengo** | F596 | 🇮🇹 Italy | Bergamini (FREMM GP) | ❓ Unknown | 4714049 | 🔴 Dark | — |
| **HNLMS Evertsen** | F805 | 🇳🇱 Netherlands | De Zeven Provinciën LCF | `244942000` | 4601022 | 🟢 **Live** | 35.50°N, 24.19°E (off Crete) |
| **FGS Nordrhein-Westfalen** | F223 | 🇩🇪 Germany | Baden-Württemberg | `211921000` | 0 | 🔴 Dark | — |
| **HMS Dragon** | D35 | 🇬🇧 UK | Type 45 Daring | `235053408` | 4907866 | 🔴 Dark | — |
| **USS Gerald R. Ford** | CVN-78 | 🇺🇸 USA | Ford-class CVN | `338803000` | 0 | ⚠️ Stale (Feb 2026) | 33.65°N, 12.00°W (off Morocco) |
| **USS Oscar Austin** | DDG-79 | 🇺🇸 USA | Arleigh Burke IIA | `338847000` | 0 | 🟢 **Live** | 35.51°N, 24.23°E (off Crete) |
| **HS Psara** | F-454 | 🇬🇷 Greece | Hydra (MEKO 200HN) | ❓ Unknown | 0 | 🔴 Dark | — |
| **HS Kimon** | F-601 | 🇬🇷 Greece | Kimon (Belharra/FDI) | `237780180` | — | 🔴 Dark | — |

### Not deployed (included in some infographics but NOT near Cyprus)

| Vessel | Hull # | Flag | MMSI | Last AIS | Note |
|--------|--------|------|------|----------|------|
| **HNLMS De Zeven Provinciën** | F802 | 🇳🇱 Netherlands | `244911000` | 59.25°N, 19.73°E (Baltic, Nov 2025) | Same class as Evertsen — likely confused in infographics |

---

## MMSI Watchlist

Comma-separated for API queries (VesselFinder, AISStream.io, Datalastic):

```
227999300,228711555,225920870,244942000,211921000,235053408,338803000,338847000,237780180
```

### Cyprus Bounding Box

| Parameter | Tight box | Wide discovery box |
|-----------|-----------|-------------------|
| Format | `LAT_MIN,LON_MIN,LAT_MAX,LON_MAX` | — |
| Values | `34.0,32.0,36.0,35.5` | `33.5,31.0,36.5,36.5` |

---

## Key OSINT Findings

### 1. MMSI misattribution: Martinengo ≠ 247364500

**MMSI `247364500`** is registered to **ITS Luigi Rizzo (F595)**, not Federico Martinengo (F596).

- DataDocked API returned AIS name `NAVE LUIGI RIZZO` for this MMSI
- Confirmed by MarineTraffic, ShipSpotting (IMO 4568933 = Luigi Rizzo), MarinevesselTraffic
- Federico Martinengo's actual IMO is **4714049** (ShipSpotting)
- Martinengo's MMSI remains unknown — the ship is AIS-dark
- Italian Navy may rotate MMSIs between sister ships, or the API returned stale data from Rizzo's last broadcast on that transponder

### 2. Only 2 of 12 ships broadcasting AIS

| AIS Status | Count | Ships |
|------------|-------|-------|
| 🟢 Live | 2 | Evertsen, Oscar Austin |
| ⚠️ Stale | 4 | Languedoc, CdG, Ford, De Zeven Provinciën |
| 🔴 Dark | 6 | Kimon, Psara, Cristóbal Colón, Martinengo, Dragon, NRW |

Both live ships are **off Crete** (near NSA Souda Bay), not directly off Cyprus. Every ship reported operating around Cyprus itself is AIS-dark — standard wartime OPSEC.

### 3. Greek Navy OPSEC

The Hellenic Navy systematically withholds MMSI numbers from public AIS databases. Both Psara and Kimon show `MMSI: —` on MarinevesselTraffic and similar trackers. Kimon's MMSI (`237780180`) was found via VesselFinder direct lookup — a rare catch for a newly commissioned vessel.

### 4. Layered defence architecture

Greek deployment around Cyprus uses complementary capabilities:
- **HS Kimon (FDI)**: Sea Fire AESA radar + Aster 30 → high-altitude BMD
- **HS Psara (MEKO 200)**: Centaur/Kentavros EW system → low-altitude drone jamming at cost of electricity, not missiles

This solves the cost asymmetry problem: expensive interceptors reserved for ballistic threats, cheap EW used against drone swarms.

### 5. De Zeven Provinciën (F802) confusion

Multiple infographics show HNLMS De Zeven Provinciën near Cyprus. AIS data shows F802 in the **Baltic Sea** (Nov 2025). The ship actually deployed is her sister **HNLMS Evertsen (F805)** — same class, different hull.

### 6. Ford CSG position assessment

USS Gerald R. Ford's last AIS position (off Morocco, Feb 18, heading NE at 18.2 kn) is over 5 weeks stale. Based on itamilradar reporting of Ford CSG combat operations in the E. Med and P-8A surveillance flights near Crete coinciding with Ford's presence, the carrier is almost certainly now operating south of Cyprus.

---

## Hellenic Navy Frigate Fleet Reference

### Hydra-class (MEKO 200HN) — 4 ships

| Ship | Hull | Commissioned | MMSI | Note |
|------|------|-------------|------|------|
| HS Hydra | F-452 | 1992 | — | Active |
| HS Spetsai | F-453 | 1996 | — | Active |
| HS Psara | F-454 | 1998 | — | Deployed Cyprus (rotating out) |
| HS Salamis | F-455 | 1998 | — | Active |

### Elli-class (ex-Kortenaer) — 7 ships

| Ship | Hull | Origin | MMSI | Note |
|------|------|--------|------|------|
| HS Elli | F-450 | ex-Pieter Florisz | — | Expected to replace Kimon/Psara at Cyprus |
| HS Limnos | F-451 | ex-Witte de With | — | Active |
| HS Adrias | F-459 | ex-Callenburgh | — | Active |
| HS Aigaion | F-460 | ex-Banckert | — | Active |
| HS Navarinon | F-461 | ex-Van Kinsbergen | — | Active |
| HS Kountouriotis | F-462 | ex-Kortenaer | — | Active |
| HS Bouboulina | F-463 | ex-Philips van Almonde | — | Active |

### Kimon-class (Belharra/FDI) — 1 active, 2 building

| Ship | Hull | Status | MMSI |
|------|------|--------|------|
| HS Kimon | F-601 | Active (Cyprus) | `237780180` |
| HS Nearchos | F-602 | Building | — |
| HS Formion | F-603 | Building | — |
| HS Themistokles | F-604? | Ordered | — |

---

## Data Sources

| Source | Type | URL |
|--------|------|-----|
| VesselFinder | AIS positions + MMSI lookup | [vesselfinder.com](https://www.vesselfinder.com) |
| DataDocked | Vessel Location API | [datadocked.com](https://datadocked.com) |
| itamilradar | Military aviation/naval OSINT | [itamilradar.com](https://www.itamilradar.com) |
| MarinevesselTraffic | NATO warship tracking | [marinevesseltraffic.com](https://www.marinevesseltraffic.com) |
| ShipSpotting | Vessel photo/IMO database | [shipspotting.com](https://www.shipspotting.com) |
| Global Fishing Watch | AIS + behavioural analytics API | [globalfishingwatch.org](https://globalfishingwatch.org/our-apis/) |
| AISStream.io | Free real-time AIS WebSocket | [aisstream.io](https://aisstream.io/) |
| Equasis | Vessel registration/inspection | [equasis.org](https://www.equasis.org/) |
| IMO GISIS | Official IMO ship records | [gisis.imo.org](https://gisis.imo.org/) |
| ITU MARS | MMSI/callsign registry | [itu.int/mars](https://www.itu.int/en/ITU-R/terrestrial/mars/Pages/default.aspx) |
| VLIZ MarineRegions | EEZ boundary WMS | [marineregions.org](https://marineregions.org) |

---

## Repository Structure

```
eastern-med-warship-tracker/
├── index.html          # Interactive Leaflet map (GitHub Pages entry point)
├── data/
│   └── warships.json   # Structured vessel data with AIS + OSINT
├── README.md           # This file
└── LICENSE
```

---

## How to Use

### View the map
Open `index.html` in any browser, or visit the GitHub Pages URL.

### Query AIS APIs
Use the MMSI watchlist with:
- **AISStream.io** (free WebSocket): filter by `FiltersShipMMSI`
- **VesselFinder API** (paid credits): query `api.vesselfinder.com/vessels?mmsi=...`
- **Datalastic** (paid, self-serve): REST API with JSON response
- **Global Fishing Watch** (free, non-commercial): Python client `gfw-api-python-client`

### Monitor with bounding box
Set up an AISStream.io WebSocket subscription with the Cyprus bounding box to detect new warships entering the area:

```javascript
const socket = new WebSocket("wss://stream.aisstream.io/v0/stream");
socket.onopen = function() {
  socket.send(JSON.stringify({
    Apikey: "<YOUR_KEY>",
    BoundingBoxes: [[[34.0, 32.0], [36.0, 35.5]]],
    FilterMessageTypes: ["PositionReport"]
  }));
};
socket.onmessage = function(event) {
  let msg = JSON.parse(event.data);
  console.log(msg);
};
```

---

## Disclaimer

This is an **open-source intelligence research project** for educational purposes. All data is derived from publicly available AIS broadcasts and open-source reporting. Warship positions marked as "AIS-dark" are approximate based on news reporting, not precise geolocation. Military vessel tracking has legitimate applications in journalism, academic research, and maritime domain awareness.

---

## License

MIT — see [LICENSE](LICENSE).
