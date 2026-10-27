# Building an Android APK Without Gradle

The cloud sandbox where Saling Jaga was built could reach Maven Central and
Ubuntu's apt, but not `dl.google.com` or Google's Maven, so the Android Gradle
Plugin was out.
The app still had to ship as a signed APK with screenshot tests in CI.

## The approach
Ubuntu packages the old but complete Android toolchain:

```bash
sudo apt-get install android-sdk-platform-23 aapt dalvik-exchange apksigner zipalign
aapt package -f -m -J gen -M AndroidManifest.xml -S res -I android.jar -F unsigned.apk
javac -source 8 -target 8 -bootclasspath android.jar -d classes $(find java gen -name '*.java')
java -jar dx.jar --dex --output=classes.dex classes && aapt add unsigned.apk classes.dex
zipalign -f 4 unsigned.apk aligned.apk && apksigner sign --ks release.jks --out app.apk aligned.apk
```

- Compile against API 23 but set `targetSdkVersion` 33 in the manifest. Newer APIs
  (notification channels) are called through reflection
- The UI is built in code: no XML layouts, no AndroidX, no dependencies
- `aapt package --version-code N --replace-version` stamps the build number, so CI
  can make every release an update over the last one

For tests, Robolectric 4.14 runs from Maven Central with native graphics. It
renders the real activity to PNG, which is where the README screenshots come
from.

## Gotchas
- `dx` only accepts Java 8 bytecode, so no lambdas. Anonymous classes everywhere
- Robolectric depends on `androidx.test`, which lives on Google's Maven. Excluding it
  and writing about 24 small stub classes in the test source set worked
- Robolectric also needs `android-all` as `testRuntimeOnly`, or it fails with
  `TypeNotPresentException: android.app.Application`
- Dialogs are separate windows, so screenshotting the activity misses them. Draw the
  activity, dim it, then draw the latest dialog's decor view on top

## When to use it
Small apps where you want a tiny APK, a build anyone can reproduce with apt, or
when Google's hosts are unreachable. For anything with Jetpack libraries, Compose
or Play Store app bundles, use Gradle. This path stops being worth it as soon as
you need a single AndroidX dependency.
