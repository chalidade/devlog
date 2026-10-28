# Tools: QRIS With an Amount, and Receipts as PDF

Day 11 of the [tools roadmap](https://github.com/chalidade/tools/blob/main/ROADMAP.md)
was for small businesses: two tools, 67 in total.

- **QRIS Nominal:** read a shop's static QRIS from an image, a pasted
  screenshot or the camera (the same QR reader as the QR tool), type an amount,
  and download a new QR as PNG or SVG that asks the buyer for exactly that
  amount. It inserts tag 54, switches tag 01 to dynamic and recomputes the
  CRC-16. It also checks the original CRC and warns when it doesn't match.
  Nothing is sent anywhere. How it works:
  [adding an amount to a static QRIS](https://github.com/chalidade/devlog/blob/main/notes/adding-an-amount-to-a-static-qris.md)
- **Receipt and invoice:** recipient, items (quantity × price), discount and tax
  become an A4 PDF through pdf-lib. The amount in words comes from yesterday's
  Terbilang engine. The last document is kept in the browser for next time, and
  "new document" keeps only the sender's details

**Lesson:** a static QRIS is a short text with a checksum at the end. Once I
read the format, the change was a few lines: one new field, one changed flag,
and a new checksum.
