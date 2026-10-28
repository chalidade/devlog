# Tools: Prayer Times, Qibla Direction and Hijri Dates

Day 9 of the [tools roadmap](https://github.com/chalidade/tools/blob/main/ROADMAP.md)
was worship: three tools, 62 in total. All three work without an API.

- **Prayer times:** Imsak, Subuh, sunrise, Dhuha, Zuhur, Asar, Maghrib and Isya
  for 48 bundled cities or your GPS location, with the next prayer marked and a
  printable month table. The times are computed on the device from the sun's
  position with Kemenag's parameters: Subuh at 20°, Isya at 18°, Asar at a
  shadow of 1×, and a 2-minute ihtiyat
- **Qibla direction:** the angle and distance to the Ka'bah from your location,
  plus a live phone compass through `DeviceOrientationEvent` (with the sensor
  permission prompt iOS needs), telling you to turn left or right, and a
  calibration warning
- **Hijri ⇄ Gregorian:** both directions through the `islamic-umalqura`
  calendar built into `Intl`, plus the year's Islamic holidays. The page notes
  that Kemenag's official dates come from moon sighting and can differ by a day

**Lesson:** `Intl` already ships a Hijri calendar, and prayer times are
astronomy plus a few published angles. Neither needs a server. The honest part
is saying where the computed answer and the official one can disagree.
