# Kita Berkembang: Income and Expenses, and More Than One Product Photo

A round of changes to [Kita Berkembang](https://kitaberkembang.com) from my own list
after using the store dashboard: one merged PR (#16, 33 files, about 1,100 lines
added) released as version 0.10.0. Claude Code wrote the code and tests from my
requirements; I reviewed the screenshots and tested the live site.

- **New Income and Expenses menus.** Income lists completed orders plus income the
  owner records by hand, such as a bazaar sale. An expense has a name, category,
  quantity and total; the unit price is computed from total divided by quantity,
  so the owner types what is on the receipt instead of doing the division
- The dashboard home shows profit for the period, and a loss is written "-Rp" so a
  negative number is not missed. Both menus sit behind a new feature switch, like
  every other feature
- Products take up to eight photos, and the first one is the thumbnail. Products
  saved with a single photo keep working without a migration step
- Settings got shorter: contact and social links moved there from the landing page,
  the free-text opening hours field was removed in favour of the existing per-day
  schedule, and the map location picker opens as a pop-up so the owner focuses on
  placing the pin
- Owners choose a map pin from 20 icons or their logo, and can add a Google review
  link to the order page. The link must be https on a Google domain, because it is
  shown to buyers
- Shipping fees and new-order notifications are now off by default and hidden,
  and the server ignores them when the switch is off, not just the settings page
- CI runs 104 PHPUnit tests and 32 Playwright tests before the deploy

**Lesson:** for a small food stall, a finance feature succeeds when it matches the
receipt in their hand. Ask for what is printed on it, the total and the quantity,
and let the software do the division.

**Next:** export the income and expense records to a spreadsheet for monthly
bookkeeping.
