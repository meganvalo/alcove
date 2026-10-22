# alcove. — EPUB Reader

A small, installable iPhone-friendly EPUB reader designed for GitHub Pages.

## Publish on GitHub Pages
1. Create a repository (for example `alcove-reader`).
2. Upload **all four files** from this folder to the repository root: `index.html`, `manifest.json`, `sw.js`, and `icon.svg`.
3. In GitHub, open **Settings → Pages**.
4. Under Build and deployment, choose **Deploy from a branch**, select `main` and `/(root)`, then Save.
5. Wait for GitHub Pages to publish the site. Open the published URL in Safari on your iPhone.
6. Tap Share → **Add to Home Screen** → Add.

## First version features
- Open an EPUB from the iPhone Files picker (including iCloud Drive).
- Table of contents and previous/next page navigation.
- Bookmarks and text highlights.
- Text-size controls and paper, sepia, and night themes.
- Remembers the last reading position for a given filename and file size on the same device.
- Local browser storage for bookmarks and highlights.

## Notes and limitations
- The EPUB rendering engine (epub.js) loads from jsDelivr, so the first open requires an internet connection. The app shell is cached for repeat visits, but this is not a full offline EPUB library yet.
- Safari may clear site data if website data is removed. Bookmarks/highlights are stored locally in the browser and are not synced across devices.
- This is a first version: the book is selected from Files each time you open it; the original EPUB is not copied into a persistent in-app library.
- If you upload the repo under a project path, the relative links above are designed to work on GitHub Pages.
