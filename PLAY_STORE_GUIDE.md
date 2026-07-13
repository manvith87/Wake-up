# Getting "Wake Up" onto the Play Store

The app in this folder (`index.html`, `manifest.json`, `sw.js`) is a real, working prototype:
voice-controlled alarm setting, a sunrise progress arc, alarm list with toggles, and it rings
when the time hits — as long as the browser tab is open.

That last part is the catch for the Play Store. There are two honest paths from here,
depending on what you need.

## Path A — Fast: wrap this web app (good for a demo / MVP)

Tools like **Bubblewrap** or **PWABuilder** wrap a PWA into an Android app (a "Trusted Web
Activity") that you can upload to the Play Store as-is.

Steps:
1. Host these three files on a real HTTPS domain (GitHub Pages, Netlify, Vercel — all free).
2. Add real icon files (`icon-192.png`, `icon-512.png`) referenced in `manifest.json`.
3. Go to https://www.pwabuilder.com, paste your URL, and it will generate a signed Android
   package (.aab) for you.
4. Create a Google Play Developer account (one-time $25 fee) at
   https://play.google.com/console.
5. Upload the .aab, fill in the store listing (screenshots, description, privacy policy —
   required even for simple apps), and submit for review.

**Limitation to know:** because it's still web tech under the hood, Android may kill the
background timer if the phone is locked/idle for a while, so the alarm isn't 100% guaranteed
to fire like a native alarm clock. Fine for personal use or an early prototype; risky for a
polished "reliable alarm" product.

## Path B — Solid: rebuild natively for real background alarms (recommended for a serious app)

For an alarm to ring reliably even when the app is closed and the phone is locked, it needs
Android's native `AlarmManager` + a foreground service — that only works in a native Android
project (Kotlin/Java) or a cross-platform framework like **React Native** or **Flutter** with
a native alarm plugin.

If you want this, I can generate the full source for either:
- A native Android Studio project (Kotlin) — most reliable, direct AlarmManager access.
- A React Native project — if you'd rather work in JavaScript, using a library like
  `notifee` or `react-native-alarm-notification` for the native alarm bridge, and
  `@react-native-voice/voice` for on-device speech recognition.

Either way, you'd still need to:
1. Build it in Android Studio (or `expo prebuild` for React Native).
2. Get a Google Play Developer account ($25 one-time).
3. Sign the release build and upload the `.aab` to Play Console.
4. Fill out the store listing, content rating questionnaire, and privacy policy (Play Store
   requires a privacy policy URL for any app that uses the microphone).

I can't compile, sign, or upload an app from this environment (no Android SDK or network
access here), but I can write all the source code for either path — just tell me which one
and I'll get started.

## Quick note on the microphone permission

Since this app listens for voice commands, the Play Store listing will need to disclose
microphone use in the privacy policy and Android will show a runtime permission prompt the
first time — both paths above need this regardless of which you pick.
