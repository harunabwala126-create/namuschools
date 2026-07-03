# NMPS Portal — Deployment

This is a single self-contained `index.html` file — no build step, no dependencies to install.
It works as-is on both GitHub Pages and Vercel.

## Deploy to GitHub Pages

1. Create a new repo on GitHub (e.g. `nmps-portal`).
2. Upload `index.html` to the **root** of the repo (must be named exactly `index.html`).
3. Go to **Settings → Pages**.
4. Under "Build and deployment", set **Source** to `Deploy from a branch`.
5. Set **Branch** to `main` and folder to `/ (root)`, then **Save**.
6. Wait ~1 minute — your site will be live at:
   `https://YOUR_USERNAME.github.io/nmps-portal/`

To push updates later: just replace `index.html` in the repo (upload again, or `git push`) — GitHub Pages redeploys automatically within a minute or two.

## Deploy to Vercel

**Option A — no account needed for a quick test:**
Drag-and-drop won't work on Vercel directly (that's Netlify), so use Option B.

**Option B — proper deploy (recommended):**
1. Push `index.html` (and `vercel.json`, included here) to a GitHub repo.
2. Go to [vercel.com](https://vercel.com) → **Add New → Project**.
3. Import the GitHub repo.
4. Leave all build settings as default (no framework, no build command needed — Vercel auto-detects it as static).
5. Click **Deploy**. You'll get a live `https://your-project.vercel.app` URL immediately.

To push updates later: just `git push` to the repo — Vercel redeploys automatically.

## Notes

- Both platforms serve over `https://`, which fixes the local-storage reliability issues you'd get from opening the file directly (`file://`).
- If you deploy to **both** GitHub Pages and Vercel, note they're separate domains — each will have its own independent browser storage. Data entered on one won't automatically appear on the other unless you set up the Firebase Firestore sync already built into the file (see the `FIREBASE_CONFIG` comment block near the top of the `<script>` section).
- The app has no server-side code and needs none — everything (grading, PIN auth, pupil records) runs client-side and saves to the browser's local storage, or to Firestore if you configure it.
