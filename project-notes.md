# Beyond Surveys Consulting — Build Log

All project spec, content, and styling notes are in `project-spec.md`.

---

## BUILD LOG

### Session 6 — 2026-05-06

**Completed**

* `beyondsurveys/services.html` — Services page substantially redesigned:
  * Opening paragraph text enlarged to 1.4rem to fill full container width
  * All visible "Track" terminology replaced with "Path" (card IDs and URL params kept as track1/track2/track3 for anchor link compatibility)
  * Track card boxes replaced with a parchment/scroll aesthetic: graduated radial-gradient backgrounds (freshest parchment on Path 1, most aged on Path 3), amber border, and CSS scroll roll pseudo-elements (::before/::after ovals peeking above and below each card, z-index: -1)
  * Full-width hero banner behind "Services" heading: "banner path in woods.png" as a CSS background image with a 65%-opacity green linear-gradient overlay — text remains white and legible
  * "Path in the woods.png" added to the In-Kind Support section as a left-side image with text floated right
  * Tap-to-expand cards: cards start collapsed at 165px showing only the path title, "Best for…" subtitle, and "Tap to read more ▼" hint; tapping any card expands all three simultaneously to equal height (measured via scrollHeight); tapping again collapses all three; scroll rolls appear only when expanded; link clicks do not bubble up to the card toggle
  * Path 2 h2 shortened to "Path 2 — Student Support"; Path 3 shortened to "Path 3 — Workshops" so all three titles fit on one line and the expand hint is consistently visible

**Design decisions made (not previously in spec)**

* Hero banner uses CSS multi-layer background shorthand: `linear-gradient(rgba…) url(…) center / cover` — the gradient sits on top as a colour wash, the image behind it. This technique requires no extra HTML elements.
* Tap-to-expand uses `scrollHeight` (not a fixed large max-height) so the animation runs only as far as the content actually extends; tallest card's scrollHeight is applied to all three so they stay equal when open
* Scroll rolls (::before/::after) use `display: none` on non-expanded cards — while overflow:hidden would clip them anyway, being explicit avoids any rendering edge cases
* Collapse/expand is group behaviour: one tap affects all three cards, keeping the page tidy and the cards visually consistent at all times

**Still in progress / needs attention**

* **Next session prompt:** Consider merging the Work With Me page and the Services page — they currently have substantially overlapping content (both describe the three paths and offer ways to get in touch). A combined page would reduce redundancy and simplify navigation.
* `grantersacademy/index.html` — not yet built; deferred (content still in progress)
* All pre-go-live checklist items remain open (see Section 12 of `project-spec.md`)

---

### Session 5 — 2026-05-05

**Completed**

* `beyondsurveys/index.html` — Beyond Surveys home page substantially reworked:
  * Intro section restructured as a 50/50 two-column flex layout: new condensed text (two paragraphs) on the left, `assets/generic consulting image.png` on the right
  * h1 heading enlarged from 1.9rem to 2.5rem, forced line break removed, word "actually" removed — now reads "Build measurement capacity your organization owns"
  * CTA/pricing banner: Patrick Hand bold tagline added above pricing links — "Let's build a measurement system you understand, you own, and you can grow independently!"
  * Approach section replaced "Our approach" h2 + four prose paragraphs with a two-column layout:
    * Left (~40%): CSS circle (cream background, amber border, `aspect-ratio: 1`, `border-radius: 50%`) containing "I help organizations:" bullet list in Patrick Hand
    * Right (~60%): new "Why Beyond Surveys?" heading with rewritten survey-problem text and bullet list

* `beyondsurveys/style.css` — container `max-width` widened from 860px to 1040px; applies to all Beyond Surveys pages

* `beyondsurveys/learning.html` — Learning Resources page rebuilt:
  * Intro text reduced to one sentence plus "I am always building new content."
  * Four-step TOC flow removed entirely
  * Page intro restructured as two-column flex: heading + framing + notify-link on the left; callout on the right
  * Callout went through several iterations this session (green text block → teal typography → terracotta → burgundy/circle → banner). Final design: left-pointing ribbon banner using CSS `clip-path: polygon()`, burgundy background (#7A3048, chosen by Greta), white Patrick Hand heading, white body text
  * Resource cards replaced with a 3-column CSS Grid video layout:
    * Sessions 1 and 2: 16:9 YouTube thumbnails fetched from `img.youtube.com/vi/[ID]/hqdefault.jpg` (no API key needed); circular play button overlay with hover animation; clicking thumbnail opens YouTube video
    * "Common Survey Design Mistakes" and "Other Ways to Measure Your Impact": matching 16:9 parchment placeholder with "Coming soon" in Patrick Hand; not clickable; slight opacity reduction
    * M4C partnership attributed with a live link in both active cards
  * Grid is responsive: 3 columns → 2 columns (≤ 760px) → 1 column (≤ 480px)

**Design decisions made (not previously in spec)**

* Container widened to 1040px globally — two-column layouts on the home page felt cramped at 860px; all Beyond Surveys pages benefit from more breathing room
* CSS circle on home page approach section uses `aspect-ratio: 1` + `border-radius: 50%` + 17% internal padding to keep text within the safe circular area; converts to a rounded box on mobile (≤ 680px)
* YouTube thumbnails: `hqdefault.jpg` (480×360, 4:3) is displayed in a 16:9 wrapper with `object-fit: cover` — slight crop but reliable without API access
* Callout banner shape implemented with `clip-path: polygon(28px 0, 100% 0, 100% 100%, 28px 100%, 0 50%)` — a left-pointing arrow that visually "points back" at the content it references
* Burgundy (#7A3048) added as a fourth accent colour — used only for the Learning Resources callout banner; provides contrast against the amber/brown/green palette without clashing

**Still in progress / needs attention**

* `grantersacademy/index.html` — not yet built; deferred (content still in progress)
* Two resource link placeholders on home page (`href="#"` below the lifecycle graphic) still need updating once learning module anchors are confirmed
* All pre-go-live checklist items remain open (see Section 12 of `project-spec.md`)

---

### Session 4 — 2026-04-03/04

**Completed**

* Project infrastructure reorganised for session efficiency:
  * `CLAUDE.md` — created with session start/end protocol, design cheat-sheet (palette, typography, nav), build status table, 4-step wrap-up protocol, spec section index, shared CSS instruction, collaboration preferences
  * `project-notes.md` — trimmed to build log only (~80 lines vs. ~700); all spec content extracted to `project-spec.md`
  * `project-spec.md` — new file containing all spec sections 1–13 with line-range index at top for targeted reads
  * `beyondsurveys/style.css` — shared stylesheet created; tokens, reset, container, nav, bio card, footer and shared responsive rules extracted from `beyondsurveys/index.html`
  * `beyondsurveys/index.html` — updated to load shared CSS; SVG lifecycle graphic built to replace placeholder; body text widened to full container; resource links centred; bio card centred

* All remaining Beyond Surveys pages built:
  * `beyondsurveys/services.html` — intro, three equal-height track cards (CSS grid, `align-items: stretch`), stacked action links, "Not sure which track" CTA, In-Kind Support banner (amber borders)
  * `beyondsurveys/learning.html` — green-border framing section, four-step horizontal TOC flow (responsive: vertical on mobile), "Getting Started" parent card with two session sub-items, two Coming Soon muted cards with badge
  * `beyondsurveys/portfolio.html` — two-column card grid (`align-items: start`), five portfolio examples with project-name-only titles, permission notice on Market Dollars, video placeholder on Scoping Housing, pull quotes on Measurement 101, dashboard image on Community Needs Survey, mini bio card
  * `beyondsurveys/workwithme.html` — compact three-column track cards (equal height via grid stretch), three button visual weights (green fill / outlined brown / outlined amber), shared enquiry form with JS source-param routing, JS replaces form with confirmation on submit
  * `beyondsurveys/inkind.html` — standalone in-kind application page, not in navbar, accessible only from Work With Me; has standard nav (no active item), page-title intro, in-kind form with JS confirmation

**Design decisions made (not previously in spec)**

* Track cards on Work With Me use `align-items: stretch` (not `start`) so all three cards match height; `flex-grow: 1` on description paragraph pushes buttons to bottom of every card
* In-Kind Support application moved to dedicated `inkind.html` rather than a section at the bottom of `workwithme.html` — keeps the Work With Me page focused and makes the in-kind application feel appropriately separate
* Portfolio card order changed from spec order: Row 1 = KPI System + Community Needs Survey; Row 2 = Scoping Housing + Measurement 101; Row 3 = Market Dollars (full width) — two longest cards together, permission-pending card alone for maximum visibility
* "Example N —" prefix removed from portfolio card titles — project names only
* SVG lifecycle graphic: two circular diagrams, labels at radius 110, 14° arc gap per step, scroll container on mobile (`min-width: 640px`); caption changed to "grounded, useful and yours"
* Home page body text widened to full container (removed `max-width: 680px`) to match lifecycle graphic width; resource links centred; bio card centred

**Still in progress / needs attention**

* `grantersacademy/index.html` — coming-soon stub not yet built; deferred (Greta still drafting content)
* SVG lifecycle graphic label positions may need minor visual tweaks after browser review
* All pre-go-live checklist items remain open (see Section 12 of `project-spec.md`)

---

### Session 3 — 2026-04-02

**Completed**

* `index.html` — notebook graphic redesigned and belief callout revised:
  * Cards now pivot from `transform-origin: left bottom` — tops fan away from the book, bottoms stay tucked behind the cover
  * Card positions changed from negative rotation (top leaning in) to positive rotation: card-1 (Beyond Surveys) at `rotate(8deg) top: 25px`, card-2 (Granter's Academy) at `rotate(14deg) top: -55px` (user adjusted to -55px)
  * "Learn more →" on card-1 pushed to bottom-right with `align-self: flex-end`
  * Notebook wrapper expanded to 640×520px to accommodate wider fan footprint
  * Label text on cover ("Greta James / Projects") centred with `text-align: center`
  * Belief callout stretched to bottom-align with bio column: `align-items: stretch` on grid, `flex: 1` on callout
  * Belief callout font size increased to `1.2rem`, line-height to `1.85` to fill the box
* `beyondsurveys/index.html` — Beyond Surveys home page built:
  * Beyond Surveys navbar: `← Greta James` back-link (left, secondary) + `Home | Services | Learning Resources | Portfolio | Work With Me` (right); back-link hides on screens ≤ 760px to save space
  * Intro section: brand eyebrow, h1 heading, Patrick Hand tagline, two positioning paragraphs; "free resources" links to `learning.html`
  * Pricing/CTA block: cream background, amber top and bottom borders, italic text with bold green links; consultation link uses `mailto:` for now with TODO comment
  * Our Approach section: four paragraphs of prose followed by lifecycle graphic placeholder (clearly labelled, dashed amber border) and two resource links (placeholder `href="#"` pending learning module pages)
  * Mini bio card: circular headshot, two-line bio, "Learn more about Greta →" back-link; cream card with amber circle border and subtle shadow

**Design decisions made (not previously in spec)**

* Back-link "← Greta James" hidden at ≤ 760px (not ≤ 660px) — the 5-item consulting nav already crowds at tablet widths; the hub is still reachable via direct navigation
* Consultation call CTA on home page links to `mailto:` (not `workwithme.html`) — the Work With Me page form isn't built yet; TODO comment marks where the booking link goes
* Resource links (Common survey design mistakes, Other ways to measure your impact) use `href="#"` placeholder — will link to learning module anchors once `learning.html` is built
* Mini bio card uses circular crop (border-radius: 50%) rather than the rectangular headshot on the hub page — suits the smaller card format

**Still in progress / needs attention**

* `beyondsurveys/index.html` — SVG lifecycle graphic (two circular diagrams, "The usual story" / "A better way") deferred to next session; placeholder div in place with full spec reference
* `grantersacademy/index.html` — coming-soon stub still not built; spec not yet written (discussed: needs more content planning before building)
* All remaining `/beyondsurveys/` pages not yet built: `services.html`, `learning.html`, `portfolio.html`, `workwithme.html`
* All pre-go-live checklist items remain open (see Section 12 of project-spec.md)

---

### Session 2 — 2026-04-01

**Completed**

* `index.html` — full hub page built and revised:
  * Sticky navbar with About (static, amber underline), Beyond Surveys Consulting, and Granter's Academy
  * Two-column about section: left column holds headshot + belief callout stacked; right column holds name heading + three bio paragraphs
  * Belief callout styled with Patrick Hand font, quiet green left border, faint green-tinted background — positioned directly below photo
  * CSS-only notebook graphic (no image files) scaled to 1.5× original design: 278×435px cover with spine and label, two 330×402px fanning project cards. Back card (Granter's Academy) raised to `top: -35px` so its title tab is visible above the front card. Third card slot reserved in commented HTML and CSS for future use.
  * Hover interaction: each card slides 15px outward while holding rotation angle
  * Mobile tap-to-reveal drawer (JS swap at ≤ 660px breakpoint)
  * Quiet footer with email and LinkedIn links
* `build-process.md` — new plain-English documentation covering site architecture, tech choices, component descriptions, and a how-to-change guide for common edits
* `project-notes.md` — hub page styling notes and navbar spec updated to reflect all design decisions made during build

**Design decisions made (not previously in spec)**

* Belief callout repositioned from bottom of bio text to left column below photo — keeps the left column visually balanced and creates a natural pause between photo and bio
* Belief callout font set to Patrick Hand — distinguishes it from the Georgia body text and gives it a personal, handwritten quality consistent with the notebook aesthetic
* Notebook scaled to 1.5× for visual impact at desktop viewport widths; rotation angle on back card reduced from −12° to −9° to compensate for the wider card size (otherwise the tilt would be too steep)
* Back card raised with 50px top padding on the notebook scene (rather than clipping) so the title tab appears clearly above the cover without overflow issues
* Granter's Academy added to navbar (in addition to the notebook card) so it is accessible via direct navigation, not only through the notebook graphic

**Still in progress / needs attention**

* `grantersacademy/index.html` — coming-soon stub page not yet built; Granter's Academy links in navbar and notebook card currently 404
* All `/beyondsurveys/` pages not yet built
* All pre-go-live checklist items remain open (Formspree, domain, email, Food Bank permission, calendar links — see Section 12 of project-spec.md)

---

### Session 1 — 2026-04-01

Initial project setup. `project-notes.md` written as handoff spec. Repository created at `gretajames.github.io`. No HTML files built.
