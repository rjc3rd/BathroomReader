# BathroomReader

The Android app shell for [BathroomReader](https://bathroomreader.org) — a
[Capacitor](https://capacitorjs.com/) wrapper, not a native rewrite. It loads
the live site (`https://bathroomreader.org`) inside a WebView so it can be
packaged and installed like a normal Android app.

There's no app-specific UI or logic here. All actual content — jokes, news,
podcasts, the book reader — lives on the website itself, in a separate repo.
This project only exists to produce an installable `.apk`.

## Structure

- `www/` — placeholder loading page; Capacitor points the WebView at the
  configured remote URL instead of bundled assets
- `capacitor.config.json` — app id, name, and the remote URL it loads
- `package.json` — Capacitor CLI/core/android dependencies

## Building

```bash
npm install
npx cap add android   # first time only
npx cap sync
npx cap open android
```

Then build/run from Android Studio as usual.
