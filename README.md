# ESA Search

A lightweight web tool for searching Elastic Security Advisories (ESAs) by deployment version. Enter a target version (8.0.0 and above) and filter matching advisories by product, platform, and severity.

Data is sourced from the official [Elastic Security Announcements](https://discuss.elastic.co/c/announcements/security-announcements/31) forum and stored locally in `esas.json`.

## Features

- **Version search** — Find advisories affecting a specific stack version (e.g. `8.19.11`)
- **Dynamic filters** — Product, platform, and severity options are built automatically from `esas.json`
- **Select all / none** — Quick toggles for each filter category
- **Sort by severity** — Order results by CVSS score (highest first)
- **Direct links** — Each row links to the original ESA announcement on Discuss Elastic

## Project files

| File | Description |
|------|-------------|
| `index.html` | Single-page search UI (HTML + Tailwind CSS + vanilla JS) |
| `esas.json` | Crawled advisory database (8.x+ affected ranges) 

## Quick start

The page loads data via `fetch()`, so it must be served over HTTP — opening `index.html` directly as a file (`file://`) will not work.

```bash
cd ESA_search
python3 -m http.server 8765
```

Open [http://localhost:8765/index.html](http://localhost:8765/index.html), enter a version, and click **Search**.


## JSON record format

Each entry in `esas.json` looks like:

```json
{
  "esa_id": "ESA-2026-13",
  "title": "Improper Input Validation in Kibana Leading to Denial of Service",
  "url": "https://discuss.elastic.co/t/...",
  "affected_product": "Kibana",
  "affected_range": ">=8.4.0 <=8.19.11",
  "fixed_version": "8.19.12, 9.2.6, 9.3.1",
  "severity": "Medium (6.5)",
  "platforms": ["Elastic Cloud"]
}
```

An advisory with multiple affected version ranges or products may appear as more than one row.

## Requirements

- **Browser** — Any modern browser for the UI

## License

Private/internal use. Elastic Security Advisories are published by Elastic; refer to each linked announcement for official guidance.
