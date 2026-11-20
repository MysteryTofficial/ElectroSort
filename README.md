# ElectroSort

**Component label & sticker generator with readable QR codes and schematic symbols.**

Version **1.1.0** · Made by **MysteryT**

ElectroSort is a single-page web app for generating print-ready A4 PDF sheets of
component labels. Each sticker shows the part name, category, a simplified
schematic symbol, key specifications, and a QR code that opens the datasheet or
a relevant search page.

---

## Features

- **985 components** in an external `components.json` database
- **Custom sticker size** (default **62 × 86 mm**) with automatic A4 pagination
- **Crisp QR codes** rendered at high resolution and scaled to millimetres
- **31 original schematic symbol templates** (IEC/ANSI-style SVG)
- **No build step**: plain HTML, CSS and JavaScript
- **Privacy-friendly**: no accounts, analytics, cookies or tracking; custom parts
  stay in your browser's `localStorage`
- **PDF export** with each label captured individually and placed at exact
  millimetre coordinates

---

## Run it

The app fetches `components.json`, so browsers will block it when you open the
file directly via `file://`. Serve the folder over HTTP:

```bash
cd ElectroSort
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

If you do open `index.html` directly, use the **Load components.json Manually**
button in the warning banner that appears.

---

## Project files

| File | Purpose |
|---|---|
| `index.html` | Entire application (UI, logic, PDF export) |
| `components.json` | Component database: 985 entries with specs, schematic SVG and link |
| `favicon.svg` | App icon |
| `LICENSE` | MIT license for the original code and symbols |
| `THIRD_PARTY_NOTICES.md` | CDN library licenses, datasheet and trademark notices |
| `.gitignore` | Ignores editor/OS files and local backups |

`components2.json`, `components3.json`, `components4.json` and
`components.json.bak` are leftover/working datasets and are **not** used by the app.

---

## Component data format

`components.json` is a JSON array. Each entry looks like:

```json
{
  "id": "ne555p",
  "name": "NE555P",
  "category": "IC",
  "package": "DIP-8",
  "symbol": "ic",
  "specs": "Supply: 4.5-16V\nOutput: 200mA\nFreq: up to 500kHz",
  "schematic": "<svg viewBox=\"0 0 60 40\" ...>...</svg>",
  "url": "https://www.ti.com/lit/ds/symlink/ne555.pdf"
}
```

Notes:

- Every entry has a non-empty `url`. Manufacturer/direct PDF links are used
  where available; otherwise the link points to a relevant datasheet-search or
  product-search page.
- Entries named `XX` are **generic templates** (for example "Resistor XX
  (SMD 0603)"). They link to a part-type search, not to a specific datasheet.
  Replace `XX` with your actual value when labelling parts.
- Every entry has a self-contained SVG `schematic`, so no external symbol files
  are needed. The `symbol` field groups parts that share a symbol template.

---

## Legal & licensing

- Original code and original schematic symbols: **MIT** — see `LICENSE`.
- Third-party libraries, datasheet links and trademarks: see
  `THIRD_PARTY_NOTICES.md` and the in-app **Legal Notice, Privacy & Licenses**
  dialog.
- Specifications are simplified/typical values. Always verify against the
  official datasheet before using a part in a real design.
- No datasheet PDFs, manufacturer images, logos or trademarks are bundled.

---

## Credits

Created by **MysteryT**. Symbol style references generic IEC/ANSI conventions;
the drawings themselves were made for this project.
