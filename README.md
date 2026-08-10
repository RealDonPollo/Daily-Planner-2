# Daily Planner — PWA

A single-page daily to-do planner. No backend, no build step, no dependencies.
Data lives in the browser's `localStorage` on each device.

## Deploy to GitHub Pages

1. Create a new **public** repo, e.g. `daily-planner`.
2. Upload every file in this folder to the repo root (drag-and-drop works in the GitHub web UI):
   - `index.html`
   - `manifest.webmanifest`
   - `sw.js`
   - `icon-192.png`, `icon-512.png`, `icon-maskable-512.png`, `apple-touch-icon.png`
3. Repo → **Settings** → **Pages** → Source: *Deploy from a branch* → Branch: `main`, folder: `/ (root)` → Save.
4. Wait ~1 minute. The site appears at `https://<your-username>.github.io/daily-planner/`.

HTTPS is required for the service worker, and GitHub Pages gives you that automatically.

## Install on your phone

- **Android / Chrome**: open the URL → menu (⋮) → *Add to Home screen* / *Install app*.
- **iPhone / Safari**: open the URL → Share button → *Add to Home Screen*.
  (On iOS this only works from Safari, not Chrome.)
- **Windows / Chrome or Edge**: open the URL → install icon in the address bar.

Once installed it launches full-screen with its own icon and works offline.

## Updating the app

1. Edit `index.html` and push the change.
2. Bump the cache name in `sw.js` (`planner-v1` → `planner-v2`) and push that too.
3. Close and reopen the installed app. The old cache is deleted and the new version loads.

Without step 2 the service worker may keep serving the old file from cache.

## Your data

- Stored per device, per browser. The phone and the PC keep **separate** lists.
- **Settings → Export backup** writes a JSON file with every day, your recurring
  tasks and your colour labels.
- **Settings → Import backup** merges a backup back in: new days are added, existing
  days keep what they have and gain anything missing (tasks matched on text + time slot),
  notes are appended rather than overwritten.
- Clearing browsing data / site data in the browser will delete the planner's data too.
  Export occasionally if that would hurt.

## File map

| File | Purpose |
|---|---|
| `index.html` | The whole app — markup, styles, logic |
| `manifest.webmanifest` | Name, icons, colours; makes it installable |
| `sw.js` | Service worker; caches the app for offline use |
| `icon-*.png` | App icons (`maskable` is the one Android crops into its icon shape) |
