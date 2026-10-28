# weeknoo: One Repo for Every Website, and a Prayer Tracker as Its First App

First day of [weeknoo](https://github.com/chalidade/weeknoo), my website
workspace. The rule is one repo and one flow: every site lives in
`sites/<name>/` and is generated from a shared `template/`, so all of them run
on the same stack (Vite, React 19, Tailwind v4, shadcn/ui, Motion). Twelve
commits, most of them written by Claude Code.

- **The workspace:** a generator script, the 21st.dev component registry wired
  into shadcn, typed clients for Quran, hadith, asbabun nuzul and Indonesian
  region data, a Capacitor pipeline (`npm run apk`), and GitHub Actions that
  build every site on push
- **Every site gets a public link.** CI publishes each one to GitHub Pages under
  `/weeknoo/<site>/`
- **A local database module** in the template: one Dexie (IndexedDB) database
  per site, plus helpers that export the whole thing to a JSON file and import
  it back. That replaced `localStorage` for apps that store what the user writes
- **The homepage and the prompt pipeline.** The homepage at the Pages root has a
  prompt box that opens a prefilled GitHub issue labeled `prompt`, and a Claude
  Code routine picks it up. I added a client-side access-code screen the same
  day; I deleted it again on 3 October, once it was clear it protected nothing
- **PANDUAN.md**, one manual in Indonesian, and CKEditor 5 and Recharts
  installed in the template
- **JAIM (Jaga Iman)**, a worship tracker, as web app and APK: per-prayer status
  (on time, late, missed) with a 14-day date scroller, a 30-juz recitation grid,
  and a prayer schedule from your location with a live countdown. By night it
  had an evaluation tab (2 points per prayer on time, +1 at the mosque as a
  bonus, so a day can go over 100%), monthly and yearly comparison, local
  profiles with an optional PIN, and a Qur'an tab with per-ayah audio and the
  asbabun nuzul shown under the verses that have one
- **An APK bug worth remembering:** "use my location" did nothing in the APK.
  With no location permission in the manifest, the WebView refuses without ever
  showing a dialog. The fix went through `@capacitor/geolocation`, plus a button
  that opens settings when the permission is permanently denied. Permissions now
  live in `sites/<name>/android-permissions.txt` and the build script injects
  them, because the `android/` folder is regenerated

**Lesson:** a WebView inside an APK doesn't behave like a browser. The browser
asks the user; the WebView asks the manifest, and when the manifest says nothing
the answer is no, with no error to tell you why.
