# Fever in the Returned Traveller — Interactive Explorer

**Prototype v0.1 · reviewed Oct 2026 · owner: Infection Services**
An aid to thinking, not a diagnostic rule. Corroborate with the departmental guideline, secondary sources, and current Health NZ / Public Health advice.

## Components

| File | What it is |
|------|------------|
| `fever_traveller_explorer.html` | The tool. A single self-contained HTML file — no server, no external files, no patient data. Open it in any modern browser (Chrome, Edge, Firefox, Safari). |
| `fever_traveller_data_master.csv` | The **single source of truth**. 31 infections × 20 regions plus incubation windows, route, syndrome, clue and first test. Edit here; the tool and the Word figure are both regenerated from it. |
| `fever_traveller_explorer_README.md` | This file. |

## How to test locally

1. Download `fever_traveller_explorer.html`.
2. Double-click it, or drag it into a browser tab. It runs immediately offline.
3. On a phone, open it the same way (it is responsive).

## What it does

- **Colour by** — Route of acquisition, Presenting syndrome, or Organism.
- **Region** — Pacific at country level, then broad regions. Absent infections grey out and drop to the bottom; uncommon ones get a hollow ring.
- **Days since leaving risk area** — Off by default; pick a band (≤7 / 8–14 / 15–21 / >21 d) to highlight compatible infections. Long-tail infections stay highlighted at later bands. Click Off (or Reset) to clear.
- **Click any infection** — opens a detail panel (incubation, clue, first test, regional grade).
- **Theme** — System / Light / Dark, remembered per browser.
- **"i" button** — version/owner, data-source note, and "Report an error" (opens the Microsoft Form).
- **Print / export…** — content (as-shown / full), colour (full / greyscale), range column (show / hide), and paper (A4 or A5, portrait or landscape). Print/PDF via the browser; Download PNG saves a 2× image.

## Editing the data

Open the CSV. Grades are `c` (common), `u` (uncommon) or `absent`. Incubation columns are in days.
Send the edited CSV back and the tool + static Word figure are regenerated from it — they cannot drift apart.

## Known limitations / to confirm

- Regional grades (~250 cells) are a **starting point for departmental sign-off**, not validated data.
- "Report an error" is a link to the Microsoft Form, not a pre-filled submission.
- Hosting: this is one static file. It can go on GitHub Pages, an intranet web page, or a Teams website tab. SharePoint document libraries tend to download `.html` rather than display it.
