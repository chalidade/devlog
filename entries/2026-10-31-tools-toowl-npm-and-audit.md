# Tools Becomes toowl: 72 npm Packages and a Security Audit

Overnight, [tools](https://chalidade.github.io/tools/) got a package for every
tool, a security audit, a new name, and one more tool, 73 in total.

- **Every tool is now an npm package** in `packages/`: a custom element plus an
  API without UI, with an English README. Shared element code lives in
  `packages/_shared/`, and a script creates a new package skeleton. 21 are
  published so far; the tool pages show the npm and script-tag install
- **A security audit of all 72 tools, with the fixes shipped.** A crafted
  .docx could run a script from the print button in Word to PDF; documents are
  now sanitized and printed in a sandbox. Office files can no longer load
  images from outside servers (which leaks the reader's IP). The metadata
  remover now also strips embedded JPEG previews and Extended XMP, where GPS
  could survive. Extreme inputs are refused instead of freezing the tab, and
  "12.5" is no longer read as 125 in three calculators
- **The site is now called toowl**, with an owl mascot as the icon and a text
  wordmark that follows the theme
- **Generator Surat:** five kinds of letters (job application, leave, power of
  attorney, statement, resignation) as PDF or Word

**Lesson:** a tool that promises "nothing is uploaded" also has to stop a file
from fetching things on its own. An image URL inside a document is a request
the user never made.

**Next:** publish the remaining packages.
