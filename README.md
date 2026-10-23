# alcove.

A small, private EPUB and PDF reader that runs entirely in your browser. No app store, no account, no server. Host it for free on GitHub Pages, add it to your home screen, and it behaves like a native reading app.

It's built mainly for iPhone and iPad (Safari), but works in any modern browser.

## Features

**Library**
- Import EPUB and PDF files from your device (multiple at once)
- Cover grid with reading progress, search, rename (title and author) and delete
- Reading dates for every book: when you started it, when you last read it, and when you finished it (set automatically, and editable from the book's details)
- Opens the last book you were reading, right where you left off

**Reading EPUBs**
- Two layouts: **pages** (tap or swipe to turn) and **continuous scroll** across chapters
- Jumps to Chapter 1 or the Introduction the first time you open a book (falls back to the title page)
- Table of contents, a progress slider, and a "back to where you were" button after following footnotes or links
- Bookmarks and highlights (four colors) with a list of each per book
- Tap an image to view it full screen, with pinch and double-tap zoom
- Settings: text size, serif or sans, theme (black, graphite, light, auto), margins, line spacing

**Reading PDFs**
- Continuous scroll with pinch and double-tap zoom
- Table of contents (from the PDF's outline), page slider, bookmarks
- Optional dark rendering for dark themes

**Other**
- Works offline once loaded
- Position is saved precisely (by text location, not just percentage), so it survives changing text size or layout
- Everything stays on your device

## Supported devices and browsers

| Platform | Browser | Status |
|---|---|---|
| iPhone, iPad (iOS / iPadOS 16.4 or newer) | Safari, and installed to the Home Screen | Primary target |
| Mac | Safari 16.4+, Chrome, Edge, Firefox | Should work |
| Android | Chrome, Edge, Samsung Internet, Firefox | Should work |
| Windows / Linux | Chrome, Edge, Firefox | Should work |

Notes:
- **iOS / iPadOS 16.4+** is needed because the app reads EPUB files with the browser's built-in decompression support, which arrived in that version. Older versions can't open books.
- Only Safari can install web apps on iPhone and iPad. Other iOS browsers can open the site but can't add it to the Home Screen as a proper app.
- Testing so far: the author uses it on iPad and iPhone, and the code has been run through automated tests in a phone-sized Chromium browser. Other combinations in the table are expected to work but haven't all been tried. Issues and reports are welcome.

## Install (host it yourself)

You need a free GitHub account.

1. **Create a repository** (for example `alcove`).
2. **Upload these three files** to the root of the repo:
   - `index.html`
   - `sw.js`
   - `icon.png`
3. In the repo go to **Settings → Pages**. Under **Build and deployment**, set **Source** to "Deploy from a branch", choose the `main` branch and the `/ (root)` folder, then save.
4. After a minute or two your site is live at `https://YOUR-USERNAME.github.io/REPO-NAME/`.

### Add it to your phone or tablet

- **iPhone / iPad:** open the site in **Safari**, tap the **Share** button, choose **Add to Home Screen**, then open alcove. from the new icon.
- **Android:** open the site in Chrome, open the menu, and choose **Install app** or **Add to Home screen**.
- **Desktop:** just open the link in your browser, or use your browser's "Install" option.

> **Add your books after installing.** On iOS, the Home Screen app and Safari keep separate storage, so books imported in a Safari tab won't appear in the installed app.

## Using it

### Adding books
Tap **add**, then pick `.epub` or `.pdf` files from the Files app. Tap **edit** on the library screen to rename or delete a book.

### Page mode
| Action | What it does |
|---|---|
| Tap the right 30% of the screen, or swipe left | Next page |
| Tap the left 30% of the screen, or swipe right | Previous page |
| Tap the middle | Show or hide the menu |
| Press and hold a word, then drag | Select text to highlight |
| Tap a highlight | Change its color, copy it, or delete it |
| Tap an image (middle of the screen) | View it full screen |
| Tap the percentage at the bottom | Show or hide the menu |

### Scroll mode
Scroll normally. Tap the middle to show the menu. Select text the usual iOS way to highlight it.

### PDFs
Scroll through pages, pinch or double-tap to zoom, and tap once to show the menu.

### Menu
Top bar: **library**, bookmark ribbon, **contents** (contents, bookmarks, highlights), **settings**. Bottom bar: slider to jump anywhere in the book.

### Keyboard (iPad keyboard or desktop)
Right arrow or space: next page. Left arrow: previous page. Escape: close panels or the menu.

## Your data and privacy

- Books, covers, reading positions, dates, bookmarks and highlights are stored in your browser's local storage (IndexedDB) on that device. Nothing is uploaded anywhere.
- There are no accounts, no analytics and no tracking.
- The only network request the app makes beyond loading its own files is for **PDF support**: the first time you add or open a PDF it downloads [PDF.js](https://mozilla.github.io/pdf.js/) from the cdnjs CDN. It's cached afterwards, so PDFs then work offline.
- **Nothing syncs between devices.** If you clear website data, delete the Home Screen app, or iOS clears storage for an unused site, your library goes with it. Keep your original book files.

## Limitations

- No DRM support. Copy-protected EPUBs (for example from Kindle or Kobo stores) won't open.
- Highlights work in EPUBs only, not PDFs.
- No search inside a book yet.
- EPUBs are shown with alcove.'s own typography. The publisher's styling is intentionally stripped (this keeps themes consistent), so some books lose special formatting. Fixed-layout EPUBs (such as some comics and picture books) aren't specially handled.
- Scripts and interactive content inside EPUBs are removed for safety.
- Light mode uses a black strip behind the iOS status bar, because iOS fixes the clock and battery text to white for web apps like this.

## Troubleshooting

- **I updated the files but nothing changed.** Fully close the app and reopen it. If it still looks old, remove it from the Home Screen and add it again. Your books are stored separately and should stay.
- **A book won't open.** It may be DRM-protected or damaged. Try opening it in another reader to check.
- **PDFs won't add or open.** You need an internet connection the first time, so the PDF library can download.
- **Books disappeared.** The browser's storage was cleared. Re-add them from your files.
- **A cover is missing.** Covers are rebuilt automatically from the book file the next time you open the library.

## How it's built

A single `index.html` of plain HTML, CSS and JavaScript, with no build step and no dependencies to install.

- Reads EPUB files with a small built-in ZIP reader (uses the browser's `DecompressionStream`)
- Stores everything in IndexedDB
- `sw.js` is a small service worker that makes the app load offline
- PDF rendering uses PDF.js, loaded on demand

To customize it, edit `index.html` directly. Colors live in the `body[data-theme=...]` rules at the top of the stylesheet.

## Credits

- Title font: **Chrysanthi Unicode**, a freeware font from [FontSpace](https://www.fontspace.com/chrysanthi-unicode-font-f13315). It's embedded in the file, trimmed to Latin characters to keep the app small. Check its license on FontSpace if you plan to redistribute your own copy.
- PDF support: [PDF.js](https://github.com/mozilla/pdf.js) by Mozilla, Apache License 2.0, loaded from cdnjs at runtime.

## License

Add the license of your choice here (MIT is a common option for projects like this).
