# Prebuilt PiPup APKs

The APKs are published as **GitHub Release assets** (not committed here, to keep the
repo lean). Download them from:

➡️ **https://github.com/AnttiKaleva/PiPup/releases/tag/v0.1.5-modern**

| Asset | targetSdk | Notes |
|-------|-----------|-------|
| `PiPup-modern-targetSdk34-debug.apk` | 34 (Android 14) | Recommended. Installs without the Play Protect "older Android" warning. |
| `PiPup-legacy-targetSdk28-debug.apk` | 28 (Android 9) | Original toolchain build. Triggers the Play Protect warning (tap *Install anyway*). |

Both are debug-signed — fine for sideloading, not for Play Store distribution.

## Install (Android TV)
```bash
adb connect <tv-ip>:5555
adb install -r PiPup-modern-targetSdk34-debug.apk
# overlay permission (no Settings UI on TV):
adb shell appops set nl.rogro82.pipup SYSTEM_ALERT_WINDOW allow
```