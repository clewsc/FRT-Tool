# Fever in the Returned Traveller — editing the data

The tool now loads its data from **`data.csv`** at runtime. To change the dataset:

1. Edit **`data.csv`** in Excel (or any spreadsheet / text editor).
2. Save it as CSV (UTF-8), keeping it next to `index.html` on the web host.
3. Refresh the page. No code change needed.

## Requirements

- **`index.html` and `data.csv` must be served together over http/https** (your intranet host, GitHub Pages, or a Teams site). Opening `index.html` by double-click (`file://`) will *not* read the CSV — the browser blocks it — and the tool will quietly fall back to a built-in copy of the data.
- **There is no built-in fallback.** If `data.csv` is missing, misnamed, or malformed, the tool shows a full-screen error explaining the likely cause (rather than silently showing stale data). This is deliberate: a load error means something is wrong with the upload/hosting and should be fixed.
- Opening `index.html` by double-click (`file://`) shows the "needs a web address" error, because browsers block file-to-file reads. Always test via the hosted http(s) address.

## Columns (first 14 are fixed, in this order)

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

## Region columns (everything after `first_test`)

- Each remaining column header is a **region name**; the cell value is the grade:
  - `c` = common, `u` = uncommon, blank/anything else = not reported there.
- **Add a region** by adding a new column with a header name and grades — it appears in the Region dropdown automatically.
- **Rename** a region by changing its header text.
- **Reorder** regions by moving columns (the "All regions" option is always first).

## Notes

- Keep the first 14 column headers exactly as above (the tool checks them).
- Values with commas (e.g. "Bacterial gastroenteritis (NTS, Campylobacter, Shigella)") must be quoted — Excel does this automatically on save.
- `index.html` no longer contains a copy of the data — `data.csv` is the single source of truth.
