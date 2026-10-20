# Kita Berkembang: A README With the Tests to Back It

[Kita Berkembang](https://kitaberkembang.com), my online-store platform for small
Indonesian businesses, got an English README (PR #17, documentation), drafted by
Claude Code from the code.

- Features grouped by who uses them (store owners, buyers, the platform admin),
  then the architecture: a WordPress Multisite with one plugin, where each store
  is a subsite
- A security section listing only what the plugin actually does: login lockout
  per IP, XML-RPC and user enumeration closed, security headers, image-only
  uploads with PHP blocked in `uploads`, server-side pricing, rate limits on
  orders, and CSV-injection-safe exports
- Test counts stated exactly: **97 PHPUnit test methods (104 cases with data
  providers) in 15 classes**, and **32 Playwright tests in 9 specs** on a Pixel 7
  and a desktop Chrome project
- The CI pipeline written out: PHPUnit and Playwright must both pass before the
  FTP deploy job runs, and merging to `main` deploys to production
- The previous Indonesian README stays as `README.id.md`

**Lesson:** a security section is only worth writing if each line points at
code. Written that way, it doubles as a checklist for the next review.
