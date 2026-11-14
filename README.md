# Beat Cooker — website

Landing page and legal pages for the Beat Cooker app, hosted on **Firebase Hosting**
(project `beat-cooker`, https://beat-cooker.web.app).

```
public/            # everything that gets deployed
  index.html       # landing page
  privacy.html     # served at /privacy
  terms.html       # served at /terms
  404.html
  assets/          # site.css, site.js, logo and social images
firebase.json      # hosting config (clean URLs, headers, caching)
.firebaserc        # Firebase project ID
```

## Local preview

```bash
npm i -g firebase-tools
firebase emulators:start --only hosting --project demo-beat-cooker
# → http://127.0.0.1:5000
```

## Deploy

Manual:

```bash
firebase login
firebase deploy --only hosting --project beat-cooker
```

Automatic (GitHub Actions):

- `.github/workflows/firebase-hosting-merge.yml` deploys to the live channel on every push to `main`.
- `.github/workflows/firebase-hosting-pull-request.yml` deploys a 7-day preview channel for each PR and comments the URL.

Both need a repository secret named `FIREBASE_SERVICE_ACCOUNT` containing a service-account JSON key
for the `beat-cooker` project. The service account needs these roles: Firebase Hosting Admin,
Firebase Authentication Admin, Cloud Run Viewer, API Keys Viewer and Service Usage Consumer
(without the last one the deploy fails with 403).

## GitHub Pages transition

The root-level `index.html`, `privacy.html` and `terms.html` are redirect stubs that send visitors of
the old GitHub Pages addresses to the Firebase site. Once the App Store listing and the released app
point to the new URLs, GitHub Pages can be disabled and these root files deleted.
