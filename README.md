# My Library

A single-file web app for tracking a personal physical book collection.

## Run it

Open `index.html` in any browser — that's it. No install, no build, no account.

For a local server instead (optional):

```bash
python3 -m http.server 8123
```

then visit http://localhost:8123.

## Features

- **Collection & wishlist** — two views. When you buy a wishlist book, "Move to
  collection" opens a "Bought it!" step that asks which shelves it lands on
  (with the option to create a new shelf right there).
- **Add books by ISBN** — type an ISBN and click *Look up*; title, author, and cover are fetched from Open Library. Manual entry works as a fallback (or instead).
- **Shelves** — create, rename, and delete custom shelves. A book can sit on
  several at once, so shelves work both as physical locations ("Living room",
  "Office") and mental ones ("Need to read", "Did not finish"). New shelves can
  be created from the sidebar or right inside the add/edit form.
- **Custom covers** — upload a photo of your own copy (downscaled and stored
  locally); one click switches back to the ISBN cover.
- **Tags** — free-form comma-separated tags; click a tag in the sidebar to filter.
  The ✎ button opens the tag manager: add new tags, rename/delete existing
  ones across every book at once, and give each tag a color from an
  eight-color palette — the color shows on sidebar chips, book cards, and the
  detail view.
- **Search & sort** — search across title/author/tags; sort by date added, title, or author; filter by read status.
- **Read status** — unread / reading / read / did not finish. Change it from the
  add/edit form, or one click in the book's detail view.
- **Read log** — a third list for books you've read but don't own (library
  loans, borrowed copies). They keep ratings, notes, and warnings; "Add to
  collection" promotes one if you later buy a copy.
- **Book details** — click a cover or title to open a detail view with the book's
  description (fetched once from Open Library and cached), your star rating,
  content warnings, and personal notes.
- **Content warnings** — add comma-separated warnings when adding/editing a book;
  they show as ⚠ pills on the card and prominently in the detail view.
- **Ratings & notes** — 1–5 stars (click a star again to clear) and free-form
  notes, both edited right in the detail view.
- **Remove** — with a confirmation step so nothing vanishes by accident.
- **Export / import** — download your whole library as JSON for backup, or restore from a file.

## Where the data lives

Everything is stored on your device in the browser's IndexedDB (database
`myLibraryDB`) — room for thousands of books and cover photos. Nothing leaves
your device; the only network calls are the optional Open Library ISBN lookups
and cover images. Libraries created before the IndexedDB switch are migrated
automatically from `localStorage` on first load.

Clearing the browser's site data still erases the library, so the app nudges
you to **Export library** if it's been more than a month since your last
backup.

## Installing on a phone (PWA)

When served over HTTP(S) the app is a Progressive Web App: `manifest.json`
plus a service worker (`sw.js`) that caches the app shell, fonts, and covers
for offline use. Open it in a mobile browser and choose **Add to Home Screen**
/ **Install app** — it gets its own icon, opens full-screen, and works
offline. On iOS, installing also protects the data from Safari's periodic
site-data eviction. (Service workers don't run from `file://`, so install via
a hosted URL or the local server.)
