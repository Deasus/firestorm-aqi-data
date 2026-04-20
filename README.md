# FIRESTORM AQI Data

Global air quality data pipeline for the FIRESTORM wildfire intelligence platform.

## What This Does

Every 30 minutes, fetches PM2.5 readings across a global 2° grid (~5,400 points) from Open-Meteo's Air Quality API and outputs a compact JSON file.

## Output

`data/current-aqi.json` — Compact JSON with grid readings:

```json
{
  "updated": "2026-04-20T20:00:00Z",
  "resolution_deg": 2,
  "total_points": 5400,
  "stats": { "max_pm25": 245.3, "avg_pm25": 18.7, "unhealthy_points": 42 },
  "grid": [[lat, lng, pm25, aqi], ...]
}
```

## Usage in FIRESTORM

```javascript
fetch('https://raw.githubusercontent.com/Deasus/firestorm-aqi-data/main/data/current-aqi.json')
  .then(r => r.json())
  .then(data => {
    // data.grid = [[lat, lng, pm25, aqi], ...]
    // Render as haze overlay on map
  });
```

## Cost

$0. Open-Meteo is free with no API key. GitHub Actions uses ~60 min/month.

## Data Source

[Open-Meteo Air Quality API](https://open-meteo.com/en/docs/air-quality-api) — CAMS (Copernicus Atmosphere Monitoring Service) global air quality forecast data.
