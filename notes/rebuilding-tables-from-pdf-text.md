# Rebuilding Tables From PDF Text

A PDF has no tables. It has pieces of text at x/y positions, and any ruling lines
are just drawings. So "PDF → Excel" is really: guess the grid from where the text
sits. This is the approach in my [tools](https://chalidade.github.io/tools/#/pdf-to-excel)
PDF → Excel converter, all in the browser with pdf.js and ExcelJS.

## Rows: shared baselines

pdf.js gives text items with a transform. Items whose baselines match (within a
fraction of the font size) form one line. Inside a line, a gap wider than about
0.6× the font size starts a new **segment** — a candidate cell. Smaller gaps are
word spaces pdf.js left out, so they get a space re-inserted.

## Table blocks: runs of multi-segment lines

A line with 2+ segments is "tabular". Consecutive tabular lines form a block. A
one- or two-line run of single-segment lines tightly sandwiched between tabular
lines is pulled into the block too — that's a row with one filled cell, or a cell
whose text wrapped onto a second line.

## Columns: gutters nobody crosses

For each block, build a coverage array over the x-axis and count how many segments
cover each pixel column. Wherever coverage drops to (almost) zero for at least two
units, that's a gutter; its midpoint is a column boundary.

```ts
const tolerance = Math.floor(lines.length * 0.08) // a long note may span a gutter
if (coverage[i] <= tolerance) /* inside a gutter */
```

The 8% tolerance matters: one merged title cell or a long remark would otherwise
erase a real column.

## Numbers are the other half

A cell like `Rp15.500.000` should be the number 15500000 with format `"Rp"#,##0`,
not text. Two rules made this reliable:

- **Decimal separator by majority vote** across the whole document: count values
  that look like `1.234,56` versus `1,234.56`, and use the winner everywhere.
  Indonesian and English invoices are both common.
- **Leading zero = identifier.** `0812…` is a phone or account number; keep it text.
  Also handled: currency prefixes, `%`, and negatives written as `(1.000)`.

## Gotchas

- A table header repeated on every page is detected by comparing row keys and kept
  once when merging pages into one sheet.
- Scanned PDFs have no text layer at all — the honest answer is an error message
  that says OCR is needed, not an empty spreadsheet.
