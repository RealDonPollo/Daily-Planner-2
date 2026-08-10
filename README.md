# Daily Planner

A daily to-do planner that installs on your phone and PC like a real app.
Day-by-day lists with a calendar, colour categories, recurring tasks, per-day
notes and a weekly review.

No build step, no dependencies, no backend. One HTML file, a manifest and a
service worker.

---

## 1. Put it on GitHub

**Option A — push from your machine** (this folder is already a git repo with one commit):

```bash
# create an empty repo on github.com first, then:
git remote add origin https://github.com/<your-username>/daily-planner.git
git branch -M main
git push -u origin main
```

**Option B — no git** : create a new repo on github.com, click *uploading an existing file*,
and drag in everything from this folder (including the `.github` folder and `.nojekyll`).

The repo must be **public** for GitHub Pages on a free account.

## 2. Turn on Pages

Repo → **Settings** → **Pages** → **Source: GitHub Actions**.

The included workflow (`.github/workflows/pages.yml`) then deploys on every push to `main`.
First run takes about a minute; the URL appears at the top of the Pages settings page:

```
https://<your-username>.github.io/daily-planner/
```

## 3. Install it

| Device | How |
|---|---|
| Android (Chrome) | Open the URL → ⋮ menu → **Install app** |
| iPhone (Safari) | Open the URL → Share → **Add to Home Screen** (Safari only, not Chrome) |
| Windows / macOS (Chrome, Edge) | Open the URL → install icon in the address bar |

It then launches full-screen with its own icon and works offline.

---

## Using it

| Thing | Where |
|---|---|
| Add a task | Type, pick a colour and time slot, press Enter |
| Complete / delete | Checkbox on the left, `×` on the right |
| Priority | The ⚑ flag — sorts the task to the top of its slot |
| Move between days | `‹` `›` arrows, the week strip, or ☰ for a full month |
| Carry work forward | **Pull unfinished** — moves yesterday's open tasks to the day you're on |
| Repeating tasks | **↻ Recurring** — pick weekdays; they appear automatically |
| Name your colours | **⚙ Settings → Colour labels** (e.g. blue = Work, red = School) |
| See how the week went | **Weekly review** — per-day and per-category completion |

Tasks pulled forward get a `carried N×` badge. Anything carried twice or more
shows up in the weekly review under *Carried over repeatedly* — those are the
ones to either schedule properly or drop.

## Your data

Stored in the browser's `localStorage`, **on each device separately**. Your phone
and your PC keep independent lists.

- **Settings → Export backup** writes a JSON file containing every day, your
  recurring tasks and your colour labels.
- **Settings → Import backup** merges a file back in. New days are added; existing
  days keep what they have and gain anything missing (tasks matched on text +
  time slot); notes are appended, never overwritten. Importing the same file
  twice is safe.

Use export/import to move data between devices, or to bring data over from the
Claude-hosted version of this app.

Clearing site data in your browser deletes the planner's data too. Export
occasionally if that would hurt.

## Updating the app

1. Edit `index.html`, commit, push. The workflow redeploys automatically.
2. **Bump the cache name in `sw.js`** — `planner-v1` → `planner-v2`.
3. Close and reopen the installed app.

Step 2 is the one people forget. Without it the service worker may keep serving
the previously cached file and your change won't show up.

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire app — markup, styles, logic |
| `manifest.webmanifest` | Name, icons, colours; makes it installable |
| `sw.js` | Service worker; caches the app for offline use |
| `icon-*.png` | App icons (`maskable` is the one Android crops to its icon shape) |
| `.nojekyll` | Stops GitHub Pages running Jekyll over the files |
| `.github/workflows/pages.yml` | Deploys to Pages on every push to `main` |

## Licence

MIT — see [LICENSE](LICENSE).
