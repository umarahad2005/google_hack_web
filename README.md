# Zimma AI: web build

This repository holds the **compiled Flutter web build** of *Zimma AI* (Flutter package name `google_hack`, version 1.0.0). It is the static output of `flutter build web`, set up to deploy on Vercel. The Dart source code is **not** in this repository.

## What the app does

The following comes from the UI text and API calls in the compiled bundle:

- Users describe what they need ("What do you need done today?"), with Roman Urdu among the language options.
- The AI recommends a service provider and shows its reasoning ("Why this provider?", AI score and score breakdown).
- Users can confirm a booking, view a booking receipt, and track the service status until it is completed, then rate it.
- Accounts support email/password sign-up and sign-in, "Continue with Google", and a guest session. Users can edit their profile (display name, preferred language).

The bundle references Gemini AI, Supabase (auth), and a separate backend API (`/api/requests`, `/api/profile`) hosted on FastAPI Cloud.

## Tech stack (as seen in the build)

- Flutter web (CanvasKit/Skwasm renderers, service worker)
- Riverpod for state management
- Supabase client for authentication
- Vercel for static hosting

## Repository contents

```
.
├── index.html, flutter.js, flutter_bootstrap.js, flutter_service_worker.js
├── main.dart.js        # compiled app
├── assets/             # fonts, shaders, asset manifests
├── canvaskit/          # Flutter web rendering engine (wasm/js)
├── icons/, favicon.png, manifest.json
├── version.json
└── vercel.json         # SPA rewrite to index.html, no-cache on index.html and the service worker
```

## Running locally

Because this is a prebuilt static site, any static file server will work from the repo root, for example:

```bash
npx serve .
# or
python -m http.server 8080
```

## Deployment

`vercel.json` has no build command and uses the repo root as the output directory. Vercel serves the files as they are and rewrites every route to `index.html`.

To change the app, rebuild it from the Flutter source project with `flutter build web` and replace these files with the contents of `build/web/`.
