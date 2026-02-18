# Dr. SS. Magagula – Practice Website

A clean, premium single-page website for a private GP practice based in Colesberg, Northern Cape. Built to be fast, mobile-friendly, and easy to hand off to anyone who needs to update it.

---

## What's in the box

Everything lives in one HTML file — `index.html`. There's no build step, no package manager, no framework to install. You open the file in a browser and it works. The only external dependencies are two font families and the icon library, both loaded from CDNs.

```
project/
├── index.html        ← the entire site
├── README.md         ← you're reading it
└── img/
    └── Doc img.png   ← doctor's photo (you supply this)
```

---

## Tech used

### HTML5
Plain, semantic HTML. Sections are labelled properly (`<header>`, `<section>`, `<footer>`) which helps with accessibility and makes the code readable at a glance. No templating engine, no JSX — just markup.

### CSS Custom Properties (variables)
All the colours are defined once at the top of the stylesheet inside `:root { }`. So if the client ever wants to tweak the rose or blue tones, you change one line and it updates everywhere. The three brand colours are:

| Name | Value | Role |
|------|-------|------|
| Rose | `#923f5b` | Primary brand — buttons, headings, accents |
| Blue | `#568bc8` | Secondary — service icons, hover states |
| Slate | `#899dbe` | Supporting — borders, muted text, subtle fills |

### CSS Grid & Flexbox
Layout is handled entirely with modern CSS — no Bootstrap, no column classes. Grid is used for the two-column hero, the services cards, and the contact section. Flexbox handles the nav bar, badge rows, and anything that needs simple horizontal alignment. Both collapse gracefully on smaller screens using `@media` breakpoints.

### Playfair Display (font)
Loaded from Google Fonts. A classic serif with personality — used for the doctor's name, section titles, and card headings. It gives the site a credible, professional feel without looking corporate or cold.

### DM Sans (font)
Also from Google Fonts. A clean, modern sans-serif used for all body text, buttons, labels, and the nav. It pairs well with Playfair Display — one adds character, the other stays out of the way.

### Lucide Icons
A lightweight, open-source icon library loaded from a CDN. It renders crisp SVG icons at any size. The library is loaded at the bottom of the `<body>` tag (not the `<head>`) so the icons only initialise after the HTML has finished loading — this prevents the "feather is not defined" type errors that happen when scripts run before the DOM is ready.

Usage is simple: you add `<i data-lucide="icon-name"></i>` anywhere in the HTML, and `lucide.createIcons()` in the script swaps it for the actual SVG.

### CSS Backdrop Filter (glassmorphism)
Used on the header, the hours card, and the contact modal. `backdrop-filter: blur()` makes the background behind an element go blurry when you open an overlay — the effect that makes the hours panel feel like it's floating over the page. It's supported in all modern browsers. The header uses it too, so as you scroll down the content behind the nav looks frosted rather than just hidden.

### CSS Animations
Two types are used:

- **Floating stat cards** on the hero image gently bob up and down on a 6-second loop using `@keyframes`. They're offset by 3 seconds so they don't move in sync, which looks more natural.
- **Overlay cards** (hours and contact modal) scale from 93% to 100% when they open, using a spring-style cubic bezier curve (`cubic-bezier(0.34, 1.56, 0.64, 1)`) that gives a slight overshoot — a subtle bounce that feels premium without being distracting.

### Vanilla JavaScript
Kept as minimal as possible. The JS only does four things:

1. Calls `lucide.createIcons()` to render the icons
2. Opens and closes the hours overlay
3. Opens and closes the contact modal
4. Builds the WhatsApp deep-link URL and opens it in a new tab

No frameworks, no libraries. The Escape key closes any open overlay, and clicking the dark background behind a card also closes it — both standard UX expectations covered.

### Responsive Design (mobile-first approach)
The site is designed to work on phones first. The hero switches from a two-column layout to a stacked single column on screens narrower than 768px. The image moves above the text on mobile. Font sizes use `clamp()` so they scale fluidly between small and large screens without needing a breakpoint for every size. Padding also uses `clamp()` so the site never feels cramped on a phone or uncomfortably wide on a large monitor.

---

## How to update common things

**Change a phone number or email** — search for the old value in `index.html` and replace it. It appears in the contact card, the modal, and the footer.

**Update practice hours** — find the `hoursOverlay` section in the HTML and edit the `.hours-row` entries.

**Swap the doctor's photo** — replace the file at `img/Doc img.png`. Keep the same filename, or update the `src` attribute on the `<img>` tag in the hero section.

**Add a Google Map** — replace the `.map-box` div with a standard Google Maps embed `<iframe>`. The embed code is available from Google Maps by clicking Share → Embed a map.

**Change the WhatsApp number** — find `wa.me/27517530000` in the script block and update the number. Format is country code + number, no spaces or plus sign.

---

## No build required

Drop the `index.html` file and the `img/` folder onto any web host — shared hosting, Netlify, GitHub Pages, Vercel, wherever — and it's live. No Node, no npm, no compilation.
