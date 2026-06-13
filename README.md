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

## Toolchain
`master` builds with the modern stack — Gradle 8.7 / AGP 8.5.2 / Kotlin 1.9.24,
AndroidX, compile/targetSdk 34, Glide 4 — and requires **JDK 17**. This is the
recommended build and removes the Play Protect "older Android" warning.

The original pre-modernization toolchain (Gradle 5.1.1 / AGP 3.4.1 / Kotlin 1.3.31,
`com.android.support`, targetSdk 28, **JDK 8**) is preserved in history at commit
[`172f2e6`](https://github.com/AnttiKaleva/PiPup/tree/172f2e6); a prebuilt legacy
APK is attached to the [v0.1.5-modern release](https://github.com/AnttiKaleva/PiPup/releases/tag/v0.1.5-modern).

## Build from source
```bash
JAVA_HOME=/path/to/jdk-17 ./gradlew assembleDebug
```
Output: `app/build/outputs/apk/debug/app-debug.apk`. Requires the Android SDK with
platform-34 + build-tools 34.0.0.

To build the original instead: `git checkout 172f2e6` and use **JDK 8** with
platform-28 + build-tools 28.0.3.

## Usage
Send a popup (multipart form to the device on port 7979):
```bash
curl -s http://<tv-ip>:7979/notify \
  -F "title=PiPup" -F "message=hello" -F "duration=8" -F "position=0"
```