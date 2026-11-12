# Rituximab Rate Buddy (offline web app)

A small phone-first web app that works out the rituximab dose row, pump rates and step timer from the trust infusion chart,
keeps a session log with pump and observation tick-boxes, and produces a downloadable record (PDF or text).

**Clinical aid only. Verify every dose and rate against the trust protocol and the prescription.**
It does not replace local policy, the pump's own checks or the official record. It asks for no patient identifiers and stores
no patient data (only display preferences such as the colour theme are saved on the device).

## What is in this folder

| File | Purpose |
| --- | --- |
| `index.html` | the whole app (HTML, CSS and JavaScript, no external requests) |
| `manifest.json` | web app manifest (relative `start_url` and `scope`, so it works under any sub-path) |
| `sw.js` | service worker: cache-first precache, versioned cache name, old caches removed on activate |
| `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` | icons |
| `.nojekyll` | tells GitHub Pages to serve the files as they are |

## Publish on GitHub Pages

1. Create a repository named `rituximab-rate-buddy` and put the contents of this folder at the repository root.
2. Settings > Pages > Deploy from a branch > `main` / `(root)`.
3. Open `https://<user>.github.io/rituximab-rate-buddy/` once while online. The app shows "Ready for offline" when it has saved itself.
4. Install it: Android/desktop Chrome and Edge offer **Install app** in Settings; on iPhone use Share > Add to Home Screen.

All URLs are relative, so the same files also work from a custom domain or any other static host over HTTPS.

## Releasing an update

Rebuild with `python3 make-ghpages.py` (it computes a content hash for the cache name in `sw.js`), or bump `VERSION` in `sw.js`
by hand if you edit files directly. Devices pick up the new version the next time they open the app while online;
the old cache is deleted automatically. A new version never reloads a page that is running an infusion timer.
