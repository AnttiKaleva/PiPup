# PiPup

Picture-in-picture style popup notifications for Android TV. A foreground service
runs a small HTTP server (port `7979`); POST a request to it and PiPup draws a
notification overlay (text / image / video) on top of whatever is playing.

App id: `nl.rogro82.pipup`. Fork of [rogro82/PiPup](https://github.com/rogro82/PiPup).

## Downloads

Prebuilt debug-signed APKs are attached to the
**[v0.1.5-modern release](https://github.com/AnttiKaleva/PiPup/releases/tag/v0.1.5-modern)**:

- `PiPup-modern-targetSdk34-debug.apk` — **recommended**, installs cleanly on Android 14.
- `PiPup-legacy-targetSdk28-debug.apk` — original build (Play Protect shows an "older
  Android" warning; tap *Install anyway*).

## Install (Android TV)
```bash
adb connect <tv-ip>:5555
adb install -r PiPup-modern-targetSdk34-debug.apk
adb shell appops set nl.rogro82.pipup SYSTEM_ALERT_WINDOW allow   # overlay perm (no TV Settings UI)
```

## Branches
- **`master`** — original toolchain: Gradle 5.1.1 / AGP 3.4.1 / Kotlin 1.3.31,
  `com.android.support`, compile/targetSdk 28. Builds only on **JDK 8**.
- **`modernize-agp8`** — modernized: Gradle 8.7 / AGP 8.5.2 / Kotlin 1.9.24, AndroidX,
  compile/targetSdk 34, Glide 4. Builds on **JDK 17**. Removes the Play Protect warning.

## Build from source
```bash
# modern (this branch)
JAVA_HOME=/path/to/jdk-17 ./gradlew assembleDebug

# legacy (master branch)
JAVA_HOME=/path/to/jdk-8  ./gradlew assembleDebug
```
Output: `app/build/outputs/apk/debug/app-debug.apk`. Requires the Android SDK with
the matching platform + build-tools (28 for legacy, 34 for modern).

## Usage
Send a popup (multipart form to the device on port 7979):
```bash
curl -s http://<tv-ip>:7979/notify \
  -F "title=PiPup" -F "message=hello" -F "duration=8" -F "position=0"
```