# Beyond Surveys Consulting — Project Spec

## Section Index

Use these approximate line ranges with offset/limit when reading this file to avoid loading the whole document.

| Section | Content | Approx. start line |
|---------|---------|-------------------|
| 1 | Project Overview (structure, tech stack, file layout) | 18 |
| 2 | Design Principles + Colour Palette | 60 |
| 3 | Navigation | 90 |
| 4 | Hub Page — styling notes + content | 105 |
| 5 | Beyond Surveys Home Page | 165 |
| 6 | Services Page | 250 |
| 7 | Learning Resources Page | 335 |
| 8 | Portfolio Page | 405 |
| 9 | Work With Me Page | 510 |
| 10 | Contact Forms | 565 |
| 11 | Images | 620 |
| 12 | Open Items — pre-go-live checklist | 632 |
| 13 | Future Additions | 648 |

*Ranges are approximate. If a read clips content, extend the limit by 20–30 lines.*

---

## 1. PROJECT OVERVIEW

This document contains all content, structure, styling guidance, and technical notes needed to build the Beyond Surveys Consulting website. Read the relevant section before writing code for that page.

### Site structure

The site has two levels:

**Hub site:** `gretajames.ca`

- A minimal personal landing page introducing Greta James and routing visitors to her projects
- One page: About

**Consulting site:** `gretajames.ca/beyondsurveys`

- The full Beyond Surveys Consulting site, self-contained within the /beyondsurveys subdirectory
- Five pages: Home, Services, Learning Resources, Portfolio, Work With Me

### Tech stack

- Custom HTML/CSS/JS — no WordPress, no framework
- Hosted on GitHub Pages at gretajames.github.io (custom domain to be pointed once purchased from Namecheap)
- No backend — forms handled via Formspree (free tier, account creation required before go-live)

### File structure

```
gretajames.github.io/
├── index.html                          ← gretajames.ca hub/About page
├── assets/
│   ├── Professional head shot.jpg      ← Greta's headshot
│   ├── Community Needs Dashboard.jpg   ← Portfolio image
│   └── (additional images as added)
├── grantersacademy/
│   └── index.html                      ← Coming soon stub page
└── beyondsurveys/
    ├── style.css                       ← Shared stylesheet for all Beyond Surveys pages
    ├── index.html                      ← Beyond Surveys home page
    ├── services.html
    ├── learning.html
    ├── portfolio.html
    └── workwithme.html
```

### Local project path

`C:\Users\Greta James\Documents\Claude Code\Consulting Website\`

---

## 2. DESIGN PRINCIPLES

- Clean and minimal — fast to build, easy to maintain, appropriate for the audience
- Warm but professional tone — not corporate, not casual
- Mobile-first — all pages stack cleanly on mobile
- Consistent card/panel treatment across pages for visual cohesion
- The consulting site should feel self-contained — visitors who land at /beyondsurveys should not need to visit gretajames.ca to understand who they're hiring

### Colour palette

Use the following parchment-inspired palette throughout both sites. The hub page (gretajames.ca) may use the full palette expressively; the consulting site (/beyondsurveys) should use it more restrainedly.

| Role | Name | Hex |
|------|------|-----|
| Page background | Parchment | #FAF6EE |
| Surface / card background | Warm cream | #E8D9B5 |
| Accent / highlight | Amber brown | #C8A96A |
| Primary text / borders | Deep brown | #7A5C2E |
| CTA / active accent | Quiet green | #4A6B4A |
| Body text / headings | Ink | #2C1F0E |

### Typography

- Use **Patrick Hand** (Google Font) as the display/accent font — used for lifecycle graphics, pull quotes, and any hand-drawn-style elements
- Pair with a clean serif (Georgia or similar) for body text and headings
- Avoid generic sans-serif system fonts (Inter, Arial, Roboto) throughout

---

## 3. NAVIGATION

### Hub navbar (gretajames.ca)

`About | Beyond Surveys Consulting | Granter's Academy`

- About = active/home page at gretajames.ca — rendered as static text (not a link) with amber underline
- Beyond Surveys Consulting links to gretajames.ca/beyondsurveys
- Granter's Academy links to gretajames.ca/grantersacademy

### Beyond Surveys navbar (gretajames.ca/beyondsurveys)

`Home | Services | Learning Resources | Portfolio | Work With Me`

- Include a subtle back-link to gretajames.ca in the top left — styled as "← Greta James" as a secondary element, not competing with the main navbar
- Back-link hides at ≤ 760px (the 5-item consulting nav already crowds at tablet widths)
- This navbar is entirely scoped to the consulting content

---

## 4. HUB PAGE — gretajames.ca

### Styling notes

- Clean and minimal — introduces Greta and routes visitors to projects
- **Layout:** Two-column grid on desktop. Left column (260px): photo stacked above belief callout. Right column: name heading + bio paragraphs. Collapses to single column on mobile (photo → callout → bio).
- **Notebook / fanning pages graphic** — the centrepiece of the hub page. CSS-only field notebook (worn cover, visible spine) with two project cards fanning out to the right like tabbed pages. Scaled to 1.5× the original design size. Cards are positioned so both titles are visible: the back card (Granter's Academy) is raised so its title tab appears above the front card and above the notebook cover's top edge. Each card rotates from its left edge (transform-origin: left center) and slides outward on hover. On mobile, the notebook is replaced by a tap-to-reveal drawer.
- Cards pivot from `transform-origin: left bottom` — tops fan away from the book, bottoms stay tucked behind the cover
- Card positions: card-1 (Beyond Surveys) at `rotate(8deg) top: 25px`, card-2 (Granter's Academy) at `rotate(14deg) top: -55px`
- Notebook wrapper: 640×520px
- Currently two project tabs fan from the notebook:
  1. **Beyond Surveys Consulting** → gretajames.ca/beyondsurveys
  2. **Granter's Academy** → gretajames.ca/grantersacademy (points to a coming-soon placeholder page)
- Design accommodates a third tab without rebuilding the layout (commented placeholder in both HTML and CSS)
- The "belief" paragraph is styled as a blockquote/callout positioned below the photo in the left column — left border in quiet green (#4A6B4A), faint green-tinted background, **Patrick Hand font**, standard type size. Sits flush below the photo with natural column spacing above. Stretched to bottom-align with bio column: `align-items: stretch` on grid, `flex: 1` on callout. Font size `1.2rem`, line-height `1.85`.
- Email link at bottom is quiet — plain text, not a prominent CTA
- Add a placeholder HTML comment where the belief paragraph will eventually link to a standalone article:
  `<!-- TODO: link belief paragraph to article on social service sector incentives when ready -->`

### Content

**navbar:** `About | Beyond Surveys Consulting | Granter's Academy`

---

**About**

I'm Greta James — a researcher and monitoring and evaluation consultant based in Southern Ontario. I've spent the last several years applying that research background to helping social service organizations use data and empirical research to make better decisions and grow their impact. But I never expected to end up here.

I have always consumed ideas like candy — I devoured anthropology and psychology, cognitive science and biology in my undergraduate before completing a PhD in cognitive psychology at the University of Waterloo in 2018, where I specialized in judgment and decision-making. Then an unexpected thing happened: a short-term contract helping a local family shelter evaluate and redesign their programming showed me that I didn't just want to study how things work — I wanted to turn that knowledge into action. That contract turned into five years of frontline work evaluating programs and eventually into co-founding Measurement 4 Change. In that time, I've learned that very little of what researchers know about social change makes it to the front line — and very few of the questions on the front line make it back to researchers. Closing that gap is what this work is for.

Social problems are complex and difficult — but we give social service organizations almost no resources to experiment, innovate, or adapt. We expect them to deploy perfectly effective programming and make accurate decisions without the funding or support to probe the critical questions that inform their work. And we don't culturally accept failure or risk-taking — we certainly don't fund it.

*[BLOCKQUOTE/CALLOUT — style with left border accent, slightly larger type, generous whitespace]:*

> A well-functioning social service sector needs two things: affordable measurement and evaluation supports so organizations can learn from what they do, and financial incentives that reward innovation and honest learning rather than punishing uncertainty. That's what I'm working toward.

<!-- TODO: link belief paragraph to article on social service sector incentives when ready -->

**Current projects**

*(Displayed via the notebook/fanning pages graphic — see styling notes above)*

**Beyond Surveys Consulting** — Affordable monitoring and evaluation support for small social service organizations in Southern Ontario, with a focus on building internal measurement capacity that doesn't rely on surveys.
[Learn more →](gretajames.ca/beyondsurveys)

**Granter's Academy** — Coming soon.
[Learn more →](gretajames.ca/grantersacademy)

---

*Get in touch: greta@gretajames.ca or visit https://www.linkedin.com/in/greta-james/*

---

## 5. BEYOND SURVEYS — HOME PAGE

### `gretajames.ca/beyondsurveys/index.html`

### Styling notes

- Three visually distinct sections, each with its own background treatment or clear dividing line:
  1. Intro/positioning section
  2. Pricing/CTA block — visually prominent, separated above and below (light background or border)
  3. Our Approach section
- The two resource links at the bottom ([Common survey design mistakes →] and [Other ways to measure your impact →]) are placeholder links pointing to learning module content — use anchor tags with href="#" for now
- Mini bio card at the very bottom of this page: small headshot (assets/Professional head shot.jpg), two lines of bio, "Learn more about Greta →" linking to gretajames.ca. Style consistently with portfolio card treatment.

### Lifecycle graphic — "Our Approach" section

Include a side-by-side pair of circular lifecycle diagrams in the Our Approach section, after the explanatory prose. These are SVG graphics rendered directly in the page (no external image files needed).

**Style:**

- Font: Patrick Hand (Google Font) throughout — load via `<link>` in `<head>`
- No boxes around step labels — text sits directly between the arc arrows, along the circle path
- Arrow style: short curved arcs following the circle perimeter, with open arrowheads
- Left circle uses warm red-brown tones (#B06040 arcs, #3D1A08 text)
- Right circle uses green tones (#5A8A5A arcs, #1A3A1A text)
- A vertical dashed divider (#C8B48A) separates the two circles
- Italic captions below each circle: "familiar, exhausting, useless" and "grounded, light, and yours"
- Centre of each circle holds a short italic label ("every year, unchanged" / "deepens over time")

**Left circle — "The usual story" (6 steps, clockwise):**

1. Funder asks for impact data
2. Cobble a rushed survey
3. Staff don't see the point
4. Bots & silence. Chase responses.
5. Data sits in a folder
6. No learning. Repeat.

**Right circle — "A better way" (5 steps, clockwise):**

1. Build a clear TOC for your program
2. What questions matter most?
3. Find data you already collect
4. Update your theory
5. A little smarter next year

### Content

**Beyond Surveys Consulting**
*Measure. Learn. Grow.*

---

**Build measurement capacity your organization actually owns**

Impact measurement matters. It helps you make better daily programming decisions, strengthens your grant applications, and keeps your organization growing. But for small organizations, accessing quality support has historically meant expensive consultants or going it alone.

I work specifically with small social service organizations in Southern Ontario — housing, mental health, harm reduction, food services, trauma-informed care, and basic needs — to build practical, affordable impact measurement systems. My goal isn't to make you dependent on me. It's to build your internal capacity so you can do this work yourselves. In fact, you can start for free right now by checking out my [free resources].

---

*[See my pricing tiers] — or [book a free consultation call] to figure out where to start.*

---

**Our approach**

I help organizations build measurement around a program-focused theory of change: starting with what your program is actually trying to do, identifying the key questions you need to answer to know if it's working, and then choosing the right tools to answer those questions.

Most organizations default to surveys when they think about impact measurement — and surveys have their place. But they're only one tool, and often not the most useful one. Poorly designed surveys produce data that looks useful but isn't. Survey fatigue is real: many people choose not to finish — or not to start. And the rise of online bots makes it increasingly difficult to tell valid responses from fake ones.

The good news is that most organizations are already sitting on rich sources of data they aren't fully using. Program records, attendance patterns, referral rates, case notes, service milestones — these can tell you a great deal about your operations and impact, often with less burden on the people you serve.

The goal is a measurement system you understand, you own, and you can grow without me.

[Common survey design mistakes →] | [Other ways to measure your impact →]

---

*[Mini bio card — see styling notes above]*

---

## 6. BEYOND SURVEYS — SERVICES PAGE

### `gretajames.ca/beyondsurveys/services.html`

### Styling notes

- Three track cards sit side by side on desktop, stacked on mobile
- Each card has consistent internal structure: title, italicised best-for line, short paragraph, bullet points, action links
- Use a subtle visual hierarchy: Track 1 can have a slightly more prominent border or header treatment; avoid making Track 3 look like a lesser option
- Add anchor IDs to each track card: id="track1", id="track2", id="track3" — these are linked from the Work With Me page
- "Not sure which track" CTA sits below the three cards, centered, visually separated
- In-Kind Support is its own section below, with a different background tone or clear dividing line

### Content

**Services**

I offer multiple ways to work together depending on your organization's needs, budget, and capacity. All tracks are designed with the same goal: to leave your organization more capable than when we started.

---

**Track 1 — Direct Consulting** {#track1}

*Best for organizations ready for dedicated, customized support*

Every organization's measurement challenges are different — and this track is designed to meet you where you are. Whether you're just starting to think about impact measurement or looking to strengthen an existing system, we'll scope the project together and build something that fits your context, your capacity, and your goals.

Past projects have included:

- Reviewing existing research to scope and design a new program
- Measuring the impact of an existing program
- Developing KPIs and dashboards for organization-wide performance tracking
- Designing shared measurement initiatives across multiple organizations

If you have something in mind that doesn't fit neatly into any of the above, reach out anyway — this track is built for flexibility and the best projects often start with an unusual question.

[Book a free consultation call →]

---

**Track 2 — Graduate Student Support** {#track2}

*Best for organizations with a defined project and a limited budget*

For organizations with a clear, scoped project and a limited budget, I can facilitate a connection with a graduate student researcher who will lead the work. I provide oversight and supervision throughout — you get quality support at a significantly reduced cost.

- I match you with a suitable graduate student and supervise the work
- The student works independently and sets their own fee or honorarium arrangement with your organization
- My fee covers the time I spend on supervision, guidance, and quality review
- Best suited to well-defined projects with realistic scope

---

**Track 3 — Self-Paced Workshops** {#track3}

*Best for organizations with little to no budget that want to build lasting internal capacity*

Free, openly available workshop content teaches evidence-based measurement methods you can apply directly to your own programs.

- All workshop content is free and openly available
- Work through the material at your own pace and apply it to your programs as you go
- Want support along the way? Guided application sessions are available to help you work through the content as it applies to your specific context (small cost)
- Prefer to learn with others? I periodically offer synchronous cohort-based courses in partnership with M4C — [join the M4C mailing list] to be notified of upcoming offerings
- Looking for a more tailored experience? Custom workshop delivery is available for organizations that want facilitated, team-based learning

---

**Not sure which track is right for you?**
[Book a free consultation call →] and we'll help you figure it out.

---

**In-Kind Support**

I believe that the organizations that most need good measurement support are often the least able to pay for it. A limited number of in-kind engagements are available each year for organizations that cannot access any of the above tracks due to financial constraints.

[Apply for in-kind support →]

---

## 7. BEYOND SURVEYS — LEARNING RESOURCES PAGE

### `gretajames.ca/beyondsurveys/learning.html`

### Styling notes

- The introductory description section should have a slightly different background tone or left border accent — signals philosophy/framing content rather than a clickable resource
- The TOC progression (scoping → strategy → assumptions → impact measurement) could optionally be rendered as a subtle four-step visual flow rather than prose — designer's discretion
- The "Having trouble applying this content" line should be a quiet callout — inline italic with linked text, not a banner
- Existing video content and coming soon placeholders should be visually distinct:
  - Existing content: complete, ready-to-use card styling
  - Coming soon: muted card with a "Coming soon" badge, no broken links
- The two-part series is grouped under one parent card; Session 1 and Session 2 are sub-items within it
- M4C attribution and "start with Session 1" note appear on the parent card
- Coming soon cards show title and description but replace the link with a "Coming soon" label
- Email signup for notifications should be visually prominent — a simple inline form or clearly styled link
- Design with expansion in mind — this page will grow significantly

### Content

**Learning Resources**

Every program starts with a theory of change — an idea about what problem you're solving, why your approach will work, and what success looks like. A program is only as strong as its theory of change, but most programs don't have them or they go unused.

These resources are designed to help you build a theory of change and understand how it shapes the measurement work you do. From there we start building measurement tools — without defaulting to surveys.

Are you still scoping the problem your program is trying to solve? You might need a literature review or some field research before you build anything. Have you identified the problem but aren't sure which strategy will work? Existing research or a small pilot might be your next step. Does your program rely on key assumptions about how change happens? Testing those assumptions directly may be more valuable than measuring outcomes right now. Is your program well-established and ready for rigorous impact measurement? That's where a solid evaluation framework and KPIs comes in.

Good measurement follows the program — not the other way around. These resources will help you figure out where you are, what questions matter most, and how to answer them using the full range of tools available to you — including many that don't involve surveys at all.

New modules are in development. [Sign up to be notified when new content is available →]

*Having trouble applying this content to your own program? [Track 3 guided application support] is designed for exactly that — or [reach out directly] if you'd like to talk it through.*

---

**Getting Started with Impact Measurement**
*In partnership with M4C — a working group of the Children and Youth Planning Table of Waterloo Region*

A two-part introductory series covering the core concepts of measuring program impact for community organizations. Developed and delivered in collaboration with M4C. **Start with Session 1** — Session 2 builds directly on the concepts introduced there.

*Session 1 — Introduction to Impact Measurement*
An introduction to quantitative measurement, what it means to measure your impact, and a practical exercise to help you begin applying these concepts to your own programs.
[Watch Session 1 →](https://www.youtube.com/watch?v=6cg1kBsFIQA)

*Session 2 — Building an Evaluation Framework* *(Requires Session 1)*
A hands-on session focused on developing an evaluation framework for your program — including how to articulate your program's goals, establish clear objectives, and build a framework to measure how effectively your program is achieving them.
[Watch Session 2 →](https://www.youtube.com/watch?v=NkPLikfO5gI)

---

**Coming Soon**

*Common Survey Design Mistakes* [Coming soon]
Learn the most common ways surveys go wrong — and how to avoid them. This module will help your organization assess whether an existing survey is giving you reliable data, and what to fix if it isn't.

*Other Ways to Measure Your Impact* [Coming soon]
Surveys are only one tool. This module walks through the rich sources of data most organizations already have — program records, service milestones, attendance patterns, case notes, administrative data, and more — and helps you identify which are most relevant to your program's key measurement questions.

---

## 8. BEYOND SURVEYS — PORTFOLIO PAGE

### `gretajames.ca/beyondsurveys/portfolio.html`

### Styling notes

- Each portfolio item is a card with consistent structure: title, organization/context line in italics, description paragraphs, italicised "This is an example of:" tag line at the bottom
- The tag line functions as a label — links each tag to the relevant service track on the Services page
- Cards should have clear visual separators but feel cohesive — consistent width, spacing, typographic treatment
- Example 2 and Example 5 have coming-soon components — display the full text content but show a clearly labelled placeholder where media will go
- Example 3 has a temporary notice (see below) — style it as a visually prominent highlighted box (amber/yellow background) so it is impossible to miss before publishing. Add an HTML comment: `<!-- REMOVE THIS NOTICE before going live — confirm permission with Food Bank of Waterloo Region first -->`
- Example 4 quotes should be styled as pull quotes — visually distinct, enough weight to draw the eye
- Portfolio page should expand cleanly as more examples are added
- On mobile, cards stack in the same order as below

### Content

**Portfolio**

The projects below are examples of the kinds of work I do. They span program scoping, KPI development, impact measurement, and capacity building — and are drawn from real organizations in Southern Ontario.

---

**Example 1 — Building an Organization-Wide KPI System**
*Marillac Place, Waterloo Region | Program Development & Evaluation Role*

Marillac Place is a transitional shelter serving pregnant and parenting mothers experiencing homelessness. Over several years in a program development and evaluation role, I built the organization's first agency-wide KPI system — including client retention, task completion, housing outcomes, and mental health indicators — and automated data collection through interactive Power BI dashboards to support real-time decision making.

The results were measurable: evidence-based program changes led to an 84% reduction in warnings issued to participants and a 200% increase in housing plan completion rates.

*This is an example of: [KPI development], [program evaluation], [data dashboards]*

---

**Example 2 — Scoping a Housing Program: From Hub to TIP**
*Marillac Place & the Side-by-Side Collaborative | Research to Support Program Design*

<!-- Coming soon: video presentation to be embedded here when ready -->

*[Video presentation in development — check back soon]*

The Side-by-Side Collaborative — comprising Marillac Place, Camino Wellbeing + Mental Health, and The Pregnancy Centre — was exploring how to improve housing supply and supports for young parents in Waterloo Region. I led the literature review component of a feasibility study that evaluated three housing models, drawing on evidence from Housing First research, the Family Options Study, and analysis of the local housing market.

The research found that a centralized housing hub was less effective than a scattered permanent housing approach, and contributed to the decision to pursue the Transition to Independence Program (TIP) — a lower-cost, higher-impact model that uses rental subsidies to incentivize homeowners to develop accessory dwelling units, increasing housing supply while housing individual families.

*This is an example of: [research to scope and support program design], [literature review], [housing and homelessness]*

---

**Example 3 — Measuring the Impact of the Market Dollars Program**
*The Food Bank of Waterloo Region | Graduate Student Supervision*

⚠️ **PERMISSION PENDING — DO NOT PUBLISH UNTIL CONFIRMED**
*Note: Included with permission, pending final confirmation from the Food Bank of Waterloo Region. Remove this notice and the HTML comment below before going live.*

<!-- REMOVE THIS NOTICE before going live — confirm permission with Food Bank of Waterloo Region first -->

The Food Bank of Waterloo Region runs the Market Dollars Pilot Program, a collaborative initiative providing households experiencing food insecurity with $100/month to spend on fresh food at the Kitchener Market. I connected a graduate student researcher with the organization and provided oversight throughout the project.

The student designed an experimental study to evaluate program impact, coordinated data collection with the Food Bank, analyzed behavioral data alongside participant surveys, and produced a final report. Key findings showed strong program uptake compared to regular programming and increased participant satisfaction. It also increased consumption of fruits and vegetables and home cooking.

*This is an example of: [graduate student facilitation], [program evaluation using behavioral data], [food security]*

---

**Example 4 — Building Measurement Capacity: Measurement 101**
*In partnership with M4C — a working group of the Children and Youth Planning Table of Waterloo Region*

Measurement 101 was a pilot course designed to help small nonprofits build their own internal measurement capacity. I developed and delivered the course, which used a hybrid model: asynchronous learning modules paired with synchronous sessions where participants applied course content to real measurement projects with support from graduate student mentors.

Fourteen organizations participated, representing a range of sectors including mental health, food security, literacy, and community foundations. All participants said they would recommend the course. Participants rated the course content, instructor support, and mentorship highly across the board.

What participants said:

> "[This course was] well paced and provided quality content and instruction that was very helpful to our agency and we left with a plan to move forward with."
> — Project READ

> "I'm so grateful for this course — it sharpened my impact measurement skills and shifted my mindset, showing that data isn't just for reporting, but for learning, growth, and real change driven by the voices of those we serve."
> — The Food Bank of Waterloo Region

> "Greta was very approachable and made the course content more accessible. She is very good at coming up with examples for new concepts."
> — Waterloo Region Community Foundation

*This is an example of: [workshop design and delivery], [measurement capacity building], [graduate student mentorship model]*

---

**Example 5 — Community Needs Survey**
*Marillac Place, Camino Wellbeing + Mental Health, and The Pregnancy Centre | Community Needs Assessment*

<!-- Coming soon: dashboard image to be inserted here -->

*[Dashboard image placeholder — assets/Community Needs Dashboard.jpg]*

The Community Needs Survey was a shared measurement tool developed across three organizations to measure the service needs of low-income families in Waterloo Region — including service access rates, prioritization of services, and barriers to access. I led all aspects of the project: stakeholder engagement, participant recruitment, ethics approval, survey design, data analysis, and final reporting. I also built interactive dashboards to share findings across partner organizations.

*This is an example of: [community needs assessment], [multi-organization data collection], [dashboards]*

---

## 9. BEYOND SURVEYS — WORK WITH ME PAGE

### `gretajames.ca/beyondsurveys/workwithme.html`

### Styling notes

- Three track entries as cards — consistent with Services page styling but more compact
- Each track card has action links as full-width rectangular buttons stacked vertically inside the card, each with a distinct background colour:
  - Primary colour: main enquiry/action link
  - Secondary colour: "More detail about this track" link
  - Tertiary colour: Learning Resources link (Track 3 only)
- Track 3 has three stacked action links: Learning Resources, More detail, Enquire — in that order
- "Not sure where to begin" sits below the three cards, visually separated, centered
- In-Kind Support section is visually prominent — a distinct bordered or shaded section, not buried. It should be easy to find.
- All enquiry links pass a source parameter via URL query string so form submissions are labelled by track in the email subject line

### Content

**Work With Me**

There are three ways to work with me. Select the track that best fits your organization's needs and budget.

---

**Track 1 — Direct Consulting**
Dedicated, customized support for organizations ready to tackle a measurement challenge end-to-end.

[More detail about this track →](gretajames.ca/beyondsurveys/services#track1)
[Enquire about Track 1 →](?source=beyondsurveys-track1)

---

**Track 2 — Graduate Student Support**
Supervised graduate student support for organizations with a defined project and a limited budget.

[More detail about this track →](gretajames.ca/beyondsurveys/services#track2)
[Enquire about Track 2 →](?source=beyondsurveys-track2)

---

**Track 3 — Support with Self-Paced Workshops**
Short 1:1 calls to provide extra support applying content from my self-paced workshops to your project. This track is also a good fit if you've attended one of my M4C measurement trainings and want follow-up consulting support.

[Go to Learning Resources →](gretajames.ca/beyondsurveys/learning)
[More detail about this track →](gretajames.ca/beyondsurveys/services#track3)
[Enquire about Track 3 →](?source=beyondsurveys-track3)

---

*Not sure which track is right for you?* **[Book a free consultation call →]**(?source=beyondsurveys-consult) *and we'll figure it out together.*

---

**In-Kind Support**

I believe the organizations that most need good measurement support are often the least able to pay for it. A limited number of in-kind engagements are available each year for organizations that cannot access any of the above tracks due to financial constraints. If that's you, I'd still like to hear from you.

[Apply for in-kind support →](?source=beyondsurveys-inkind)

---

## 10. CONTACT FORMS

All forms are handled via Formspree (free tier). Greta must create a Formspree account and obtain a form endpoint URL before go-live. Replace `YOUR_FORMSPREE_ENDPOINT` in all form action attributes with the actual endpoint.

All form submissions arrive at greta@gretajames.ca. The email subject line is set by the hidden `_subject` field, which is auto-populated based on the URL query string parameter passed from the Work With Me page.

---

### Form — Track 1, Track 2, Track 3, and Free Consultation Enquiry

*(shared form, subject line varies by source parameter)*

Fields:

- Name *(required)*
- Email *(required)*
- Organization name *(required)*
- Brief project description *(required, text area)*
- Hidden field: `_subject` — auto-populated based on source parameter:
  - beyondsurveys-track1 → "Beyond Surveys — Track 1 Enquiry"
  - beyondsurveys-track2 → "Beyond Surveys — Track 2 Enquiry"
  - beyondsurveys-track3 → "Beyond Surveys — Track 3 Enquiry"
  - beyondsurveys-consult → "Beyond Surveys — Free Consultation Request"

Confirmation message displayed on submission:
*"Thanks for reaching out. I'll be in touch within three to five business days."*

---

### Form — In-Kind Support Application

Fields:

- Name *(required)*
- Email *(required)*
- Organization name *(required)*
- Briefly describe your organization and the work you do *(required, text area)*
- Briefly describe the measurement support you're looking for *(required, text area)*
- Would your organization be open to support from a supervised graduate student if I am not available? *(required, radio buttons: Yes / No / Maybe)*
- Hidden field: `_subject` → "Beyond Surveys — In-Kind Application"

Confirmation message displayed on submission:
*"Thanks for applying. I review in-kind applications on a rolling basis and will be in touch if I'm able to help."*

---

### Technical notes for forms

- Use Formspree's free tier — no backend required, works with static GitHub Pages sites
- On submission, replace the form with the confirmation message in-place — no redirect to a separate thank-you page
- Track 3 support call booking: for now, link to `mailto:greta@gretajames.ca?subject=Track%203%20Support%20Call%20Request`
  - Add HTML comment: `<!-- TODO: replace with booking link when calendar integration is ready -->`
- Free consultation booking: same mailto approach for now, same TODO comment

---

## 11. IMAGES

All images are in the assets/ folder at the project root.

| Filename | Used on |
|----------|---------|
| Professional head shot.jpg | gretajames.ca About page (main photo), Beyond Surveys Home page (mini bio card) |
| Community Needs Dashboard.jpg | Portfolio page, Example 5 |

Additional images will be added to assets/ as the site develops. File paths are relative to the project root.

---

## 12. OPEN ITEMS — TO RESOLVE BEFORE GO-LIVE

- [ ] Create Formspree account and replace `YOUR_FORMSPREE_ENDPOINT` in all form action attributes
- [ ] Purchase gretajames.ca domain from Namecheap and point to GitHub Pages
- [ ] Set up professional email (greta@gretajames.ca) via Proton Duo once domain is purchased
- [ ] Confirm permission from Food Bank of Waterloo Region for Example 3 in Portfolio, then remove the permission notice and HTML comment
- [ ] Add calendar booking link for Track 3 support calls and free consultation calls when a calendar solution is in place (see TODO comments in HTML)
- [ ] Replace YouTube video placeholder links with final links once videos are confirmed as permanent
- [ ] Add email signup for Learning Resources notifications (placeholder link currently)
- [ ] Add M4C mailing list link on Services page Track 3 section (placeholder currently)
- [ ] Rename assets folder to lowercase `assets` if not already done (case-sensitivity on GitHub Pages Linux server)
- [ ] Review and remove all placeholder href="#" links before go-live

---

## 13. GRANTER'S ACADEMY — DESIGN SPEC

Granter's Academy lives at `gretajames.ca/grantersacademy`. It uses its own colour palette (slate blue accents) to distinguish it from Beyond Surveys, while sharing the parchment background and ink/deep-brown text so it reads as part of the same personal brand.

### Audience
Grantmakers, foundations, and funders — not non-profits.

### Colour Palette

| CSS variable | Role | Hex |
|---|---|---|
| `--parchment` | Page background (shared with hub) | `#FAF6EE` |
| `--linen` | Surface / card background | `#DDE4ED` |
| `--steel` | Accent / highlight | `#5B7B9A` |
| `--teal` | CTA / active accent | `#2E6B6B` |
| `--deep-brown` | Primary text / borders (shared) | `#7A5C2E` |
| `--ink` | Body text / headings (shared) | `#2C1F0E` |

### Typography
Same as hub and Beyond Surveys: Patrick Hand (display/accent), Georgia (body/headings).

### Navigation
Back-link only (`← Greta James`) until the full Granter's Academy site is built. No sub-page nav on the coming soon stub.

### Mailing list
Google Form: https://docs.google.com/forms/d/e/1FAIpQLSdKaW1pP4r-7bMNSxTxy89xDtkpKDXdKCNVglt3CjvsPl6NRQ/viewform?usp=header — use this URL anywhere a mailing list signup is linked.

### Current build status
`grantersacademy/index.html` — Coming soon stub page, built in Session 7. Full site is a separate future project.

---

## 14. FUTURE ADDITIONS (not in scope for initial build)

- Full Granter's Academy site — additional pages beyond the coming soon stub
- Learning modules as they are completed — slot into Learning Resources page
- Article on social service sector incentives — link from belief paragraph on About page
- Additional portfolio examples as projects are completed
- Professional photo update if needed
- Expanded bio or CV page if needed for EA-facing profile building
- Third project tab on hub page notebook graphic when a new project is ready to launch
