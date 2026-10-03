# Tools: File Converters That Never Leave the Browser

Moved my little file tools out of the weeknoo workspace into their own repo and
shipped six converters in one evening: https://chalidade.github.io/tools/

Every file is processed on the visitor's device — nothing is uploaded, nothing is
stored. Each tool lives in `src/tools/<slug>/`, registers itself in one
`registry.ts`, and loads its heavy library with a dynamic `import()` only when opened.

- **Word → PDF** (docx-preview + jsPDF). First bug: CVs built as one big layout
  table got sliced through the middle of a text line at the page break, because I
  only cut at paragraph/row starts. Now the cut lands between two real text lines,
  and Word margins repeat on every printed page via `@page`
- **PDF → Word** (pdf.js + docx): text fragments are regrouped into lines, then
  paragraphs, keeping size, bold/italic, font, centering, indents, right tabs and
  page breaks. Scanned and password-protected PDFs get a clear message instead of
  an empty file
- **Images → PDF**: drag to reorder, rotate, A4/Letter/fit-to-image, EXIF rotation
  from phone photos applied, transparent PNG areas become white
- **PowerPoint → PDF**: slides rendered to HTML (sanitized with DOMPurify, since
  it's built from file contents), one PDF page per slide at the original size
- **Excel → PDF** (ExcelJS + jsPDF autotable): selectable vector text, theme colors
  with tint, borders, merged cells, number/date/percent formats via numfmt, hidden
  rows/sheets skipped
- **PDF → Excel**: tables rebuilt purely from where the text sits — see
  [Rebuilding Tables From PDF Text](https://github.com/chalidade/devlog/blob/main/notes/rebuilding-tables-from-pdf-text.md)
- Plus a redesign: Geist, dark theme by default, logo, and an Open Graph card

**Lesson:** "in the browser" is a real constraint and a real feature. Half the work
was finding the quirks of each rendering library — html2canvas silently drops
`list-style-position: inside` bullets, so I write the bullet characters into the
slide text myself.

**Next:** more PDF tools (compress, protect/unlock, PDF → image) and sharing the
PDF text reader across all of them.
