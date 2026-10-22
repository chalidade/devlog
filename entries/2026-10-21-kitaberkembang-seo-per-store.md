# Kita Berkembang: Every Store Gets Its Own Sitemap

[Kita Berkembang](https://kitaberkembang.com) runs each store as a subsite on its
own subdomain. Until now Google saw none of that: WordPress's built-in sitemap
only listed the sample page.

- Turned off the default sitemap content. Each store now serves `/sitemap.xml`
  with its home page and order page, and the main site serves an index of its own
  pages plus the sitemap of every active store. `/wp-sitemap.xml` still works
- Each site's `robots.txt` points to its own sitemap
- A new `KB_SEO` class writes the head of every page: description, canonical URL,
  Open Graph and Twitter card, and JSON-LD (`LocalBusiness` for a store, `Product`
  with an IDR `Offer` for its items, `Organization` and `WebSite` for the
  platform, and a list of stores for the map)
- `noindex` on the order pages reached from inside the map, and on theme pages of
  store sites, so they don't compete with the real pages
- A PHPUnit class for the SEO output, and a Google Search Console guide (a Domain
  property, so one verification covers every subdomain) in the cPanel deploy docs

**Lesson:** on a multisite, SEO is per subdomain. Each store is a separate site
to Google, so each needs its own sitemap, robots file and canonical URL.
