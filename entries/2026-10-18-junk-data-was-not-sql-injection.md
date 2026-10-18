# The Junk Data Wasn't SQL Injection

The site's database kept filling with junk, mostly thousands of accounts with
random names like `JTxvfYloXc`, and the working theory was SQL injection. It
wasn't. There's no raw SQL in the app (it's all the query builder), so I went
looking for what actually let data in.

- **Admin routes had no server-side check.** The admin layout redirected
  non-admins in JavaScript, after the page had loaded. A logged-out request
  could still create and delete records, and a student could delete users. I
  added `auth` plus a small `admin` middleware on the whole route group.
- **The payment webhook trusted its body.** One request could mark any order
  as paid. It now checks the provider's callback token, and it always re-reads
  the invoice from the provider's API before updating anything.
- **IDs from the request were trusted:** the profile update took a hidden
  `id` field, invoices and certificates were viewable by number, and an order
  URL accepted any user id. Each one now uses the logged-in user.
- **Bot sign-ups:** account confirmation links are now signed URLs. Register
  and password reset are throttled, and register has a honeypot field and
  Cloudflare Turnstile. The honeypot had a bug of my own: Laravel 8's
  `prohibited` rule fails when the field is *present*, even empty, which would
  have rejected every real sign-up. I caught it in a local test, before it
  shipped. It's `nullable|max:0` now.
- **The biggest hole wasn't in the app.** The site is served from the project
  root, so Apache served every real file: `/.env`, `/.git/`, the logs. Debug
  mode was on as well. `.htaccess` now refuses dotfiles (except
  `.well-known`), source folders, logs and any script under the upload folders.
  Uploads only accept real images. All the secrets were rotated afterwards.
- A read-only FTP scan of the upload folders found 371 images, one certificate
  PDF and no PHP files.

**Lesson:** "SQL injection" was the wrong suspect. The junk came in through the
front door: endpoints that never asked who was calling. Before reaching for a
new login system (Google sign-in was suggested), make every write endpoint
check who is asking.
