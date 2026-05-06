# WellCorr Pro — Well Correlation & Geosteering Toolkit

> A browser-based, zero-dependency tool for well log correlation, formation top picking, and geosteering QC — deployed as a single HTML file on GitHub Pages.

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-00e0a0?style=flat-square&logo=github)](https://geoharkat.github.io/wellcorr-pro/)
[![License: MIT](https://img.shields.io/badge/License-MIT-f0a030?style=flat-square)](LICENSE)
[![No Dependencies](https://img.shields.io/badge/Dependencies-None-6ab0f0?style=flat-square)]()

---

## Overview

**WellCorr Pro** is a professional-grade well correlation and geosteering analysis tool that runs entirely in the browser. Load Gamma Ray logs from two wells (a **type well** and a **current well**), interactively pick formation tops and match pairs, apply depth corrections with per-segment vertical shift and stretch/squeeze, then validate the correlation quality — all without installing any software.

---

## Features

### Three Workflow Modes

| Mode | Description |
|---|---|
| **General** | Side-by-side split-track view for picking match pairs between the type and current well |
| **Detailed** | Overlay view for fine-tuning each depth segment's offset and scale |
| **Validation** | QC dashboard with correlation score, formation table, dip angles, and depth query |

### Data Import
- Accepts **CSV**, **TXT**, and **LAS** file formats
- Interactive column-mapping dialog — choose your depth and GR columns
- Configurable null value threshold (default `-999.25`)
- Optional smoothing applied at load time

### Correlation Engine
- **Match pair picker** — click a type-well peak, then a current-well peak to pair them
- **Auto-Match** — automatically detects and pairs GR peaks across both wells
- **Auto-Correlation** — generates a segmented depth model from your match pairs with per-segment linear depth transformation (offset + scale)
- **Segment editor** — add, delete, rename, and reorder depth segments; drag split points directly on the canvas

### Signal Smoothing
Three algorithms available per track:
- Triangular weighted average
- Simple moving average
- Savitzky-Golay (2nd order polynomial)

### Validation & QC
- **Correlation score** (0–100) based on windowed GR cross-correlation at each top
- **Formation table** — type/current depths, ΔMD, formation thickness, thickness ratio, and apparent dip angle
- **Depth query** — convert any type-well MD to current-well MD and vice versa
- **Well spacing** input for dip calculation

### Session & Export
- Session auto-saved to `localStorage` — resume your work after closing the browser
- Export correlation to **JSON** for reproducibility
- Import a previously saved JSON correlation

---

## Getting Started

### Run Locally

No build step needed. Just open the file:

```bash
git clone https://github.com/your-username/wellcorr-pro.git
cd wellcorr-pro
open correlation.html   # macOS
# or
xdg-open correlation.html   # Linux
# or double-click the file in Windows Explorer
```

### Deploy to GitHub Pages

1. Fork or push this repo to your GitHub account.
2. Go to **Settings → Pages**.
3. Set source to `main` branch, root (`/`) folder.
4. Your app will be live at `https://your-username.github.io/wellcorr-pro/`.

---

## Usage

### 1 — Load your well logs

Click **Load Type Well** or **Load Current Well** and select a CSV / LAS file. Map the depth and GR columns in the dialog that appears. Repeat for the second well.

### 2 — Pick match pairs (General mode)

Enable the **Picker** (or press `P`), click a characteristic GR peak on the type track, then click the corresponding peak on the current track. Repeat for 2–5 representative horizons. Click **Apply Auto-Correlation** to generate the depth model.

### 3 — Fine-tune (Detailed mode)

Switch to **Detailed** mode. Select a segment on the canvas and adjust its **Vertical Shift** (depth offset in metres) and **Stretch / Squeeze** ratio with the sliders. Click **Update Correlation** to preview the result. Add split points as needed.

### 4 — Validate (Validation mode)

Switch to **Validation** mode to inspect the correlation score, formation thicknesses, and depth differences. Enter the well spacing to compute apparent dip angles.

---

## Input File Format

WellCorr Pro reads any delimited text file with at least a depth column and a GR column. Example CSV:

```
DEPTH,GR,RHOB
100.0,45.2,2.31
100.5,48.7,2.29
101.0,52.1,2.27
...
```

LAS files are parsed the same way — select `DEPTH` (or `MD`) and your GR curve in the column mapper.

---

## Keyboard Shortcuts

| Key | Action |
|---|---|
| `P` | Toggle point picker |
| `F` | Fit view to full depth range |
| `V` | Cycle through modes (General → Detailed → Validation) |
| `Esc` | Cancel current action |
| `↑` / `↓` | Scroll depth |
| `Ctrl + Scroll` | Stretch / squeeze selected segment |
| `Shift + Drag` | Box zoom |

## Mouse Controls

| Action | Result |
|---|---|
| Left-click curve | Select segment / pick point |
| Left-drag on curve | Move segment vertically |
| Left-drag on empty area | Pan depth |
| Middle scroll | Zoom depth |
| Middle drag | Pan depth |
| Right-click | Context menu (add split, add top, flatten, zoom, reset, remove) |
| Double-click | Add formation top |

---

## Project Structure

```
wellcorr-pro/
└── correlation.html   # Entire application — self-contained, no build required
```

All rendering is done on an HTML5 `<canvas>` element. No frameworks, no bundler, no server required.

---

## Browser Support

Any modern browser with ES5 and Canvas 2D support:

- Chrome / Edge 90+
- Firefox 90+
- Safari 14+

---

## Roadmap

- [ ] Multi-well panel view (3+ wells)
- [ ] LAS 3.0 export
- [ ] Resistivity / RHOB track support
- [ ] Dip vector overlay
- [ ] PDF / PNG export of the correlation panel

---

## Author

**Ismail Harkat**
[geoharkat@gmail.com](mailto:geoharkat@gmail.com)

---

## License

MIT © Ismail Harkat
