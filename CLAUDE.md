# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

The static website for RuntimeLoop, an independent app studio in Dhaka, Bangladesh. It is served by GitHub Pages at `https://runtimeloopapps.github.io/` from the `runtimeloopapps/runtimeloopapps.github.io` repo. Pushing to the default branch deploys the site.

There is no build step, package manager, linter or test suite. Every page is hand-written HTML with inline `<style>`. To preview locally, run `python3 -m http.server 8000` from the repo root and open `http://localhost:8000/`.

## Structure

- `index.html` is the whole studio site on one page. After the hero and banner strip come `#apps`, `#about`, `#build` (category cards) and `#contact`, and each app has an `<article class="app" id="<app>">` card inside `#apps`. The only JavaScript fills in the footer year.
- `hatekhori/index.html` is a meta-refresh redirect to `../#hatekhori`. The app card on the homepage is the app's real landing page.
- `hatekhori/privacy-policy.html` is the privacy policy the Google Play listing links to (package `com.runtimeloop.hatekhori`). Its URL must not change. It is standalone, with its own inline styles and a dark-mode palette, and it has a "Last updated" date that should be bumped whenever its content changes.
- `assets/` holds shared images. `banner-web.jpg` is the Open Graph/Twitter preview image, referenced by absolute URL in the `<meta>` tags.
- The earlier purple design was kept in an `old-backup/` folder outside the repo; it is not on this machine. The current page reuses its layout, but not its colors.

## Conventions

- Design tokens are CSS custom properties on `:root` in each page. The studio palette (`--bg`, `--accent` blue, `--accent-2` cyan) comes from the logo and banner. Hatekhori has a warm palette of its own (`--paper`, `--marigold`, `--ink`, `--clay`, `--sand`) that is used only inside its app card and on its policy page.
- Fonts come from Google Fonts: Manrope (`--sans`) for Latin text and Hind Siliguri (`--bangla`) for Bangla. Wrap Bangla text in an element with `lang="bn"` and the Bangla font.
- To add a new app, follow the Hatekhori pattern: add an app card in `index.html`, add `<app>/index.html` as a redirect to `../#<app>`, and add `<app>/privacy-policy.html` for the Play Store listing.
- The pages already have accessibility features: `aria-labelledby` on sections, `.sr-only`, `:focus-visible` outlines and `prefers-reduced-motion` handling. New markup should keep them.
- Contact email: `runtimeloop.apps@gmail.com`.

## Keep in step with the Hatekhori app

This repo is cloned beside the app at `../hatekhori/` (a separate repo; never merge the two). The Hatekhori card and `hatekhori/privacy-policy.html` state facts about the app, and Google Play's reviewers check the policy against it:

- Card: 50 Bangla letters and English A to Z, three short letter games, ages 3 to 6, works fully offline, no ads, no purchases, collects no data, the Play link (`com.runtimeloop.hatekhori`).
- Policy: no networking code and no permissions, the `<queries>` explanation, the Parent Zone links behind a parental gate, "Reset progress", what progress is stored, the contact email and package name.

If an app change (new letters, games or features, a permission or dependency, stored data, ads or purchases, age range, email) makes any of this untrue, tell the owner first and name the text affected. Then update the app and this site together, bump the policy's "Last updated" date, and keep `../hatekhori/store/privacy/index.html` identical to the live policy. Push only when the owner says so.
