# 02 — Environmental Sensor Quality Monitoring and Anomaly Detection

Source: Auckland region ground-gauge network (rainfall, river discharge, river water level), 2015-2026, hourly resolution, from Auckland Council's Environment Auckland open-data portal. Ground-observation data only.

## Project objective

Environmental monitoring networks routinely contain missing values, faulty readings, duplicated records, and unrealistic spikes, all of which degrade reporting quality and downstream decisions. "Done" looks like an anomaly-detection model plus a dashboard that labels readings as normal, suspicious, missing, or requiring review.

## Files

- `gauge_data/rainfall/<station_id>.csv` — 113 rainfall stations, hourly total rainfall (mm).
- `gauge_data/river_discharge/<station_id>.csv` — 53 stations, hourly discharge (m3/s). Source dataset is labelled `River Discharge.Continuous` by the portal — a continuous hourly reading, not an explicit maximum-of-interval aggregation.
- `gauge_data/river_water_level/<station_id>.csv` — 55 stations, hourly water level (m). Source dataset is labelled `River Water Level.Continuous` by the portal, same caveat as above.
- `station_inventory.csv` — one row per file above: station id, name, river catchment, coordinates, parameter, unit, span/coverage, gap notes, source.

## Format notes

- Each CSV is exactly as exported from the source portal — only the original `.zip` wrapper has been removed.
- Timestamps are NZST (UTC+12), no daylight-saving shift.
- Every station/parameter combination has its own dedicated file — no merging across stations has been done.

## What you'll need to figure out

This is real, unfiltered agency-exported data: expect missing periods, stations with little or no data, and possible inconsistencies between stations. `station_inventory.csv`'s `gap_notes_or_coverage` column is a starting point, not a full audit — identifying, categorising, and flagging data-quality problems (missing, suspicious, duplicate, out-of-range) is the project itself.
