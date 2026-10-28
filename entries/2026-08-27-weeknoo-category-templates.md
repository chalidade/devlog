# weeknoo: Nine Category Templates, So a Site Doesn't Start Blank

Two days after the workspace started, the blank starter turned out to be the
slow part. Every new site began from an empty hero.

- **`npm run new -- <site> --category <name>`** now copies a category overlay
  over the template and gives a complete page (Navbar, Hero, content sections,
  Footer) with its own palette, Google Fonts and Indonesian dummy copy. Nine
  categories: portfolio, company profile, product landing, SaaS, restaurant,
  blog, education, photography and local business
- Eleven more categories are written up in `categories/SPEC.md` but not built.
  The spec is the contract for all of them: allowed imports, styling with tokens
  only, no external images
- **`npm run check-categories`** builds each overlay against a throwaway site
  (`sites/.catcheck`, git-ignored, installed once) so a broken template shows up
  before anyone uses it
- **kopi-senja**, a coffee-shop landing page, came in through the prompt
  pipeline (issue #2): menu, testimonials, opening hours and location
- The prompt-runner routine moved to polling every hour (`18 * * * *`)
- **`npm run delete -- <site>`** removes a site and its card on the homepage
  gallery, after you type the site's name again to confirm

**Lesson:** a template that only one script uses will rot quietly. A command
that builds every overlay is what keeps nine of them usable.
