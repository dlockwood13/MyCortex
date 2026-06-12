# Cortex

A swipe feed for postgraduate psychology, built from the Bella's Brain pattern and retuned for Masters (Level 7) and PhD (Level 8) study. It covers the forty subdisciplines on the standard psychology/neuroscience map as typed concept cards: theory, key study, debate, method, frontier. Each card carries a level tag (L7 taught mastery, L8 research frontier), a self-check that tests reasoning rather than recall, and the app tracks what you have seen, understood and saved.

It is a single-file app (React via CDN, transformed in the browser by Babel) and works as an installable PWA. Progress is stored on the device.

## What is different from a GCSE feed

A swipe-and-recall feed works at GCSE because the content is shallow and factual. Postgraduate psychology is competing theories, methodological trade-offs and live debates, so the cards are written to provoke critical comparison, not memorisation, and the self-checks ask you to reason. The app also includes a **Research proposal** scaffold, the artefact that actually separates taught study from a doctorate: working title, problem statement, research question, aims and objectives, literature gap, theoretical framework, methodology, ethics and reflexivity, and a feasibility timeline. It saves on the device and exports to text.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The whole app (content and logic inlined) |
| `manifest.webmanifest` | Makes it installable (name, icon, fullscreen) |
| `sw.js` | Service worker, offline use after the first visit |
| `icon-192.png`, `icon-512.png`, `icon-512-maskable.png` | App icons |
| `apple-touch-icon.png`, `favicon.png` | iOS / browser icons |
| `.nojekyll` | Tells GitHub Pages to serve files as-is |

## Deploy to GitHub Pages

### Option A, upload in the browser

1. Create a new repository, e.g. `cortex`.
2. **Add file -> Upload files**, drag in every file in this folder (including the hidden `.nojekyll`), and commit.
3. **Settings -> Pages**. Source: Deploy from a branch, branch **main**, folder **/ (root)**. Save.
4. Wait a minute, then open `https://dlockwood13.github.io/cortex/`.

### Option B, command line

```bash
cd path/to/this/folder
git init
git add -A
git commit -m "Cortex"
git branch -M main
git remote add origin https://github.com/dlockwood13/cortex.git
git push -u origin main
```

Then enable Pages as in step 3 above.

## Install on a phone

- **iPhone (Safari):** open the Pages URL, tap Share, then Add to Home Screen.
- **Android (Chrome):** open the URL, tap the menu, then Install app.

## Updating later

Edit `index.html`, re-upload it, and bump the `CACHE` version near the top of `sw.js` (e.g. `cortex-v2`) so phones pick up the new version instead of the cached one. The content lives in the `window.CORTEX_DATA` block near the top of `index.html`; add cards to any discipline's `cards` array and quiz items to its `quiz` array using the same shape.

## Extending the content

Each card is `{ type, level, title, body }` where `type` is one of `theory | study | debate | method | frontier` and `level` is `7` or `8`. Each quiz item is `{ q, a: [...], correct, why }`. The forty disciplines and six domains are defined at the top of the data block. Nothing else needs changing to add content.

## Notes

- Progress (understood, saved, quiz history, proposal draft) is stored in the browser on each device. Use **Export progress** on the You tab to back it up.
- Offline works after the first online visit, once the service worker has cached the app and its libraries.
- Content is original summary written for study; it is a primer and revision aid, not a substitute for primary sources. Check seminal studies and current debates against the literature before citing them.
