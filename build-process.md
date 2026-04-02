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

All notebook elements live inside a `640 × 520px` wrapper div using `position: absolute` to place them precisely.

Three layers (back to front):

1. **Card 2 — Granter's Academy** (rendered first in HTML, lowest z-index)
   - `top: -55px` — positioned above card-1 so its title is clearly visible
   - `transform: rotate(14deg)` — more rotation, fans further to the right
   - Slightly warmer background colour than card-1 to visually distinguish the two pages

2. **Card 1 — Beyond Surveys Consulting** (in front of card-2)
   - `top: 25px`
   - `transform: rotate(8deg)` — less rotation, sits in front

3. **Notebook cover** (rendered last, highest z-index — sits on top of both cards)
   - `278 × 435px` dark brown rectangle with rounded right corners
   - Left strip (spine) is a darker shade with an inset shadow
   - A cream label rectangle sits near the top of the cover face (CSS `::after` pseudo-element)
   - "Greta James / Projects" in Patrick Hand sits centred over the label
   - Faint horizontal lines near the bottom suggest a worn ruled page

**How the card rotation works:**

Both cards use `transform-origin: left bottom`. This means rotation pivots from the card's bottom-left corner — the point tucked behind the notebook cover. A positive rotation angle (e.g. `rotate(8deg)`) tips the top of the card away from the book to the right, while the bottom stays anchored behind the cover. This creates the visual of pages fanning out from a binding.

The cover has the highest z-index, so it always sits on top of the cards and naturally hides the bottom-left corner of each card. The visible portion of each card — the part sticking out to the upper right — is what the reader sees.

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

---

## Beyond Surveys Consulting site — component by component

The Beyond Surveys site lives in the `beyondsurveys/` subfolder. Each page is a self-contained HTML file that shares the same design tokens (colours, fonts) as the hub page but has its own navbar and layout.

### How the consulting site differs from the hub page

| | Hub page (`index.html`) | Consulting site (`beyondsurveys/`) |
|---|---|---|
| Audience | General visitors, curious about Greta | Potential clients evaluating a specific service |
| Navbar | About · Beyond Surveys · Granter's Academy | ← Greta James · Home · Services · Learning Resources · Portfolio · Work With Me |
| Tone | Personal, introductory | Professional, service-focused |
| Palette use | Expressive (notebook graphic) | More restrained |

### Beyond Surveys navbar

Every consulting page has the same navbar structure:

- **← Greta James** (far left) — a subtle back-link to the hub page (`../`). It is intentionally muted (lower opacity, smaller font) so it doesn't compete with the main navigation. It is hidden on screens narrower than 760px to prevent crowding, since the five-item consulting nav already fills the bar at tablet widths.
- **Home · Services · Learning Resources · Portfolio · Work With Me** (right side) — the five consulting pages. The current page is shown as static bold text with an amber underline (same pattern as "About" on the hub page).

### Beyond Surveys home page (`beyondsurveys/index.html`)

Three visually distinct sections, plus a mini bio card and footer.

**1 — Intro section**

- A small all-caps brand label ("Beyond Surveys Consulting") in Patrick Hand sits above the main heading — acts as a visual anchor so visitors who land directly at this URL know where they are
- The `h1` heading ("Build measurement capacity your organization actually owns") is the primary SEO heading for the page
- The tagline "Measure. Learn. Grow." is in Patrick Hand italic — same hand-drawn quality as the hub page's belief callout
- Two paragraphs of positioning copy follow; "free resources" links to `learning.html`

**2 — Pricing / CTA block**

- Cream background with amber borders top and bottom — visually separates it from the sections above and below
- Italic surrounding text with bold green links draws the eye to the two actions: see pricing (→ `services.html`) and book a consultation call
- The consultation booking link currently uses `mailto:greta@gretajames.ca` as a placeholder. There is an HTML comment directly on this link marking where a calendar booking link should replace it when one is set up

**3 — Our Approach section**

- Four paragraphs explaining the theory-of-change approach and the limits of survey-only measurement
- Followed by a **lifecycle graphic placeholder** — a dashed amber box marking where the SVG diagram will go (to be built in a future session). The placeholder contains an HTML comment with the full diagram spec so the next developer can build it without hunting through the project notes
- Two resource links at the bottom ("Common survey design mistakes →" and "Other ways to measure your impact →") use `href="#"` as placeholders until the corresponding learning module pages exist

**Mini bio card**

- Sits below the main content, above the footer, separated by a hairline rule
- Circular-cropped headshot (72×72px), two lines of bio text, and a "Learn more about Greta →" link back to the hub page
- Uses a cream card background with a subtle shadow — the same card treatment used elsewhere in the consulting site

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
Find `<footer class="site-footer">` near the bottom of any page and edit the text and link targets inside it.

### Change a colour globally on one page
Open the relevant `.html` file, find the `:root {` block near the top of the `<style>` section, and change the hex value next to the token name (e.g. `--green: #4A6B4A;`). Note: because each page has its own `<style>` block, you would need to make the same change in every file to update the whole site. If you find yourself doing that often, it may be worth asking a developer to extract the shared CSS into a separate file.

### Update the Beyond Surveys intro text
Open `beyondsurveys/index.html`, find `<section class="intro-section">`. The two paragraphs of copy are in `<p>` tags. Edit the text directly. The tagline is in `<p class="intro-tagline">`.

### Replace the consultation booking link
In `beyondsurveys/index.html`, find the comment `<!-- TODO: replace with booking link when calendar integration is ready -->`. The `<a>` tag immediately after it is the "book a free consultation call" link. Replace the `href="mailto:..."` value with your calendar booking URL.

### Update the mini bio card text
In `beyondsurveys/index.html`, find `<div class="bio-card-text">`. Edit the `<p>` tag content for the bio text.

### Add a new nav link to the consulting site
Open the relevant consulting page, find `<ul class="nav-links">`, and add `<li><a href="newpage.html">Page Name</a></li>`. Remember to add the same link to every consulting page so the navbar stays consistent across the site.

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
| 3 | 2026-04-02 | Notebook graphic redesigned (new rotation scheme, cards fan from bottom pivot); belief callout stretches to match bio height; `beyondsurveys/index.html` built (navbar, intro, CTA block, Our Approach, mini bio card); SVG lifecycle graphic deferred to next session |
