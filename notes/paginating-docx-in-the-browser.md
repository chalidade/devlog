# Paginating a .docx in the Browser Without Cutting Lines

docx-preview renders a Word file to HTML, one `<section>` per Word section. It only
breaks pages where Word *recorded* a break, so a long section is one tall element.
Turning that into a PDF means choosing where each page ends. Two bugs taught me how.

## Bug 1: the cut went through a line of text

My first version cut at the top of the last paragraph or table row that fit. Fine
for normal documents — but many CVs are one big layout table. One row, the whole
page. The only candidate cut was the row's top, so the fallback sliced straight
through a line of text.

Fix: cut between **actual rendered lines**, not between elements. A `Range` over
each text node returns one rect per wrapped line:

```ts
range.selectNodeContents(node)
for (const r of range.getClientRects()) boxes.push([r.top, r.bottom])
```

Images add their own boxes. Then start at the page limit and move the cut up to the
top of any box it passes through, repeating until it lands in a gap. A 1.5px overlap
tolerance stops tight line-heights from dragging the cut up through a whole
paragraph, and if nothing fits (an image taller than a page) it cuts hard at the limit.

## Bug 2: continuation pages lost their margins

The print path ("Save as PDF", for selectable text) put Word's margins on the
section as padding. A section that overflowed onto a second printed page had no top
margin there. `box-decoration-break: clone` is meant for that, but support is
patchy.

Fix: move the margins to `@page`, which the browser repeats on every printed page:

```css
/* size and margins are read from the rendered section; A4 + 1in shown */
@page { size: 794px 1123px; margin: 96px 0 96px 0 }
section.docx { padding-top: 0 !important; padding-bottom: 0 !important;
               display: block !important; overflow: visible !important }
```

docx-preview's on-screen `flex` + `overflow: hidden` also has to be undone for
print, otherwise a line at the page edge is clipped instead of moved.

## Takeaway

Test document converters against the ugliest real files you have — a CV laid out
in a single table broke an assumption every "normal" test document satisfied.
