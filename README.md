# Fever in the Returned Traveller — incubation and geographic explorer

**Prototype v0.2 · reviewed Oct 2026 · owner: Infection Services**

An aid to thinking. Incubation windows and regional grades are approximate and outliers occur — corroborate with the departmental guideline, secondary sources, and current Health NZ / Public Health advice.

---

## 1. For users

An interactive chart of incubation periods for infections that cause fever in the returned traveller. Each row is an infection; the bar shows its usual window (thick) and full reported range (thin), plotted on a log scale of days from exposure to first symptom. Filters let you narrow to a region or a time-since-exposure, and any row opens a detail panel.

### What it does

- **Colour by** — Route of acquisition, Presenting syndrome, or Organism.
- **Region** — "All regions" first, then the Pacific at country level and broader world regions. In a region view, infections not reported there grey out and drop to the bottom, and ones that are uncommon there get an **amber dot** beside their name.
- **Days since leaving risk area** — off by default; pick a band (≤7 / 8–14 / 15–21 / >21 d) to highlight compatible infections. Long-tail infections stay highlighted at later bands. Click **Off** (or **Reset**) to clear.
- **Click any infection** — opens a detail panel with the incubation window, a clinical clue, a suggested first test, and the regional grade.
- **Theme** — System / Light / Dark, remembered per browser.
- **"i" button** — version and owner, a data-source note, and **Report an error** (opens the Microsoft Form).
- **Print / export…** — choose content (as-shown / full), colour (full / greyscale), the range column (show / hide), paper orientation (A4 portrait or landscape), and a **Teaching mode**. Print/PDF goes through the browser; **Download PNG** saves a 2× image.
  - **Teaching mode** turns the figure into a worksheet: *Disease name* leaves the labels blank to fill in; *Incubation* leaves the plot blank to draw in. (To also hide the numeric ranges for a recall exercise, set the range column to *Hide* as well.)
  - **Safari / iOS** ignores the requested orientation and prints portrait by default — switch it manually in the print/export dialog. (Chrome, Edge and Firefox honour the orientation automatically.)

### Status and limitations

- Regional grades (37 infections × 22 regions) are a **starting point for departmental sign-off**, not validated data.
- "Report an error" is a link to the Microsoft Form, not a pre-filled submission.

---

## 2. Tool guide (hosting & deployment)

### Files

| File | What it is |
|------|------------|
| `index.html` | The tool — a single HTML file, no build step, no patient data. Runs in any modern browser (Chrome, Edge, Firefox, Safari). |
| `data.csv` | The **single source of truth** for the figure — infections, incubation windows, route/syndrome/organism, clues, first tests, and per-region grades. |
| `README.md` | This file. |

### Hosting — read this first

**`index.html` and `data.csv` must be served together over http/https** (an intranet page, GitHub Pages, or a SharePoint/Teams site page). The tool fetches `data.csv` at runtime, so the two files must sit in the **same folder**.

- **Do not open `index.html` by double-click (`file://`).** Browsers block file-to-file reads, so the CSV won't load and the tool shows a "needs a web address" error. Always test via the hosted http(s) address.
- **There is no built-in data fallback.** If `data.csv` is missing, misnamed, or malformed, the tool shows a full-screen error explaining the likely cause rather than silently rendering stale data. This is deliberate — a load error means something is wrong with the upload or hosting and should be fixed.

### How to test

1. Upload `index.html` and `data.csv` together to the host.
2. Open the tool's http(s) address (not the file path).
3. After editing the data, save the CSV in place and refresh the page — no code change needed.

### Hosting note

SharePoint **document libraries** tend to download `.html` rather than display it. Use a SharePoint/Teams **site page**, an intranet web page, or GitHub Pages instead.

---

## 3. Editing the data

The tool loads its data from **`data.csv`** at runtime, so the dataset changes without touching any code:

1. Edit **`data.csv`** in Excel (or any spreadsheet / text editor).
2. Save it as **CSV (UTF-8)**, keeping it next to `index.html` on the web host.
3. Refresh the page.

### Columns (the first 14 are fixed, in this order)

| column | meaning |
|---|---|
| `infection` | display name |
| `range_lo_d`, `range_hi_d` | full reported incubation range, in **days** |
| `usual_lo_d`, `usual_hi_d` | usual window (the thick bar), in **days** |
| `open_ended` | `1` if the range has a long tail (dotted), else `0` |
| `timing_text` | the text shown in the "Usual (range)" column |
| `pathogen` | `vir`, `bac`, `par`, or `fungal` |
| `route` | `mosq`, `arth`, `food`, `env`, `p2p` |
| `syndrome` | `sys`, `gi`, `resp`, `cns`, `vhf` |
| `core` | `1` = bold (core cause), else `0` |
| `rare` | `1` = hidden when "Show rare" is off, else `0` |
| `clue` | text in the detail panel |
| `first_test` | text in the detail panel |

### Region columns (everything after `first_test`)

- Each remaining column header is a **region name**; the cell value is the grade:
  - `c` = common, `u` = uncommon, `absent` or blank = not reported there.
- **Add a region** by adding a new column with a header name and grades — it appears in the Region dropdown automatically.
- **Rename** a region by changing its header text.
- **Reorder** regions by moving columns (the "All regions" option is always first).

The current dataset has **37 infections × 22 regions**.

### Notes

- Keep the first 14 column headers exactly as above — the tool checks them.
- Values containing commas (e.g. "Bacterial gastroenteritis (NTS, Campylobacter, Shigella)") must be quoted — Excel does this automatically on save.
- `index.html` contains **no copy of the data**; `data.csv` is the single source of truth, so the tool and its data cannot drift apart.
