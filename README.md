# BathroomReader

The Android app shell for [BathroomReader](https://bathroomreader.org) — a
[Capacitor](https://capacitorjs.com/) wrapper, not a native rewrite. It loads
the live site (`https://bathroomreader.org`) inside a WebView so it can be
packaged and installed like a normal Android app.

There's no app-specific UI or logic here. All actual content — jokes, news,
podcasts, the book reader — lives on the website itself, which isn't part of
this repo. This project only exists to produce an installable `.apk`.

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

## Using this to wrap your own site

This is a generic thin-WebView-wrapper pattern, not anything specific to
BathroomReader — feel free to fork it and point it at your own site instead.
Everything site-specific lives in `capacitor.config.json`:

```json
{
  "appId": "org.bathroomreader.app",
  "appName": "BathroomReader",
  "webDir": "www",
  "server": {
    "url": "https://bathroomreader.org",
    "androidScheme": "https"
  }
}
```

- `appId` — your app's unique identifier (reverse-domain style, e.g.
  `com.example.myapp`)
- `appName` — the name shown under the app's icon
- `server.url` — the site you want the app to load

Change those three values to your own, then follow the Building steps above.
`www/index.html` never actually renders (Capacitor loads `server.url`
instead), so there's nothing else to edit unless you want a real offline
fallback page.
