# Git and Auto-Deploy for a Site That Only Lived on Shared Hosting

An online-class site I look after (Laravel 8 on cPanel shared hosting) had no
working repo: the live code was whatever sat on the server. Today it got a
private GitHub repo and deploys itself on every push to `master`.

- Committed the code downloaded from the server, and stopped tracking `.env`.
  The payment provider's secret key moved out of `config/` and into `.env`.
- **GitHub Actions + FTP**, because the host has no SSH.
  [SamKirkland/FTP-Deploy-Action](https://github.com/SamKirkland/FTP-Deploy-Action)
  keeps a sync-state file on the server, so after the first run it uploads
  only changed files (about 40 files in 38 seconds).
- Excluded what only the server should own: `.env`, uploads in `storage/`,
  `vendor/` and `bootstrap/cache/`. `vendor/` is out on purpose: the server
  runs with Composer's dev packages, which are listed in
  `bootstrap/cache/packages.php`. A CI-built `vendor/` without them would
  crash the site on boot.
- Pushes that only touch `.github/` don't deploy, so workflow changes are safe
  to iterate on.
- The first full sync stopped at file 2,306 of 2,784 with
  `553 Permission denied`. A read-only `lftp` listing workflow showed one file
  with mode `444` since 2020. The fix was a chmod, then an hour-long re-upload,
  because a failed run never writes its sync state.
- **A near miss:** `core.ignorecase=true` had kept a layout folder tracked as
  `MainWeb/` while every view referenced `mainWeb/`. On Linux hosting, that
  would have broken 11 pages.

**Lesson:** look at what the server actually depends on (dev packages,
read-only files, folder-name case) before treating it as a fresh deploy
target. Each one of these would have taken the site down quietly.

**Next:** the first deploy re-uploads everything, so keep the sync-state file
on the server forever.
