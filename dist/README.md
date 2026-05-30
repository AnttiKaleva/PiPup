# Prebuilt PiPup APKs (debug-signed)

Two builds are provided:

| APK | targetSdk | Toolchain | Notes |
|-----|-----------|-----------|-------|
| `PiPup-legacy-targetSdk28-debug.apk` | 28 (Android 9) | Gradle 5.1.1 / AGP 3.4.1 / Kotlin 1.3.31, `com.android.support` | Original toolchain. Builds only on **JDK 8**. Triggers Google Play Protect "designed for an older Android version" warning on install (tap *Install anyway*). |
| `PiPup-modern-targetSdk34-debug.apk` | 34 (Android 14) | Gradle 8.7 / AGP 8.5.2 / Kotlin 1.9.24, AndroidX | Modernized (branch `modernize-agp8`). Builds on **JDK 17**. Installs without the Play Protect warning. |

Both are **debug-signed** (Android debug keystore) — fine for sideloading, not for Play Store distribution.

## Install (Android TV)
```bash
adb connect <tv-ip>:5555
adb install -r dist/PiPup-modern-targetSdk34-debug.apk
# overlay permission (no Settings UI on TV):
adb shell appops set nl.rogro82.pipup SYSTEM_ALERT_WINDOW allow
```

## Source
- Legacy code: branch `master`
- Modernized code: branch `modernize-agp8`