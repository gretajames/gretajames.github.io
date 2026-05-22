# Build Process — Greta James Website

A plain-English reference for understanding how this site is built and how to maintain it. No coding experience required to read this — it explains the decisions behind the code and how to make common changes.

---

## What we are building

Two connected websites, both living in the same folder:

| Site | Address | Purpose |
|---|---|---|
| Hub page | `gretajames.ca` | Personal landing page — introduces Greta and routes visitors to her projects |
| Consulting site | `gretajames.ca/beyondsurveys` | Full Beyond Surveys Consulting site — five pages |

There is also a coming soon page at `gretajames.ca/grantersacademy` for the Granter's Academy project (built in Session 7). The full Granter's Academy site is a future project.

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
├── CLAUDE.md                      ← Session instructions for Claude Code (auto-loaded)
├── project-notes.md               ← Build log only
├── project-spec.md                ← Full content and styling spec (sections 1–13)
├── build-process.md               ← This file
├── index.html                     ← gretajames.ca hub/About page  [BUILT]
├── assets/
│   ├── Professional head shot.jpg ← Greta's headshot
│   ├── Community Needs Dashboard.jpg
│   └── generic consulting image.png ← used on Beyond Surveys home page intro
├── grantersacademy/
│   └── index.html                 ← Coming soon stub page  [TO BUILD]
└── beyondsurveys/
    ├── style.css                  ← Shared stylesheet for all consulting pages  [BUILT]
    ├── index.html                 ← Beyond Surveys home page  [BUILT]
    ├── services.html              [BUILT]
    ├── learning.html              [BUILT]
    ├── portfolio.html             [BUILT]
    ├── workwithme.html            [BUILT]
    └── inkind.html                ← In-kind application (not in navbar)  [BUILT]
```

---

## Analytics — GoatCounter

The site uses [GoatCounter](https://goatcounter.com) for privacy-friendly traffic tracking. It is free, uses no cookies, and requires no consent banner.

**Account:** `gretajames.goatcounter.com`

**How it works:** A small JavaScript snippet loads on each page and sends a page view ping to GoatCounter's servers when a visitor arrives. No personal data is collected — GoatCounter estimates unique visitors using browser characteristics rather than cookies.

**What it tracks:** page views, unique visitors, referrers (how people found the site), browser, operating system, screen size, and country.

**The snippet** is placed just before `</body>` in all 8 HTML files:
```html
<script data-goatcounter="https://gretajames.goatcounter.com/count"
        async src="//gc.zgo.at/count.js"></script>
```

**Adding a new page:** paste the snippet above into any new HTML file, just before `</body>`.

**Ignoring your own visits:** visit `https://gretajames.ca/#toggle-goatcounter` once in each browser you use. This sets a cookie that tells GoatCounter to skip you across the whole site. You do not need to do this per page.

**Resetting stats:** GoatCounter dashboard → Settings → delete all pageviews. Useful if you want to wipe test data before going live.

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

If you ever want to adjust a colour, change it in `beyondsurveys/style.css` (for the consulting site) or in the `:root` block at the top of `index.html` (for the hub page). One change updates that colour everywhere it is used.

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

### Current Projects section

The notebook sits in its own `<section class="projects-section">` directly below the about section. The two sections are intentionally flush (no vertical padding between them) so the green callout sidebar reads as one continuous visual element down the left side of the page.

**How the visual continuity works:**

The about section and projects section both use an identical `260px | 1fr` CSS Grid. The left column of the projects grid contains an empty `<div class="callout-extension">` (with `aria-hidden="true"`) that carries the same green left border and faint green background as the belief callout above it. Because `align-items: stretch` is set on the grid, this div expands to fill the full height of the row — visually extending the callout sidebar down to the bottom of the notebook.

On screens ≤ 660px the `.callout-extension` div is hidden and both sections revert to single-column layout.

**Layout summary:**

- `projects-section` padding: `0 0 5rem` (no top padding — flush with about section above)
- `projects-grid` mirrors `about-grid`: `grid-template-columns: 260px 1fr; gap: 3rem; align-items: stretch`
- Left cell: `.callout-extension` — empty div, green border + faint green background only
- Right cell: `.projects-right` with `padding-top: 2rem`, contains the "Current Projects" label and the notebook scene
- The "Current Projects" label is small-caps, centred, upper case (`text-align: center; text-transform: uppercase`)
- The notebook scene is centred within `.projects-right` using `justify-content: center` on a flex container

**To change the notebook position:** The notebook is centred under the bio text by design. If you want it left-aligned, remove `justify-content: center` from `.notebook-scene`.

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

- A small all-caps brand label ("Beyond Surveys Consulting") in Patrick Hand sits above the main heading
- The `h1` heading ("Build measurement capacity your organization owns") spans the full width of the section at 2.5rem
- The tagline "Measure. Learn. Grow." is in Patrick Hand italic
- Below the tagline, the section uses a **50/50 two-column flex layout**: two short paragraphs of positioning copy on the left; `assets/generic consulting image.png` on the right. On screens ≤ 680px the columns stack vertically (text above image).
- To update the intro text, find the `<div class="intro-text">` block and edit the two `<p>` tags inside it. To swap the image, replace `generic consulting image.png` with a different file in the `assets/` folder and update the `src` attribute in the `<img>` tag.

**2 — Pricing / CTA block**

- Cream background with amber borders top and bottom
- A bold Patrick Hand tagline ("Let's build a measurement system you understand, you own, and you can grow independently!") sits above the pricing links — styled with class `cta-tagline`
- Two action links follow: see pricing (→ `services.html`) and book a consultation call. The consultation booking link currently uses `mailto:greta@gretajames.ca` as a placeholder with an HTML comment marking where a calendar booking link should go.

**3 — Approach section**

This section uses a **two-column flex layout**:

- **Left column (~40%):** A CSS circle containing the "I help organizations:" bullet list in Patrick Hand. The circle is created by making a square div (`aspect-ratio: 1`) with `border-radius: 50%`, a cream background, and an amber border. Internal padding of 17% keeps the text away from the curved edges. On screens ≤ 680px the circle converts to a rounded rectangle. To edit the bullet list, find `<div class="approach-circle">` and edit the `<li>` elements inside it.
- **Right column (~60%):** The "Why Beyond Surveys?" heading and three paragraphs explaining the limits of surveys and the value of existing data sources. To edit this text, find `<div class="approach-why">` and edit the content inside.

Below the two-column section, the **lifecycle SVG graphic** remains unchanged — two circular diagrams ("The usual story" / "A better way") embedded directly as inline SVG. On screens narrower than 640px it scrolls horizontally. To adjust a label, find the `<!-- LIFECYCLE GRAPHIC -->` comment block and edit the relevant `<text>` element.

Two resource links at the bottom ("Common survey design mistakes →", "Other ways to measure your impact →") still use `href="#"` — update these to real `learning.html` anchors when the modules are published.

**Mini bio card**

- Sits below the main content, above the footer, separated by a hairline rule
- Circular-cropped headshot (72×72px), two lines of bio text, and a "Learn more about Greta →" link back to the hub page
- Uses a cream card background with a subtle shadow — the same card treatment used elsewhere in the consulting site

### Services page (`beyondsurveys/services.html`)

**Hero banner**

The "Services" heading sits inside a full-width banner that uses `assets/banner path in woods.png` as a background image. A semi-transparent green overlay (`linear-gradient(rgba(74,107,74,0.65), rgba(74,107,74,0.65))`) is layered on top of the image using CSS's multi-layer background shorthand, keeping the white text readable regardless of which part of the photo is behind it. To swap the photo, replace `banner path in woods.png` in the `assets/` folder and update the filename in the `.page-intro` CSS `background` property.

**Path cards**

Three cards in a CSS Grid (three columns on desktop, one on mobile). Each card uses a parchment aesthetic — a radial gradient background that graduates from fresh cream (Path 1) to aged amber (Path 3). CSS `::before` and `::after` pseudo-elements create scroll-roll ovals that peek above and below each card when expanded.

Cards start collapsed (showing only the path title, "Best for…" line, and a "Tap to read more ▼" hint). Tapping any card expands all three simultaneously to equal height; tapping again collapses all three. The collapse/expand logic is in a `<script>` block at the bottom of the file.

Each card has an `id` attribute (`id="track1"`, `id="track2"`, `id="track3"`) so the Work With Me page can link directly to a specific path using anchor links (e.g. `services.html#track1`). These IDs are kept as "track" (not "path") to avoid breaking existing links.

**In-Kind Support section**

Below the cards, the In-Kind Support section uses a flex layout: `assets/Path in the woods.png` on the left (220px wide), text and link on the right. On mobile the image sits above the text. The section has amber borders top and bottom to signal it as a visually distinct option.

**To edit a path card:** Find the relevant `<div class="track-card" id="trackN">` block. Edit the `<h2>` (title), `<p class="best-for">` (subtitle line), `<p>` / `<ul>` (body), or `<a class="track-action">` (link) inside it. Do not edit `<p class="expand-hint">` — that is the "Tap to read more" cue text managed by CSS/JS.

### Learning Resources page (`beyondsurveys/learning.html`)

**Page intro — two-column layout**

The top of the page uses a flex row with two columns:

- **Left column (58%):** The "Learning Resources" h1, a short framing paragraph with a green left border, and a "Sign up to be notified" email link.
- **Right column (42%):** A callout banner pointing visitors to Track 3 if they need guided support. The banner is a left-pointing arrow shape created with CSS `clip-path: polygon(28px 0, 100% 0, 100% 100%, 28px 100%, 0 50%)`. It has a burgundy background (#7A3048) with white text — the heading is large Patrick Hand, the body text is smaller Georgia. On screens ≤ 680px the columns stack vertically.

To edit the callout text, find `<div class="callout-block">` and edit the `<p class="callout-heading">` and `<p class="callout-body">` inside it.

**Video grid**

Below the intro, all learning content lives in a **3-column CSS Grid** (`class="video-grid"`). Each card shows a 16:9 thumbnail, a title, and a description.

*Active video cards* (`class="video-card"`): The thumbnail is fetched directly from YouTube's CDN using the video ID — no API key required. The format is `https://img.youtube.com/vi/[VIDEO-ID]/hqdefault.jpg`. The thumbnail is wrapped in an `<a>` tag linking to the YouTube video. A circular play button (white circle with a ▶ character) sits centred over the thumbnail and animates on hover.

*Coming soon cards* (`class="video-card video-card-soon"`): The thumbnail area is replaced with a parchment-coloured placeholder the same 16:9 size, with "Coming soon" written in Patrick Hand. These cards are not clickable and are shown at 70% opacity.

**Adding a new video when it's ready:**
1. Find a `<div class="video-card video-card-soon">` block for that module
2. Change the class to `video-card` (remove `video-card-soon`)
3. Replace the `<div class="video-thumb-soon">` block with:
```html
<a href="https://www.youtube.com/watch?v=VIDEO-ID" target="_blank" rel="noopener noreferrer" class="video-thumb-link">
  <div class="video-thumb">
    <img src="https://img.youtube.com/vi/VIDEO-ID/hqdefault.jpg" alt="Video title" />
    <span class="play-btn" aria-hidden="true">▶</span>
  </div>
</a>
```
4. Replace `VIDEO-ID` in both the `href` and `src` with the real YouTube video ID (the part after `?v=` in the YouTube URL)

**Adding a brand new module card:** Copy any existing `<div class="video-card">` block and paste it inside `<div class="video-grid">`. The grid places cards left to right, wrapping to a new row every three cards.

### Portfolio page (`beyondsurveys/portfolio.html`)

Cards sit in a two-column CSS Grid on desktop, single column on mobile (below 700px). Cards use `align-items: start` so shorter cards do not stretch to match their taller neighbours.

Current visible cards: KPI System, Community Needs Survey, Market Dollars, Measurement 101. The Scoping a Housing Program card is currently hidden (commented out) until a video is ready.

**Expand/collapse behaviour:** Clicking any card toggles an `expanded` class. The "Click for details ▼" hint hides when expanded; a "Click to collapse ▲" hint appears at the bottom. The collapse hint is injected by JavaScript (not in the HTML directly), so it automatically applies to all cards including any added in the future.

**Unhiding the Scoping a Housing Program card:** Search for `Card 5: Scoping a Housing Program` in the file. The card is wrapped in an HTML comment (`<!-- ... -->`). Remove the comment delimiters and replace the `<div class="media-placeholder">` block with an `<iframe>` video embed when the video is ready.

**Video placeholder (Scoping Housing card):** A dashed amber placeholder marks where the video will go. When ready, replace `<div class="media-placeholder">` with a standard `<iframe>` embed.

**Permission notice (Market Dollars card):** The warning card has been removed — permission is confirmed. If you ever need a similar notice on another card, use `<div class="permission-notice">` (the CSS class is still defined in the shared stylesheet).

**Adding a new portfolio item:** Copy any existing `<div class="portfolio-card">` block, paste it inside the `.portfolio-grid` div, and fill in the content. The grid will automatically place it in the next available cell.

### Work With Me page (`beyondsurveys/workwithme.html`)

**Track cards:** More compact than the Services page — one short description sentence per track, then stacked action buttons. Three button visual weights: green fill (primary enquiry action), outlined brown (more detail → services page), outlined amber (learning resources, Track 3 only).

**Source parameter routing:** Every enquiry button carries a `data-source` attribute (e.g. `data-source="beyondsurveys-track1"`). When clicked, JavaScript reads this value and sets the hidden `_subject` field in the enquiry form below, so Greta receives an email with the correct subject line for that track. The same routing happens automatically when arriving from another page with a `?source=` URL parameter.

**Enquiry form:** A shared form handles Track 1, Track 2, Track 3, and free consultation requests. The hidden `_subject` field changes based on which track button was clicked. On successful submission, the form is replaced in-place with a confirmation message — no page redirect.

**Before go-live:** Replace `YOUR_FORMSPREE_ENDPOINT` in the form `action` attribute with the real Formspree endpoint URL.

### In-Kind Application page (`beyondsurveys/inkind.html`)

A separate page for in-kind support applications — not linked from the navbar. It is only reachable by clicking "Apply for in-kind support" on the Work With Me page. This is intentional: the in-kind application is a distinct process from the three standard service tracks.

The page has the full standard Beyond Surveys navbar (so visitors can navigate elsewhere if they land here), but no nav item is shown as "active" since this page is not part of the main site navigation.

The form has more fields than the standard enquiry form: organization description, support needed, and a radio button asking about openness to graduate student support.

**Before go-live:** Replace `YOUR_FORMSPREE_ENDPOINT` in the form `action` attribute with the real Formspree endpoint URL.

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
Open the relevant consulting page, find `<ul class="nav-links">`, and add `<li><a href="newpage.html">Page Name</a></li>`. Remember to add the same link to **every** consulting page's navbar (including `inkind.html`) so the navbar stays consistent.

### Add a new portfolio item
Open `beyondsurveys/portfolio.html`, find `</div><!-- /portfolio-grid -->`, and paste a new `<div class="portfolio-card">` block before that closing tag. Copy the structure from an existing card. The grid places cards automatically — no layout changes needed.

### Publish a coming-soon learning module
In `beyondsurveys/learning.html`, find the `<div class="resource-card-soon">` for the module you're publishing. Change `resource-card-soon` to `resource-card` on the opening div. Remove the `<span class="badge-soon">Coming soon</span>` from the heading. Add a link (`<a href="...">Watch →</a>`) where the badge was.

### Replace the Formspree placeholder
In both `beyondsurveys/workwithme.html` and `beyondsurveys/inkind.html`, find `YOUR_FORMSPREE_ENDPOINT` in the `<form action="...">` attribute and replace it with the real endpoint from your Formspree account.

### Add a calendar booking link
Search for `TODO: replace with booking link` across the consulting pages. Each TODO comment sits directly above a `mailto:` link. Replace the `href="mailto:..."` value with your calendar URL.

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
| 3 | 2026-04-02 | Notebook graphic redesigned (new rotation scheme, cards fan from bottom pivot); belief callout stretches to match bio height; `beyondsurveys/index.html` built (navbar, intro, CTA block, Our Approach, mini bio card); SVG lifecycle graphic deferred |
| 4 | 2026-04-03/04 | Session infrastructure: `CLAUDE.md`, `project-spec.md`, `beyondsurveys/style.css` created; `project-notes.md` trimmed to log only. All remaining consulting pages built: `services.html`, `learning.html`, `portfolio.html`, `workwithme.html`, `inkind.html`. SVG lifecycle graphic built in `beyondsurveys/index.html`. |
| 5 | 2026-05-05 | Beyond Surveys home page reworked (two-column intro, enlarged heading, CTA banner, approach section redesigned). Container widened to 1040px. Learning Resources page rebuilt (ribbon banner, video grid). |
| 6 | 2026-05-06 | Services page redesigned: parchment/scroll card aesthetic, hero banner, tap-to-expand cards, Path terminology, In-Kind image. |
| 7 | 2026-05-07 | Granter's Academy coming soon page built. Hub and GA container widened to 1040px. Services page links, intro, and card equal-height JS updated. Work With Me stripped to form only with new checkbox question. |
