# Retiring khadimhssn.github.io/makermargin/

This repository served the paid MakerMargin v1 app on GitHub Pages
(`https://khadimhssn.github.io/makermargin/`). The app now lives on kitlyapps.com.
Buyers open it at <https://kitlyapps.com/access>.

Buyer data stays in the browser on the `khadimhssn.github.io` origin. It cannot
move to kitlyapps.com by itself, so this address has to stay up as a rescue page,
not a 404.

GitHub Pages publishes branch `main`, folder `/`. There is no `gh-pages` branch
and no `pages-retirement/` directory. The files that used to be the app lived at
the repository root.

## What this branch serves

- `index.html` — “MakerMargin has moved”, with **Download your backup**. No app code.
- `sw.js` — same path the old page registered (`navigator.serviceWorker.register("sw.js")`). On activate it deletes Cache Storage entries whose names start with `makermargin` (the old cache was `makermargin-v1`) and unregisters itself.
- `README.md` — these steps.

Removed from this branch: the v1 app bundle, `manifest.webmanifest`, and `icons/`
(`apple-touch-icon.png`, `icon-192.png`, `icon-512.png`, `maskable-512.png`).

The backup button reads `localStorage` key `rasoolistore.makermargin.v1`. That is
the only key the removed app used. The obfuscated bundle built it as `rasoolis` +
`tore.mak` + `ermargin` + `.v1`, then called `localStorage.getItem` / `setItem`
with that string and `JSON.stringify` of the whole state. The page does not delete
that data.

The old service worker was network-first, so a returning visitor who is online
gets this page on the next visit. `sw.js` stays at the same URL so a browser that
updates the installed worker picks up the copy that clears the offline cache and
unregisters itself.

## Order of steps

1. **kitlyapps.com first.** In Admin, make sure the MakerMargin product exists (slug e.g. `makermargin`), mapped to Etsy listing 4599434653. Upload `MakerMargin-Online-KitlyApps.html` as the online app HTML, the buyer ZIP as the download, and `MakerMargin-Demo.html` as the Demo HTML. Use Admin › Open app to test.
2. **Swap the Pages files** (this pull request, into `main`). Merge it. Do not change the repository visibility or the Pages settings as part of the merge.
3. **Replace the buyer ZIP on Etsy** (listing 4599434653) with the KitlyApps ZIP. Its Start Here PDF should point to kitlyapps.com/access instead of github.io.
4. **About 30 days after the merge**, make the repo private (Settings › General › Danger zone › Change visibility) or delete it. That also turns Pages off. While the repo is public, the v1 source stays downloadable from git history, so do not skip this.
5. The same leak pattern exists on other public Pages repos (everafter, focuspilot, plated, rentwise all returned 200 when this was written). Check each one the same way.
