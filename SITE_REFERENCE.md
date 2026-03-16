# Personal Website — Developer Reference

This document describes how the site works and which files to modify when making changes.

---

## Overview

This is a professional portfolio website built on the **Start Bootstrap Agency v5.0.7** template, customized for science writing and research communication services. It is hosted on **GitHub Pages** as a static site — no server-side build step is needed after deployment since pre-compiled assets are already included.

**Owner**: Maria Mayofis
**Analytics**: Google Analytics (UA-89857829-2) + Google Tag Manager (GTM-PRWQRQ5)

---

## Directory Structure

```
/
├── index.html                        # Main homepage (all sections)
├── portfolio-CRISPRforCF.html        # Standalone CRISPR science explainer
├── portfolio-imagejbasics.html       # Standalone ImageJ how-to guide
│
├── css/
│   ├── agency.css                    # Compiled CSS (do not edit directly)
│   └── agency.min.css                # Minified CSS (used by the site)
│
├── scss/                             # Edit these to change styles
│   ├── agency.scss                   # Root file — imports all partials
│   ├── _variables.scss               # Colors, fonts
│   ├── _mixins.scss                  # Font family definitions
│   ├── _global.scss                  # Body, links, headings, sections, buttons
│   ├── _navbar.scss                  # Navigation bar
│   ├── _masthead.scss                # Hero/header section
│   ├── _services.scss                # Services cards
│   ├── _portfolio.scss               # Portfolio grid & modals
│   ├── _timeline.scss                # Timeline (unused in current layout)
│   ├── _team.scss                    # Team cards (unused in current layout)
│   ├── _contact.scss                 # Contact form
│   └── _footer.scss                  # Footer
│
├── js/
│   ├── agency.js                     # Main JS (smooth scroll, navbar, modals)
│   ├── agency.min.js                 # Minified version (used by the site)
│   ├── contact_me.js                 # Contact form submission
│   └── jqBootstrapValidation.js      # Form validation library
│
├── mail/
│   └── contact_me.php                # Server-side email handler (needs config)
│
├── vendor/                           # Third-party dependencies (do not edit)
│   ├── bootstrap/
│   ├── jquery/
│   ├── jquery-easing/
│   └── fontawesome-free/
│
├── img/                              # Main site images
│   ├── header-bg.jpg                 # Hero section background
│   ├── masha.jpg                     # Profile photo (circular)
│   ├── map-image.png                 # Contact section background
│   └── portfolio/                    # Thumbnail images for portfolio grid
│
└── assets/                           # Portfolio content files
    ├── *.jpg / *.pdf                  # Full images and PDFs for modals
    └── portfolio/                    # Images for standalone portfolio pages
```

---

## How the Site Works

### Page Structure (index.html)

The homepage is a single-page site with five main sections, all in `index.html`:

```
<nav>              Navigation bar (fixed, shrinks on scroll)
<header>           Hero section (background image + profile photo + intro)
<section#services> Four service cards with Font Awesome icons
<section#portfolio> Grid of 6 portfolio thumbnails (click to open modal)
<footer>           Copyright + LinkedIn/GitHub links
```

After the footer, the same file contains **6 hidden `<div.portfolio-modal>` elements** — these are the popups shown when portfolio items are clicked.

### Standalone Pages

Two portfolio items link out to their own HTML pages rather than modals:
- `portfolio-imagejbasics.html` — ImageJ tutorial
- `portfolio-CRISPRforCF.html` — CRISPR explainer

These share the same CSS and JS as the main page.

### Navigation

The navbar uses **Bootstrap 4** and three custom behaviors (in `js/agency.js`):
1. **Smooth scrolling** — `.js-scroll-trigger` links animate to the target section
2. **Navbar shrink** — adds `.navbar-shrink` class when scrolled > 100px (triggers CSS transition)
3. **ScrollSpy** — highlights the active nav link based on scroll position
4. **Modal interaction** — hides navbar when a portfolio modal opens

### Styling Architecture

Styles are written in **SCSS** (in `scss/`) and compiled to `css/agency.min.css`. The site uses that minified file. If you edit SCSS files, you must recompile (see Build Process below).

### Analytics

Both Google Analytics and Google Tag Manager scripts are in the `<head>` of every HTML file. GTM also has a `<noscript>` fallback at the top of `<body>`.

---

## What to Change and Where

### Branding & Personal Information

| What | Where | Details |
|------|-------|---------|
| Name in navbar | `index.html` | Search for `Maria Mayofis` in the `<nav>` section |
| Hero intro text | `index.html` | Inside `<header class="masthead">` |
| Profile photo | `img/masha.jpg` | Replace file (keep same filename or update HTML) |
| Hero background | `img/header-bg.jpg` | Replace file |
| Footer copyright | `index.html` | In `<footer>`, near end of file |
| LinkedIn URL | `index.html` | Footer `<a>` tag with LinkedIn icon |
| GitHub URL | `index.html` | Footer `<a>` tag with GitHub icon |

### Services Section

Location: `index.html` — search for `<section class="page-section" id="services">`

Each service is a `<div class="col-md-3">` block containing:
- A Font Awesome icon (e.g., `<i class="fas fa-pen">`)
- An `<h4 class="service-heading">` title
- A `<p class="text-muted">` description

To change an icon, find the icon name at fontawesome.com and update the `fa-*` class.

### Portfolio Grid

Location: `index.html` — search for `<section class="page-section bg-light" id="portfolio">`

Each portfolio item is a `<div class="col-md-4 col-sm-6 portfolio-item">` block. Each links to a modal by ID (`#portfolioModal1` through `#portfolioModal6`), or to an external HTML page.

To add a portfolio item:
1. Add a new `<div class="col-md-4 col-sm-6 portfolio-item">` block in the grid
2. Add a corresponding modal `<div id="portfolioModal7" ...>` at the bottom of the page
3. Add thumbnail image to `img/portfolio/` and full image to `assets/`

### Portfolio Modals

Location: `index.html` — at the bottom, before `</body>`

Each modal follows this structure:
```html
<div class="portfolio-modal modal fade" id="portfolioModal1" ...>
  <div class="modal-dialog modal-xl">
    <div class="modal-content">
      <!-- Close button -->
      <!-- Title -->
      <!-- Intro text -->
      <!-- Full image -->
      <!-- Description, metadata, links -->
    </div>
  </div>
</div>
```

The metadata block contains three rows: **Disciplines**, **Methods**, and **Contributions**.

### Contact Form

The HTML form is in `index.html` (search `id="contactForm"`). The form itself works, but the **email recipient is not configured**.

To enable contact form emails:
1. Open `mail/contact_me.php`
2. Line ~19: Change `yourname@yourdomain.com` to your actual email address
3. Line ~22: Change `noreply@yourdomain.com` to a valid sender address

Note: GitHub Pages does not support PHP. The contact form requires a server that can run PHP (not currently active on this deployment).

### Colors

File: `scss/_variables.scss`

The primary accent color (golden yellow used for buttons, links, hover states) is:
```scss
$primary: #fed136;
```

Change this value and recompile CSS to update the entire color scheme at once.

### Fonts

File: `scss/_mixins.scss`

Four font families are defined:
```scss
@mixin heading-font  → Montserrat (section titles)
@mixin body-font     → Roboto Slab (body text)
@mixin serif-font    → Droid Serif (italic/quotes)
@mixin script-font   → Kaushan Script (brand name)
```

Google Fonts are loaded in the `<head>` of each HTML file. If you change fonts here, also update the Google Fonts URL in the HTML `<head>`.

### Hero Section Layout

File: `scss/_masthead.scss`

Controls hero section padding, text sizing, and background image behavior. The background image path is also set in `index.html` inline:
```html
<header class="masthead" style="background-image: url('img/header-bg.jpg')">
```

---

## Build Process (Optional — for development)

The site uses **Gulp** for development. This is only needed if you want to edit SCSS or use live-reloading during development.

```bash
npm install           # Install dependencies
npm start             # Start dev server at localhost:3000 (runs gulp watch)
```

Gulp tasks:
- `gulp css` — Compile SCSS → CSS → minify
- `gulp js` — Minify JavaScript
- `gulp vendor` — Copy node_modules to vendor/
- `gulp build` — Full rebuild
- `gulp watch` — Watch files + BrowserSync

**Important**: When editing SCSS, run `gulp css` to recompile. The site uses `css/agency.min.css`, not the SCSS source directly.

If you only need to make HTML content changes (text, links, images), no build step is needed — just edit the HTML directly and push.

---

## Deployment

The site deploys automatically via **GitHub Pages**. Pushing to the `main` branch updates the live site.

Travis CI (`.travis.yml`) runs a build check on each push but is not required for deployment.

Pre-compiled CSS and JS are committed to the repo, so GitHub Pages can serve the site without any build step.

---

## Key Libraries & Versions

| Library | Version | Used For |
|---------|---------|---------|
| Bootstrap | 4.3.1 | Layout grid, components, modals |
| jQuery | 3.3.1 | DOM manipulation, event handling |
| jQuery Easing | 1.4.1 | Smooth scroll animation |
| Font Awesome | 5.8.1 | Icons throughout the site |
| Gulp | 4.0.0 | Build automation (dev only) |

---

## Quick Reference: Common Changes

| Task | File(s) | Notes |
|------|---------|-------|
| Change intro text | `index.html` | Inside `<header class="masthead">` |
| Update profile photo | `img/masha.jpg` | Replace file |
| Add/edit a service | `index.html` | In `#services` section |
| Add portfolio item | `index.html` | Grid item + modal at bottom |
| Edit portfolio details | `index.html` | In the relevant `#portfolioModal*` div |
| Edit CRISPR page | `portfolio-CRISPRforCF.html` | Standalone file |
| Edit ImageJ page | `portfolio-imagejbasics.html` | Standalone file |
| Change accent color | `scss/_variables.scss` | `$primary`, then recompile |
| Change section padding | `scss/_global.scss` | `.page-section` rule |
| Change navbar behavior | `js/agency.js` | Scroll distance, animation duration |
| Update analytics ID | `index.html` (head) | All 3 HTML files need updating |
