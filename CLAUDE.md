# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

The static website for RuntimeLoop, an independent app studio in Dhaka, Bangladesh. It is served by GitHub Pages at `https://runtimeloopapps.github.io/` from the `runtimeloopapps/runtimeloop.github.io` repo. Pushing to the default branch deploys the site.

There is no build step, package manager, linter or test suite. Every page is hand-written HTML with inline `<style>`. To preview locally, run `python3 -m http.server 8000` from the repo root and open `http://localhost:8000/`.

## Structure

- `index.html` is the whole studio site on one page. After the hero and banner strip come `#apps`, `#about`, `#build` (category cards) and `#contact`, and each app has an `<article class="app" id="<app>">` card inside `#apps`. The only JavaScript fills in the footer year.
- `hatekhori/index.html` is a meta-refresh redirect to `../#hatekhori`. The app card on the homepage is the app's real landing page.
- `hatekhori/privacy-policy.html` is the privacy policy the Google Play listing links to (package `com.runtimeloop.hatekhori`). Its URL must not change. It is standalone, with its own inline styles and a dark-mode palette, and it has a "Last updated" date that should be bumped whenever its content changes.
- `assets/` holds shared images. `banner-web.jpg` is the Open Graph/Twitter preview image, referenced by absolute URL in the `<meta>` tags.
- `../old-backup/` (outside the repo) holds the earlier purple design. The current page reuses its layout, but not its colors.

## Conventions

- Design tokens are CSS custom properties on `:root` in each page. The studio palette (`--bg`, `--accent` blue, `--accent-2` cyan) comes from the logo and banner. Hatekhori has a warm palette of its own (`--paper`, `--marigold`, `--ink`, `--clay`, `--sand`) that is used only inside its app card and on its policy page.
- Fonts come from Google Fonts: Manrope (`--sans`) for Latin text and Hind Siliguri (`--bangla`) for Bangla. Wrap Bangla text in an element with `lang="bn"` and the Bangla font.
- To add a new app, follow the Hatekhori pattern: add an app card in `index.html`, add `<app>/index.html` as a redirect to `../#<app>`, and add `<app>/privacy-policy.html` for the Play Store listing.
- The pages already have accessibility features: `aria-labelledby` on sections, `.sr-only`, `:focus-visible` outlines and `prefers-reduced-motion` handling. New markup should keep them.
- Contact email: `runtimeloop.apps@gmail.com`.
