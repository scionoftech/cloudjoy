# CloudJoy — cloud gaming for Google TV

An Android TV app that loads https://www.xbox.com/play in a fullscreen WebView with a
desktop (Edge on Windows) user-agent, since Microsoft blocks the Android WebView UA.
Sign in with your Microsoft account (Game Pass Ultimate required) and play with a
Bluetooth controller paired to the TV.

## Build

```bash
export JAVA_HOME=/opt/homebrew/opt/openjdk@17
./gradlew assembleRelease
# → app/build/outputs/apk/release/cloudjoy-1.0.apk
```

A prebuilt APK is included at the repo root: [`cloudjoy-1.0.apk`](cloudjoy-1.0.apk)

## Install on Google TV

1. On the TV: Settings → System → About → click **Android TV OS build** 7 times to
   unlock Developer options, then enable **USB debugging** (network debugging on some
   models: Developer options → Wireless debugging / ADB over network).
2. Find the TV's IP: Settings → Network & Internet → your network.
3. From this Mac:

```bash
export PATH="/opt/homebrew/share/android-commandlinetools/platform-tools:$PATH"
adb connect <TV_IP>:5555        # accept the prompt on the TV
adb install cloudjoy-1.0.apk
```

The app appears in the launcher as **CloudJoy** (white cloud with a play button on blue).

Alternatively, install a file-manager/sideload app on the TV (e.g. "Send files to TV")
and open the APK from there.

## Notes

- **Controller**: pair a Bluetooth gamepad with the TV itself. The web page reads it via
  the browser Gamepad API — this needs a reasonably current Android System WebView
  (v121+, Jan 2024); update it via the Play Store on the TV if input doesn't work in games.
- **B button vs BACK**: the app swallows gamepad BACK so pressing B in a game doesn't
  exit; the remote's back button navigates web history, double-press exits.
- **Login** persists via cookies; you only sign in once.
- The release APK is signed with the debug key — fine for personal sideloading, not for
  Play Store distribution.

## License

[MIT](LICENSE) © 2026 Sai Kumar Yava

## Disclaimer

CloudJoy is an unofficial, independent personal project. It is not affiliated with,
endorsed by, or sponsored by Microsoft Corporation. **Xbox, Xbox Cloud Gaming,
Xbox Game Pass, and all associated logos and trademarks are the property of
Microsoft Corporation.** All other trademarks are the property of their respective
owners. This app does not host, modify, or redistribute any game content — it simply
displays the official [xbox.com/play](https://www.xbox.com/play) website.

Use this app at your own risk — it is provided as-is, with no warranty of any kind.
This GitHub repository is the **only official source** for CloudJoy; it is not published
anywhere else (no Play Store, no app stores, no other websites). Any copy found
elsewhere is unofficial and should not be trusted.
