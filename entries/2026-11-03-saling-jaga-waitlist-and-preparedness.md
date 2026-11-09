# Saling Jaga: A Waitlist, Staying Alive in the Background, and Siap Siaga

Two days on [Saling Jaga](https://saling-jaga.com), v0.35.0 to v0.38.0, half on
the website and half in the app.

- **Website:** a waitlist for the iPhone and Play Store versions, written to a
  Google Sheet through Apps Script (the contact can be an email, WhatsApp, or a
  Threads/Instagram handle), an FAQ, terms of use, a Trakteer support card, and a
  privacy policy that now covers the iPhone app, chat history, voice notes,
  missing-person cards, LoRa and every permission
- **Run in the background:** the app asks to be exempt from battery limits and
  shows autostart steps for each phone brand, since some brands kill it otherwise
- **Share the app itself** to a nearby phone over Quick Share or Bluetooth, without
  internet. The App Bundle is now built without config splits so the installed APK
  is one shareable file
- **A guide** for power outages and two-way radios on PMR 409 MHz
- **Siap Siaga:** a one-time, skippable preparedness checklist (meeting point,
  background permission, offline map)
- An `uji-hp` skill for Claude Code that installs a pull request's CI build on real
  phones over adb and tests it there

**Lesson:** for an app meant for disasters, the hard part is staying installed
and alive before the disaster: background limits and getting the app onto the
phone without a store.
