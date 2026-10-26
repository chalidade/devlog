# fet: A Learning Room That Stores Your Work in Your Own Drive

The second half of the [fet](https://chalidade.github.io/fet/) day: every
roadmap stage got a place to actually do the work, and the site got a
community to show it in.

- **Ruang Belajar** (learning room), one per stage: a code editor with a live
  preview in a sandboxed iframe, notes, a status, and a recorder for camera or
  screen video. Work can be exported as a `.zip` or to Google Drive, or
  published to the community
- **Supabase** for accounts and data: sign-in with GitHub or Google, profiles
  showing progress across the 20 stages, posts, comments and reactions. Row
  level security on every table; a stage's own work is visible only to its owner
- **Videos go to the learner's own Google Drive**, uploaded straight from the
  browser into `fet-belajar/<stage>/`, with the
  `drive.file` scope. How that works is in
  [storing user videos in their own Drive](https://github.com/chalidade/devlog/blob/main/notes/storing-user-videos-in-their-own-drive.md)
- **Community pages:** a feed per stage, post pages with an embedded video,
  code and sanitised markdown
- **Tickable concept maps.** A markdown-it rule turns `- [ ]` items on roadmap
  pages into checkboxes, numbered the same way in both languages so a tick
  means the same concept in either. The stage banner shows mastered/total,
  saves to `localStorage` and, when signed in, to `stage_work.checked`. Ticking
  the first concept marks the stage as in progress
- **A UI refresh:** a calmer indigo palette, a shorter navbar, a sticky icon
  tab bar in the learning room, and a code/preview toggle on small screens
- The Google OAuth client ID went into `docs/.env` at the end of the day. A
  client ID is public by design, and there's no client secret in this flow

**Lesson:** the cheapest storage for large user files is storage the user
already has. Drive's `drive.file` scope makes that a fair request, because the
app can see only the files it made.
