Personal Library Manager is a clean, browser-based app for organizing and tracking your entire book collection. It runs fully in your browser, works on GitHub Pages, and lets you catalog details, track reading progress, manage book values in multiple currencies,
etc.

NOTE: Sync between devices is availaible, but not automatically, tbh I didn't feel like doing it, cause I made this program for myself, but thought to share it with others since there are people who need something like this that isn't behind a pay-wall.
If you really want cloud sync, I did put it in the code, just reuse my code and enable it yourself. I put how to do this at the bottom of this read me section, just scroll down. Lmk if any problems occur with the code.

Features:

- Add, edit, and delete books

- ISBN autofill (Open Library + Google Books fallback)

- Cover image support

- Title, authors, publisher, edition, condition

- Categories and custom tags

- Format tracking (Hardcover, Paperback, eBook, Audiobook, etc.)

- Reading status (Owned, Reading, Read, Wishlist, Loaned)

- Reading progress tracking (pages read, total pages, percentage, progress bar)

- Start and finish dates

- Star rating (1–5)

- Purchase tracking (price + purchase date)

- Multi-currency support per book

- Live exchange rate conversion to base currency

- Currency provider selection + manual mode

- Total library value calculation

- Statistics dashboard (books, value, authors, categories)

- Breakdown by status and top categories

- Smart search (title, author, ISBN, notes, tags, etc.)

- Advanced filters (status, category, author, tag, format)

- Column sorting

- IndexedDB storage (handles large collections smoothly)

- JSON export and import

- CSV export

- Dark mode / light mode toggle

- Responsive design (desktop + mobile) - SYNC BETWEEN DEVICES IS NOT CURRENTLY AVAILABLE. (If you want it, instructions are below).

- Optional Firebase cloud sync (Google sign-in + Firestore) - THIS IS NOT AVAILABLE. IT IS IN THE CODE, BUT ITS NOT AVAILABLE. (If you want it, instructions are below)

- Local data wipe option

- Fully client-side (works on GitHub Pages)



-----------------------------------------------------------------

Optional Cloud Sync (Firebase) — Setup Guide

Link: https://console.firebase.google.com

Cloud sync is already implemented in this codebase, but it’s disabled by default. To enable sync on your own copy, you just need to connect your own Firebase project.

1) Create a Firebase project

Go to Firebase Console

Create a new project (any name)

2) Create a Web App + copy config

Project Settings → General → “Your apps” → Add app (Web)

Copy the Firebase config object (apiKey, authDomain, projectId, etc.)

3) Enable Google Sign-In

Firebase Console → Authentication → Get started

Sign-in method → enable Google

4) Create a Firestore database

Firebase Console → Firestore Database → Create database

Choose Production mode

5) Set Firestore security rules (required)

In Firestore → Rules, use:

rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/library_books/{bookId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}

6) Paste config into the app

Open the app → Settings → Firebase config (JSON)

Paste the config → Save

7) Sync

Go to the Cloud tab

Sign in → use Push (upload) and Pull (download) to sync across devices

-----------
Extra note for GitHub Pages users:

If you host on GitHub Pages, add your site domain in Firebase:
Authentication → Settings → Authorized domains (add YOURNAME.github.io).


