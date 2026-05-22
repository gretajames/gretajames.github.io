# CLAUDE.md — Session Instructions for Claude Code

This file is automatically read at the start of every session. Follow all instructions here exactly.

---

## Session Start Protocol

1. Ask the user to read `project-notes.md` (build log) **only if they haven't provided orientation already**. If `project-notes.md` has already been read this session, use the version in context — do not re-read it.
2. Give the user a token budget estimate: state roughly how many tokens have been used so far and how many remain, then recommend activities that fit within the budget, reserving ~35–40k tokens for wrap-up at the end.
3. Before building any specific page, read only the relevant section of `project-spec.md` using offset/limit (see Section Index below). Do not re-read sections already in context this session.

---

## Design Cheat-Sheet

> **Sync warning:** These values mirror Sections 2–3 of `project-spec.md`. If the palette, typography, or nav structure ever changes, update both this file and `project-spec.md`.

### Colour Palette

| Role | Name | Hex |
|------|------|-----|
| Page background | Parchment | #FAF6EE |
| Surface / card background | Warm cream | #E8D9B5 |
| Accent / highlight | Amber brown | #C8A96A |
| Primary text / borders | Deep brown | #7A5C2E |
| CTA / active accent | Quiet green | #4A6B4A |
| Body text / headings | Ink | #2C1F0E |

### Typography

- **Display/accent:** Patrick Hand (Google Font) — lifecycle graphics, pull quotes, handwritten-style elements
- **Body/headings:** Georgia (serif)
- Never use Inter, Arial, Roboto, or other generic sans-serif system fonts

### Navigation

- **Hub navbar:** `About | Beyond Surveys Consulting | Granter's Academy`
- **Beyond Surveys navbar:** `← Greta James` (back-link, left, hides at ≤ 760px) + `Home | Services | Learning Resources | Portfolio | Work With Me` (right)

### Layout Container

All pages use `.container { max-width: 1040px; margin: 0 auto; padding: 0 1.75rem; }`. Never use a narrower max-width — earlier sessions used 740px or 860px but all pages have since been updated to 1040px.

### Shared CSS

All Beyond Surveys pages load `beyondsurveys/style.css` as their first stylesheet. Page-specific styles go in a `<style>` block in `<head>` after the shared stylesheet link.

---

## Current Build Status

> **Sync warning:** Update this section during every session wrap-up. It mirrors the most recent BUILD LOG entry in `project-notes.md` — keep them in sync.

As of Session 10 (2026-05-22):

| File | Status |
|------|--------|
| `index.html` | Complete (hub page) — belief callout updated to two-bullet format with project links; green callout visually extends into projects section via callout-extension div |
| `beyondsurveys/style.css` | Complete (shared stylesheet) |
| `beyondsurveys/index.html` | Complete including SVG lifecycle graphic |
| `beyondsurveys/services.html` | Complete |
| `beyondsurveys/learning.html` | Complete |
| `beyondsurveys/portfolio.html` | Complete — permission notice removed from Food Bank card; Housing card hidden (video pending); expand/collapse click hints added |
| `beyondsurveys/workwithme.html` | Stripped to form only — may want a brief intro line above the form heading |
| `beyondsurveys/inkind.html` | Complete (standalone, not in navbar) |
| `grantersacademy/index.html` | Complete (coming soon stub) — tagline placeholder left in code |

---

## Next Session Prompt

- `beyondsurveys/workwithme.html` is now just the Get in Touch form. Consider whether to add a brief title or intro sentence above the form heading to orient visitors who land there directly.
- Granter's Academy tagline: add `<p class="hero-tagline">` in `grantersacademy/index.html` when a tagline is ready (CSS stub already commented in the file).
- All pre-go-live checklist items remain open (Formspree endpoint, domain purchase, email setup, M4C mailing list link, calendar booking link).

---

## Session Wrap-Up Protocol

When approximately 85–90% of the token budget has been used, proactively say:

> "We're approaching wrap-up — here's what we completed today: [list]. Ready to do the three wrap-up steps?"

Then complete the three steps in order:

### Step 1 — Commit to GitHub
Stage all changed/new files and commit with a descriptive message summarizing what was built this session.

### Step 2 — Update `project-notes.md`
Add a new BUILD LOG entry at the top of the log (below the header, above the previous session) with:
- Today's date and session number
- What was completed
- Any design decisions made that aren't already in `project-spec.md`
- Anything still in progress or needing attention

### Step 3 — Update `build-process.md`
Add plain-English documentation for everything built today, covering:
- Site architecture decisions
- Tech choices
- Component descriptions
- A how-to-change guide for common edits

### Step 4 — Update CLAUDE.md
Update the **Current Build Status** table and any other stale content in this file to reflect the session's work.

---

## project-spec.md Section Index

When building a specific page, read only the relevant section using offset/limit. Do not read the whole file.

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

## General Efficiency Rules

- Never re-read a file already in context this session.
- Use parallel tool calls where possible (e.g., reading a spec section while checking an existing file simultaneously).
- Keep code simple, well-commented, and self-maintainable — Greta is the content owner, not a developer.
- File paths must be relative and lowercase (GitHub Pages is case-sensitive on Linux).
- Never use a framework, build tool, or backend dependency.

---

## Collaboration Preferences

- Explain design decisions before implementing — Greta wants to understand choices as they're made.
- Build in stages; confirm with Greta at each stage before proceeding.
- Keep explanations brief but complete.
- If anything in the spec is ambiguous or missing, ask before building — don't guess.
