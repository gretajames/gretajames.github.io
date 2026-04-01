# Build Process — Greta James Website

A plain-English reference for understanding how this site is built and how to maintain it. No coding experience required to read this — it explains the decisions behind the code and how to make common changes.

---

## What we are building

Two connected websites, both living in the same folder:

| Site | Address | Purpose |
|---|---|---|
| Hub page | `gretajames.ca` | Personal landing page — introduces Greta and routes visitors to her projects |
| Consulting site | `gretajames.ca/beyondsurveys` | Full Beyond Surveys Consulting site — five pages |

There is also a stub (placeholder) page planned at `gretajames.ca/grantersacademy` for the Granter's Academy project.

---

## Technology choices

**Plain HTML, CSS, and JavaScript — no framework.**

This site is built with the three fundamental languages of the web, without any additional tools, libraries, or build processes. This is a deliberate choice for several reasons:

- You can open any file in a text editor and read it directly
- There is nothing to install, update, or break
- GitHub Pages (where the site is hosted) can serve plain HTML files without any configuration
- The site will still work exactly as built in ten years, with no maintenance required

**What this means practically:** Every page is a single `.html` file. The visual styling (colours, fonts, layout) lives inside `<style>` tags in the `<head>` of each file. Any interactive behaviour (like the mobile notebook drawer) lives inside `<script>` tags at the bottom of each file.

---

## How the site is hosted

The site files live in a GitHub repository (`gretajames.github.io`). GitHub Pages reads those files and serves them as a live website — automatically, for free. When a custom domain (`gretajames.ca`) is purchased and pointed to GitHub Pages, visitors to `gretajames.ca` will see the `index.html` file at the root of the repository.

**Important:** GitHub Pages runs on a Linux server, which is case-sensitive. This means `assets/Professional head shot.jpg` and `assets/professional head shot.jpg` are treated as different files. All file paths in the HTML use the exact same capitalisation as the actual files.

---

## File structure

```
Consulting Website/
├── index.html                     ← gretajames.ca hub/About page  [BUILT]
├── assets/
│   ├── Professional head shot.jpg ← Greta's headshot
│   └── Community Needs Dashboard.jpg
├── grantersacademy/
│   └── index.html                 ← Coming soon stub page  [TO BUILD]
└── beyondsurveys/
    ├── index.html                 ← Beyond Surveys home page  [TO BUILD]
    ├── services.html              [TO BUILD]
    ├── learning.html              [TO BUILD]
    ├── portfolio.html             [TO BUILD]
    └── workwithme.html            [TO BUILD]
```

---

## Design system

All visual decisions are driven by a consistent set of values defined at the top of each CSS file as **design tokens** — named variables that store the colours:

| Name | Hex value | Used for |
|---|---|---|
| `--parchment` | `#FAF6EE` | Page background |
| `--cream` | `#E8D9B5` | Cards, surfaces, section backgrounds |
| `--amber` | `#C8A96A` | Accent lines, card borders, active nav underline |
| `--deep-brown` | `#7A5C2E` | Secondary text, borders, muted links |
| `--green` | `#4A6B4A` | Call-to-action links, blockquote accent |
| `--ink` | `#2C1F0E` | Body text and headings |

If you ever want to adjust a colour, you change it in one place (the `:root` block at the top of the CSS) and it updates everywhere on that page.

**Fonts:** Two typefaces are used throughout:
- **Patrick Hand** (loaded from Google Fonts) — used for anything that should feel hand-drawn or informal: the notebook labels, card titles, the belief callout, pull quotes, and the lifecycle diagrams in the consulting site
- **Georgia** (built into every computer) — used for all body text and headings. It is a serif font with a warm, readable quality that suits the tone of the content

No sans-serif fonts (like Arial or Roboto) are used anywhere.

---

## Hub page — component by component

### Navbar

The navigation bar sticks to the top of the screen as you scroll. It contains:
- **"Greta James"** (left) — a branded link back to the home page
- **"About"** (right) — static text, not a link, with an amber underline indicating this is the current page. Intentionally not clickable because you are already on this page
- **"Beyond Surveys Consulting"** (right) — links to `beyondsurveys/`
- **"Granter's Academy"** (right) — links to `grantersacademy/`

### About section

The about section uses a **CSS Grid** layout with two columns on desktop:

- **Left column (260px):** Greta's headshot stacked directly above the belief callout blockquote. The photo has a thin cream border and a subtle shadow. Below it, the belief callout sits flush to the bottom of the photo column.
- **Right column (flexible):** The name heading and three bio paragraphs.

On screens narrower than 660px (phones), the grid collapses to a single column. The order becomes: photo → belief callout → bio text.

### Blockquote callout (belief statement)

Positioned directly below the photo in the left column. Styling:
- **Font:** Patrick Hand — gives it a personal, handwritten quality distinct from the Georgia body text
- **Left border:** 4px solid quiet green
- **Background:** faint green tint (`rgba(74, 107, 74, 0.045)`) — barely perceptible, signals it as different from the body text without being visually heavy
- **No extra margin** above it — sits naturally below the photo with the column gap as spacing

There is an HTML comment directly above the blockquote:
```
<!-- TODO: link belief paragraph to article on social service sector incentives when ready -->
```
This is a reminder to add a link to an article Greta plans to write. It does not appear on the visible page.

### Notebook graphic

The centrepiece of the hub page. Built entirely with HTML and CSS — no image files required for the notebook itself.

**How it works on desktop:**

All notebook elements live inside a `580 × 475px` wrapper div using `position: absolute` to place them precisely.

The notebook scene has `50px` of top padding, which provides visual breathing room for the back card's title tab to appear above the notebook cover without being clipped.

Three layers (back to front):

1. **Card 2 — Granter's Academy** (rendered first in HTML, lowest z-index)
   - `top: -35px` — raised 62px above card-1's resting position, so its title area sits visibly above card-1's top edge at the right side of the notebook
   - `transform: rotate(-9deg)` — more angled, appears behind and above
   - Slightly warmer background colour than card-1 to visually distinguish the two pages

2. **Card 1 — Beyond Surveys Consulting** (in front of card-2)
   - `top: 27px`
   - `transform: rotate(-4deg)` — nearly upright, closest to the viewer
   - Both cards use `transform-origin: left center`, meaning they rotate from their left edge — the point where they tuck into the notebook cover. This creates the look of pages opening from a binding

3. **Notebook cover** (rendered last, highest z-index — sits on top of both cards)
   - `278 × 435px` dark brown rectangle with rounded right corners
   - Left strip (spine) is a darker shade with an inset shadow
   - A cream label rectangle sits near the top of the cover face (CSS `::after` pseudo-element)
   - "Greta James / Projects" in Patrick Hand sits over the label
   - Faint horizontal lines near the bottom suggest a worn ruled page

On hover, each card slides 15px to the right while holding its rotation angle, giving a "pulling out" effect.

**Adding a third project tab in the future:**

The HTML and CSS already have placeholder comments for this. When a third project is ready:
1. Add a new `<a>` element in the HTML before the `.card-2` element, with class `"project-card card-3"`
2. Uncomment the `.card-3` CSS rule (currently commented out in the `<style>` block)
3. No other layout changes are needed

**How it works on mobile:**

On screens ≤ 660px, JavaScript hides the desktop notebook scene and shows a compact version instead:
- A small notebook icon (same CSS styling, scaled to 68 × 96px)
- "Tap to explore current projects" text beside it
- Tapping slides down a drawer containing the two project cards stacked vertically
- Tapping again collapses the drawer

### Footer

A single centred line with a quiet email link and a LinkedIn link. No prominent button or call-to-action styling — intentionally low-key.

---

## How to make common changes

### Update the bio text
Open `index.html`, find `<div class="about-text">`. The bio is in three `<p>` tags. Edit the text directly between the tags.

### Update the belief statement
Find `<blockquote class="belief-callout">` in the left column of the about grid. Edit the text inside the `<p>` tag within it.

### Add or remove a nav link
Find `<ul class="nav-links">` in the navbar. Add or remove `<li><a href="...">Link Text</a></li>` items.

### Change a project card's title or description
Find `<a class="project-card card-1">` (or `card-2`). The title is in `<span class="card-title">` and the description is in `<p class="card-description">`.

### Change where a project card links
Find the card's `<a>` opening tag and update the `href="..."` attribute.

### Update the footer contact details
Find `<footer class="site-footer">` near the bottom of `index.html` and edit the text and link targets inside it.

### Change a colour globally
Open `index.html`, find the `:root {` block near the top of the `<style>` section, and change the hex value next to the token name (e.g. `--green: #4A6B4A;`).

---

## Contact forms (not yet built)

All contact forms will be handled by **Formspree** — a free service that receives form submissions and forwards them to an email address. No backend server or database is required.

Before the site goes live, you will need to:
1. Create a free account at formspree.io
2. Create a form and copy the endpoint URL it gives you
3. Replace the placeholder text `YOUR_FORMSPREE_ENDPOINT` in the form `action` attributes across the consulting site pages

---

## Before the site goes live — checklist

- [ ] Create Formspree account and add endpoint URLs to all contact forms
- [ ] Purchase `gretajames.ca` from Namecheap and point it to GitHub Pages
- [ ] Set up `greta@gretajames.ca` email (via Proton Duo once domain is purchased)
- [ ] Confirm permission from the Food Bank of Waterloo Region for Portfolio Example 3, then remove the permission warning notice
- [ ] Add calendar booking link for Track 3 support calls and free consultation calls (placeholder mailto links in HTML with TODO comments)
- [ ] Confirm YouTube video links are permanent (Learning Resources page)
- [ ] Add email signup for Learning Resources notifications
- [ ] Add M4C mailing list link on Services page
- [ ] Review and remove all `href="#"` placeholder links before publishing

---

## Build session log

| Session | Date | What was built / changed |
|---|---|---|
| 1 | 2026-04-01 | Hub page (`index.html`) — navbar, about section, blockquote callout, notebook graphic |
| 2 | 2026-04-01 | Hub page revisions: Granter's Academy added to navbar; back card raised to show title tab; belief callout moved under photo and set in Patrick Hand; notebook scaled 50% larger; build docs updated |
