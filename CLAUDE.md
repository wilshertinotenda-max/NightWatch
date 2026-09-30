# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Static, single-page personal portfolio website (plain HTML/CSS/JS, no framework, no
build tools, no package manager). It's a code-along template for the tutorial
[youtu.be/27JtRAI3QO8](https://youtu.be/27JtRAI3QO8) by Bedimcode.

**Current state:** the repo is a *skeleton*, not the finished site shown in
`preview.png`. `index.html` has all sections present but empty, its `<link>`/`<script>`
tags have blank `href`/`src` attributes (nothing is actually wired in yet), and
`assets/css/styles.css` / `assets/js/main.js` contain only section-header comments with
no rules/logic underneath. Treat any work here as filling in that skeleton unless told
otherwise.

## Commands

There is no package manager, build step, linter, or test suite in this repo — it's
served as-is.

- **Run locally:** open `index.html` directly in a browser, or serve the folder with any
  static file server (e.g. VS Code "Live Server", or `python -m http.server` from this
  directory) so relative asset paths resolve correctly.
- **Deploy:** static hosting only (GitHub Pages, Netlify, Vercel, S3, etc.) — no build
  step required.

## Architecture

- **Single page, section-based.** All content lives in one `index.html` as sequential
  `<section>` blocks with fixed ids/classes: `home`, `about`, `skills`, `qualification`,
  `services`, `portfolio`, `project`, `testimonial`, `contact`, plus a fixed bottom
  `header` (mobile-first nav) and `footer`. When adding a feature, find the matching
  section by its `<!--==== NAME ====-->` comment marker — both `styles.css` and `main.js`
  use the same comment-marker convention to delimit the CSS/JS for each section, so keep
  edits inside the matching marker block in all three files.

- **CSS design system via custom properties.** `assets/css/styles.css` defines the
  entire visual language as `:root` custom properties: a single `--hue-color` HSL seed
  drives `--first-color`/`--title-color`/`--text-color`/etc. (presets noted in a comment:
  Purple 250 / Green 142 / Blue 230 / Pink 340), plus a type scale and spacing scale
  (`--mb-*`) reused throughout. A `@media (min-width: 968px)` block overrides the
  font-size variables for desktop — this is the mobile-first breakpoint pattern used
  project-wide, not just for typography. A dark-theme variable block and toggle button
  styles are stubbed but not yet implemented (see `/*========== Variables Dark theme
  ==========*/` and `/*========== Button Dark/Light ==========*/`).

- **Third-party carousel is vendored, not installed.** `assets/js/swiper-bundle.min.js`
  and `assets/css/swiper-bundle.min.css` are the complete, unmodified Swiper.js library
  used to build the `portfolio` and `testimonial` sliders. Don't edit these files —
  initialize/configure Swiper from `main.js` instead, and remember `index.html` needs its
  `<link>`/`<script>` tags pointed at these files (and at `styles.css`/`main.js`) before
  anything will render.

- **Interactivity is centralized in `main.js`.** Its comment markers map 1:1 to browser
  behaviors the finished site needs: mobile menu show/hide, skills accordion,
  qualification tabs, services modal, Swiper init, scroll-spy active-link highlighting,
  header background-on-scroll, scroll-to-top button visibility, and dark/light theme
  persistence (implies reading/writing a theme preference, likely via
  `localStorage`/`document.body.classList`, once implemented).

- **Content is decoupled from markup.** `Text Portfolio Alexa.txt` holds the copy for
  every section (social links, bio text, stat labels, service blurbs) as a plain-text
  reference — pull from here when filling in `index.html` rather than inventing copy.
  Media referenced by the eventual markup already exists under `assets/img/` (profile,
  about photo, `blob.svg` decoration, 3 portfolio shots, 3 testimonial avatars,
  `project.png`) and `assets/pdf/Alexa-Cv.pdf` (CV download).
