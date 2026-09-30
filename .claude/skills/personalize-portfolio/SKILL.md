---
name: personalize-portfolio
description: Replace the "Alexa" placeholder content in this portfolio site with the owner's real details — name, role, bio, stats, skills, education/work history, services, projects, testimonials, contact info, social links, CV, photos and theme colour. Use when the user asks to personalize, customize, make the portfolio theirs, swap out Alexa, or update any personal detail on the site.
---

# Personalize the portfolio

This is a finished, static one-page site (plain HTML/CSS/JS, no build step) built from
the Bedimcode "Alexa" template. Every piece of personal content is still the template's
placeholder. This skill turns it into the owner's own site without breaking the layout
or the JavaScript.

## 1. Gather details before editing

Ask the user for their details, grouped by section, in **one** message. Accept partial
answers. For anything they skip, either leave the placeholder or remove that item — ask
which they prefer rather than inventing content. **Never invent** stats, employers,
dates, testimonials or client names.

| Section | What to ask for |
|---|---|
| Identity | Full name, display name for logo/footer, job title (e.g. "Frontend Developer") |
| Home | One-line description, LinkedIn / Dribbble / GitHub URLs (or which to drop) |
| About | Short bio, 3 stats (years of experience, completed projects, companies worked) |
| Skills | 2 skill groups with title + "More than N years", each skill with a % level |
| Qualification | Education entries and Work entries: title, subtitle (school/company), year range |
| Services | Up to 3 services: title, modal description, bullet points |
| Portfolio | Up to 3 projects: title, description, demo/live URL, screenshot |
| Project CTA | Keep or change "Do you have a project in mind?" banner text |
| Testimonials | Real quotes with name and photo, or remove the section |
| Contact | Phone, email, WhatsApp number (or which to drop), form handling (see §4) |
| Footer | Facebook / Instagram / Twitter(X) URLs (or which to drop) |
| Files | Profile photo, about photo, CV PDF, project screenshots |
| Theme | Accent colour: Purple 250, Green 142, Blue 230, Pink 340, or any HSL hue 0–360 |

## 2. Where each thing lives

All content is in `index.html`. Find sections by their `<!--==== NAME ====-->` comment
markers; `assets/css/styles.css` and `assets/js/main.js` use the same markers.

- **Name** appears in several places — search for `Alexa` and replace every hit:
  `<title>`, `.nav__logo`, `.home__title` ("Hi, I'm …"), image `alt` text,
  `.footer__title`, `.footer__copy`, the CV `href`, and the email address.
- **Job title:** `.home__subtitle`.
- **About stats:** the `.about__title` numbers (`3+`, `32`, `12+`) with
  `.about__subtitle` labels.
- **Skill levels live in two places.** The visible `%` is `.skills__number` in
  `index.html`, but the bar width is a class in `styles.css` (around line 532):
  `.skills__html { width: 90%; }` etc. Update both so the number and the bar match.
  When adding a skill, add a new `skills__<name>` class with its width; when removing
  one, delete its `.skills__data` block and its CSS class.
- **Qualification:** `.qualification__data` blocks inside the two
  `[data-content]` panels (education, then work). The timeline uses alternating
  left/right layout with empty `<div></div>` spacers — copy an existing block's shape
  exactly when adding or removing entries so the rounder/line alignment stays correct.
- **Services modals are matched by position, not id.** `main.js` pairs the Nth
  `.services__button` with the Nth `.services__modal`. The `data-target`/`data-modal-*`
  attributes are not what drives it. Keep each button and its modal inside the same
  `.services__content` card, and add or remove whole cards together.
- **Portfolio slides:** each `.portfolio__content.swiper-slide`. Point the "Demo"
  button `href="#"` at the real URL and add `target="_blank"`.
- **Testimonials:** each `.testimonial__content.swiper-slide`. If the user has no
  real testimonials, remove the whole `<section class="testimonial section">` rather
  than keeping fake ones — and tell them you did.
- **Contact cards:** keep the display text and the link in sync: `tel:` with the
  phone number, `mailto:` with the email, `https://wa.me/<digits only, with country code>`.
- **Social links:** home (`.home__social-icon`, LinkedIn/Dribbble/GitHub) and footer
  (`.footer__social-link`, Facebook/Instagram/Twitter). To swap a platform, change both
  the URL and the Unicons icon class (e.g. `uil-dribbble` → `uil-behance`); icon names
  are at iconscout.com/unicons.
- **Theme colour:** `--hue-color` on line 10 of `styles.css`. That single number
  re-themes the whole site, light and dark mode alike.

## 3. Swapping files

- Put new images in `assets/img/`. Easiest is to overwrite the existing file names
  (`perfil.png`, `about.jpg`, `portfolio1-3.jpg`, `testimonial1-3.jpg`) so no HTML
  changes are needed. If the user's files have different names or formats, update the
  matching `src` instead.
- `perfil.png` sits inside the SVG blob mask on the home screen: a portrait with a
  transparent or plain background works best. Mention this if they supply a busy photo.
- Put the CV at `assets/pdf/<Name>-Cv.pdf`, update the `download href` on the
  "Download CV" button, and delete `Alexa-Cv.pdf` only once the user confirms.
- Don't touch `swiper-bundle.min.js` / `swiper-bundle.min.css` (vendored library).

## 4. Contact form

The form has `action=""`, so it currently sends nothing. Tell the user, and offer a
no-backend option such as Formspree (`action="https://formspree.io/f/<id>"`
`method="POST"`) or Netlify Forms (`data-netlify="true"` if they host on Netlify).
Don't add a service without their go-ahead; they need their own account/ID.

## 5. Also update

- `Text Portfolio Alexa.txt` is the template's copy source. Either update it to the
  user's text or leave it alone and say so. Don't treat it as the source of truth once
  personal content has been written into `index.html`.
- `README.md`: offer to rewrite it for the user's own site (name, live URL, credit
  to the Bedimcode tutorial).

## 6. Verify before finishing

1. Search `index.html` for `Alexa`, `alexa@email.com`, `1234567890`, `Company Inc.`,
   `Valeria`, `Marco`, `Liam`, and the bare social root URLs (`https://github.com/"`).
   Report anything left over that the user didn't choose to keep.
2. Check that every `.skills__number` % matches its CSS width class.
3. Check that the count of `.services__button` equals the count of `.services__modal`.
4. Make sure every `src`/`href` pointing into `assets/` refers to a file that exists.
5. Open `index.html` in the browser (`start index.html` on Windows) and ask the user to
   check the menu, skills accordion, qualification tabs, service modals, both
   carousels and the dark/light toggle.
6. Summarize what changed and list any placeholders still in the site.
