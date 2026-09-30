# Repository Analysis — Responsive Portfolio Website (Alexa)

## What the project does

This is a **static, single-page personal portfolio website template** (by the YouTube
channel/creator "Bedimcode") meant to be built up while following along with a video
tutorial ([youtu.be/27JtRAI3QO8](https://youtu.be/27JtRAI3QO8)). It is not a
framework/build-tool project — it's plain **HTML, CSS, and JavaScript**, no package
manager, no dependencies to install.

According to the README, the finished site is meant to feature:
- A responsive, mobile-first personal portfolio layout
- Smooth in-page scrolling between sections
- Light/dark theme toggle
- A CV/resume download, testimonials carousel, project showcase, and contact section

**Important caveat:** the copy currently on disk is a **skeleton/starter state**, not the
finished site shown in `preview.png`. `index.html`, `assets/css/styles.css`, and
`assets/js/main.js` all contain the section headers/comments (`HOME`, `ABOUT`, `SKILLS`,
`NAV`, `DARK LIGHT THEME`, etc.) but the actual markup, CSS rules, and JS logic under most
of those comments are **empty**. The `<link>`/`<script>` tags in `index.html` also have
blank `href`/`src` attributes (the Swiper and local CSS/JS files are never actually
wired in). This matches a common "code-along" template where the instructor fills in each
commented section live in the tutorial video.

## Main structure

```
responsive-portfolio-website-Alexa-main/
├── README.md                    Project description + link to tutorial video
├── Text Portfolio Alexa.txt     Plain-text copy for all site content (bio, links, service blurbs...)
├── index.html                   Single HTML page, sectioned but mostly empty markup
├── preview.png                  Screenshot of the finished site (goal state)
└── assets/
    ├── css/
    │   ├── styles.css               Custom stylesheet (CSS vars + reusable classes defined; component rules empty)
    │   └── swiper-bundle.min.css    Third-party Swiper.js carousel styles (vendored, complete)
    ├── img/                         Profile photo, about photo, blob.svg decoration, 3 portfolio shots, 3 testimonial avatars, project.png
    ├── js/
    │   ├── main.js                   Custom site behavior (menu, tabs, modal, carousel init, scroll spy, theme toggle) — all sections empty/unimplemented
    │   └── swiper-bundle.min.js      Third-party Swiper.js carousel library (vendored, complete)
    └── pdf/
        └── Alexa-Cv.pdf               Sample downloadable CV/resume
```

## Important files or directories

| Path | Why it matters |
|---|---|
| `index.html` | The whole site is one page; every section (`home`, `about`, `skills`, `qualification`, `services`, `portfolio`, `project`, `testimonial`, `contact`) lives here as an empty `<section>` waiting for markup. |
| `assets/css/styles.css` | Defines the design system as CSS custom properties (`--hue-color`, spacing scale, font sizes, z-index scale) under `:root`. Changing `--hue-color` (line 10) is the documented way to re-theme the whole site (Purple/Green/Blue/Pink presets are given in a comment). Component-level rules (nav, buttons, cards, dark theme, media queries) are stubbed but not written. |
| `assets/js/main.js` | Intended to hold all interactivity: mobile menu toggle, skills accordion, qualification tabs, services modal, Swiper init for the portfolio/testimonial carousels, scroll-spy nav highlighting, header background on scroll, scroll-to-top button, and dark/light theme persistence. Currently just section-comment placeholders — no logic implemented yet. |
| `assets/js/swiper-bundle.min.js` / `assets/css/swiper-bundle.min.css` | Vendored third-party [Swiper.js](https://swiperjs.com/) library used for the portfolio and testimonial sliders. These are complete/functional as-is; `index.html` just needs its empty `<script>`/`<link>` tags pointed at them. |
| `Text Portfolio Alexa.txt` | Content source of truth — all placeholder copy (social links, bio text, service descriptions, stats labels) to paste into `index.html`. |
| `assets/pdf/Alexa-Cv.pdf` | Sample CV meant to be linked from the "download CV" button. |
| `preview.png` | Reference screenshot showing what the finished, styled site should look like. |
| `README.md` | Points to the tutorial video this template accompanies. |

## How the project can be installed or used

No build tools, package manager, or server-side code are involved — it's plain static
front-end files.

1. **Get the files** — already extracted to:
   `C:\Users\wilsh\Desktop\portfolio-repo\responsive-portfolio-website-Alexa-main\`
2. **Open it locally** — simplest option: double-click `index.html` to open it in a
   browser, or serve the folder with any static server (e.g. VS Code's "Live Server"
   extension, or `python -m http.server` from inside the folder) for proper relative
   paths and live reload.
3. **Wire up the empty references** — right now `index.html`'s `<link rel="stylesheet" href="">`
   and `<script src="">` tags are blank and need to point to:
   - `assets/css/swiper-bundle.min.css` and `assets/css/styles.css`
   - `assets/js/swiper-bundle.min.js` and `assets/js/main.js`
4. **Fill in the markup/CSS/JS** — follow the linked YouTube tutorial (or write your own)
   to flesh out each commented section in `index.html`, `styles.css`, and `main.js`, using
   `Text Portfolio Alexa.txt` for copy and the files in `assets/img/` and `assets/pdf/`
   for media.
5. **Customize** — swap `--hue-color` in `styles.css` to re-theme, replace the images in
   `assets/img/`, replace `Alexa-Cv.pdf`, and update the social links from
   `Text Portfolio Alexa.txt`.
6. **Deploy** — since it's static, it can be hosted anywhere that serves static files
   (GitHub Pages, Netlify, Vercel, S3, etc.) with no build step required.
