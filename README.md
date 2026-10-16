# while-site

The two pages the App Store requires for **While.**, and a landing page so the
root URL is not a 404.

```
index.html     While. — links to the two below
privacy.html   Privacy policy  ← App Store Connect: Privacy Policy URL
support.html   Support page    ← App Store Connect: Support URL
brand.css      §10 of the master reference, applied to the web
fonts/         Nunito 600/700 and Inter 400/500/600, latin subset, 89 KB
.nojekyll      Stops GitHub Pages running Jekyll over the files
```

## The fonts are self-hosted on purpose

§10.5 forbids a third-party font CDN: an extra connection on first paint, and a
privacy liability. Here it would be worse than that — `privacy.html` says the
app contacts nobody, and serving the page that says so from Google Fonts would
contradict it in the act of claiming it.

Both faces are SIL Open Font Licence. Licences are in `fonts/`.

**This repo is public on purpose, and the app repo is not.** These are the only
two files that have to be reachable by a stranger; everything else — the source,
the master reference, the strategy and pricing notes — stays private.

## Turning on GitHub Pages

1. Push this folder to a **public** repo named `while-site`.
2. Settings → Pages → Source: **Deploy from a branch** → `main` → `/ (root)` → Save.
3. Wait a minute, then check both URLs resolve:
   - `https://<user>.github.io/while-site/privacy.html`
   - `https://<user>.github.io/while-site/support.html`

Paste those into App Store Connect under **App Information**. Both are
mandatory; a `mailto:` link is rejected as a support URL.

## If you buy a domain

Do it **before** submitting rather than after. Apple expects these URLs to
resolve for the life of the app, and changing them later means editing a live
listing. Add the domain in Settings → Pages → Custom domain, put a `CNAME` file
at the root, and the URLs become `whileapp.com/privacy` and `/support`.

## Keeping them true

The privacy policy makes one load-bearing claim: **the app contains no
networking code**. That was verified before it was written —
`grep -rE "URLSession|URLRequest|WKWebView|NWConnection|dataTask"` over the
project returns nothing, and there are zero third-party package dependencies.

If that ever stops being true, this page is wrong **before** the code ships, not
after. The same goes for "no analytics" and "nothing leaves your phone".

Source of these files: `web/` in the private app repo. Edit them there and copy
across, so the two do not drift.
