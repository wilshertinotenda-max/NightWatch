# Responsive Portfolio Website (Alexa) — Analysis & Build Journey

This file combines the repository analysis, the project guidance notes, and a
stage-by-stage record of turning the project from an empty skeleton into a
working, styled, interactive site.

---

## Part 1 — Repository Analysis

*(from `ANALYSIS.md`)*

### What the project does

This is a **static, single-page personal portfolio website template** (by the
YouTube channel/creator "Bedimcode") meant to be built up while following
along with a video tutorial ([youtu.be/27JtRAI3QO8](https://youtu.be/27JtRAI3QO8)).
It is not a framework/build-tool project — it's plain **HTML, CSS, and
JavaScript**, no package manager, no dependencies to install.

According to the README, the finished site is meant to feature:
- A responsive, mobile-first personal portfolio layout
- Smooth in-page scrolling between sections
- Light/dark theme toggle
- A CV/resume download, testimonials carousel, project showcase, and contact section

**Original caveat:** the copy that shipped on disk was a **skeleton/starter
state**, not the finished site shown in `preview.png`. `index.html`,
`assets/css/styles.css`, and `assets/js/main.js` all contained the section
headers/comments (`HOME`, `ABOUT`, `SKILLS`, `NAV`, `DARK LIGHT THEME`, etc.)
but the actual markup, CSS rules, and JS logic under most of those comments
were **empty**. The `<link>`/`<script>` tags in `index.html` also had blank
`href`/`src` attributes. This matched a common "code-along" template where the
instructor fills in each commented section live in the tutorial video.
*(See Part 3 for how this was resolved.)*

### Main structure

```
responsive-portfolio-website-Alexa-main/
├── README.md                    Project description + link to tutorial video
├── Text Portfolio Alexa.txt     Plain-text copy for all site content (bio, links, service blurbs...)
├── index.html                   Single HTML page, sectioned
├── preview.png                  Screenshot of the finished site (goal state)
└── assets/
    ├── css/
    │   ├── styles.css               Custom stylesheet (CSS vars + component rules)
    │   └── swiper-bundle.min.css    Third-party Swiper.js carousel styles (vendored)
    ├── img/                         Profile photo, about photo, blob.svg, portfolio shots, testimonial avatars
    ├── js/
    │   ├── main.js                   Custom site behavior (menu, tabs, modal, carousel init, scroll spy, theme toggle)
    │   └── swiper-bundle.min.js      Third-party Swiper.js carousel library (vendored)
    └── pdf/
        └── Alexa-Cv.pdf               Sample downloadable CV/resume
```

### Important files or directories

| Path | Why it matters |
|---|---|
| `index.html` | The whole site is one page; every section (`home`, `about`, `skills`, `qualification`, `services`, `portfolio`, `project`, `testimonial`, `contact`) lives here. |
| `assets/css/styles.css` | Defines the design system as CSS custom properties (`--hue-color`, spacing scale, font sizes, z-index scale) under `:root`. Changing `--hue-color` (Purple 250 / Green 142 / Blue 230 / Pink 340) re-themes the whole site. |
| `assets/js/main.js` | Holds all interactivity: mobile menu toggle, skills accordion, qualification tabs, services modal, Swiper init, scroll-spy nav highlighting, header background on scroll, scroll-to-top button, dark/light theme persistence. |
| `assets/js/swiper-bundle.min.js` / `assets/css/swiper-bundle.min.css` | Vendored third-party [Swiper.js](https://swiperjs.com/) library used for the portfolio and testimonial sliders. Never edited directly — configured from `main.js`. |
| `Text Portfolio Alexa.txt` | Content source of truth — placeholder copy (social links, bio text, service descriptions, stats labels) used verbatim when filling in `index.html`. |
| `assets/pdf/Alexa-Cv.pdf` | Sample CV linked from the "Download CV" button. |
| `preview.png` | Reference screenshot showing what the finished, styled site should look like. |
| `README.md` | Points to the tutorial video this template accompanies. |

### How the project is installed or used

No build tools, package manager, or server-side code are involved — it's
plain static front-end files.

1. Get the files (already at `C:\Users\wilsh\Desktop\portfolio-repo\responsive-portfolio-website-Alexa-main\`).
2. Open `index.html` directly in a browser, or serve the folder with any static
   server (VS Code "Live Server", `python -m http.server`, etc.) for correct
   relative paths and live reload.
3. Deploy anywhere that serves static files (GitHub Pages, Netlify, Vercel,
   S3, etc.) — no build step required.

---

## Part 2 — Project Guidance

*(from `md file 2.md`, the Claude Code guidance file for this repository)*

### Project overview

Static, single-page personal portfolio website (plain HTML/CSS/JS, no
framework, no build tools, no package manager). It's a code-along template
for the tutorial [youtu.be/27JtRAI3QO8](https://youtu.be/27JtRAI3QO8) by
Bedimcode.

### Commands

There is no package manager, build step, linter, or test suite in this repo —
it's served as-is.

- **Run locally:** open `index.html` directly in a browser, or serve the
  folder with any static file server so relative asset paths resolve correctly.
- **Deploy:** static hosting only — no build step required.

### Architecture

- **Single page, section-based.** All content lives in one `index.html` as
  sequential `<section>` blocks with fixed ids/classes: `home`, `about`,
  `skills`, `qualification`, `services`, `portfolio`, `project`,
  `testimonial`, `contact`, plus a fixed bottom `header` (mobile-first nav)
  and `footer`. `styles.css` and `main.js` use the same
  `<!--==== NAME ====-->` comment-marker convention to delimit the CSS/JS for
  each section — edits stay inside the matching marker block across all three
  files.
- **CSS design system via custom properties.** A single `--hue-color` HSL
  seed drives `--first-color`/`--title-color`/`--text-color`/etc. A
  `@media (min-width: 968px)` block overrides font-size variables for
  desktop — the mobile-first breakpoint pattern used project-wide.
- **Third-party carousel is vendored, not installed.** Swiper.js is used for
  the `portfolio` and `testimonial` sliders; it's initialized/configured from
  `main.js`.
- **Interactivity is centralized in `main.js`.** Comment markers map 1:1 to
  browser behaviors: mobile menu show/hide, skills accordion, qualification
  tabs, services modal, Swiper init, scroll-spy active-link highlighting,
  header background-on-scroll, scroll-to-top button visibility, and
  dark/light theme persistence via `localStorage`.
- **Content is decoupled from markup.** `Text Portfolio Alexa.txt` holds the
  copy for every section — pulled from directly rather than inventing copy.

---

## Part 3 — From Skeleton to Meaningful Site: Build Stages

This section documents exactly how the repo went from the empty skeleton
described in Parts 1–2 to a working, responsive, interactive portfolio site.

### Stage 0 — Starting point (skeleton)

- `index.html`: every `<section>` present but empty; `<link>`/`<script>` tags
  had blank `href`/`src`.
- `assets/css/styles.css`: only `:root` variables and base/reset rules
  existed; every component block (`NAV`, `HOME`, `BUTTONS`, `ABOUT`,
  `SKILLS`, `QUALIFICATION`, `SERVICES`, `PORTFOLIO`, `PROJECT IN MIND`,
  `TESTIMONIAL`, `CONTACT ME`, `FOOTER`, `SCROLL UP`, `MEDIA QUERIES`) was an
  empty comment marker.
- `assets/js/main.js`: only section-comment placeholders, zero logic.
- Result: opening `index.html` rendered a blank page.

### Stage 1 — Wire up the missing references

- Added the Unicons icon library `<link>` (used throughout the nav, buttons,
  and cards).
- Pointed the two blank `<link rel="stylesheet">` tags at
  `assets/css/swiper-bundle.min.css` and `assets/css/styles.css`.
- Pointed the two blank `<script>` tags at `assets/js/swiper-bundle.min.js`
  and `assets/js/main.js`.
- Added the missing `id="qualification"` on the qualification `<section>` so
  the nav's scroll-spy (Stage 4) has something to match against.

### Stage 2 — Build the HTML markup for every section

Filled in real markup for `header`/`nav`, `home`, `about`, `skills`,
`qualification`, `services`, `portfolio`, `project`, `testimonial`,
`contact`, `footer`, and the scroll-up button — using the exact copy from
`Text Portfolio Alexa.txt` (social links, bio text, stat labels, service
blurbs, testimonial text) and the existing media in `assets/img/` and
`assets/pdf/Alexa-Cv.pdf`. This introduced the structural hooks the CSS and
JS stages depend on: `data-target`/`data-content` for tabs, `data-modal-*`
for the services modals, `swiper-wrapper`/`swiper-slide` for the two
carousels, and the nav's `id="nav-menu"`/`id="nav-toggle"`/`id="nav-close"`.

### Stage 3 — Implement the CSS component rules

Filled in every previously-empty comment block in `styles.css`:
- Dark-theme variable overrides + theme-toggle button styling.
- Fixed mobile-first nav (bottom sheet on mobile, top bar ≥768px) with active-link and scroll-header states.
- Home hero layout (blob image, social rail, scroll-down cue).
- Reusable button variants (`--flex`, `--small`, `--white`).
- About stats grid, skills accordion (open/close via max-height + rotated arrow), qualification timeline tabs, services cards + modal overlay, portfolio/testimonial Swiper theming, project CTA banner, contact cards + floating-label form, footer, scroll-up button, and custom scrollbar.
- Responsive media queries at 350px / 568px / 768px / 1024px matching the mobile-first pattern already established by the font-size variables.

### Stage 4 — Implement the JS interactivity

Filled in every previously-empty comment block in `main.js`:
- Mobile menu show/hide (and auto-close on link click).
- Skills accordion (only one category open at a time).
- Qualification tabs (Education / Work) via `data-target`/`data-content`.
- Services modal open/close per card.
- Swiper initialization for the `portfolio` and `testimonial` sliders.
- Scroll-spy that highlights the active nav link based on scroll position.
- Header background toggle on scroll.
- Scroll-to-top button visibility toggle.
- Dark/light theme toggle with `localStorage` persistence (survives reloads).

### Stage 5 — Verification

- Confirmed HTML tag counts balance (`section`, `div`, `header`, `main`,
  `footer`, `form`, `ul` all open/close evenly) and CSS brace / JS
  bracket-paren counts balance, since no Node/npm toolchain exists in this
  repo to run a linter.
- Opened `index.html` in the default browser to visually confirm the page
  renders styled and populated end-to-end instead of blank.

### Result: skeleton → meaningful site

| | Before (Stage 0) | After (Stage 5) |
|---|---|---|
| Visual result | Blank page | Full styled, responsive one-page portfolio |
| Navigation | No nav rendered | Fixed mobile-first nav with working menu toggle, active-link highlighting, scroll-triggered background |
| Content | No markup | All sections populated from `Text Portfolio Alexa.txt` |
| Interactivity | None | Accordion, tabs, modals, two Swiper carousels, scroll-to-top, dark/light theme with persistence |
| Assets | Never linked | Swiper, Unicons, styles, and script all wired in |

### View the finished site

Open this link in your browser (no server needed, it's a local static file):

[`file:///C:/Users/wilsh/Desktop/portfolio-repo/responsive-portfolio-website-Alexa-main/index.html`](file:///C:/Users/wilsh/Desktop/portfolio-repo/responsive-portfolio-website-Alexa-main/index.html)

Or double-click `index.html` in
`C:\Users\wilsh\Desktop\portfolio-repo\responsive-portfolio-website-Alexa-main\`.
