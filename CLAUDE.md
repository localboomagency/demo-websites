# Web Design Agency — Demo Sites Platform

## What this project is

A portfolio of demo websites built with Astro. Each demo lives at its own path (e.g. `/bakery`, `/gym`, `/plumber-bristol`) and is completely self-contained. The home page (`/`) shows a card grid of all demos, driven by `src/data/sites.js`.

---

## Rules for building demo sites

### 1. Home page only
Each demo is a **single home page** — one `index.astro` file inside `src/pages/[demo-name]/`. Do not create additional pages (no /about, /contact, /services pages). Everything the visitor needs must be on the home page.

### 2. Always ask before building
Before writing any code for a new demo site, ask the user these questions in order:

1. **Is this a real business or a generic demo?** (affects copy tone and placeholders used)
2. **Do you have any data to help build the site?** Prompt specifically for:
   - Business name
   - Location / service area (town, city, county)
   - Phone number
   - Email address
   - Services offered
   - Years in business / founding year
   - Number of jobs completed or customers served
   - Review count and star rating (e.g. "142 Google reviews, 4.9★")
   - Any accreditations, certifications, or trust badges
   - Tagline or any existing copy they like
   - Images (see image placement below)

### 3. CRO-first structure
All local business sites should be optimised for conversion. Use this section order:

| # | Section | Purpose |
|---|---|---|
| 1 | **Nav** | Logo/business name, phone number (click-to-call), optional "Get a Quote" button |
| 2 | **Hero** | H1 + subheading + dual CTA (call button + scroll-to-form) |
| 3 | **Trust bar** | Fast-scan social proof: years trading, jobs done, review score, key accreditation |
| 4 | **Services** | What they offer — 3–6 cards with icon, name, short description |
| 5 | **Reviews** | Star rating, review count, 3 testimonial cards with name and location |
| 6 | **Why us / About** | Short differentiator copy — what makes them trustworthy and the best choice |
| 7 | **Contact / Quote form** | Simple form: Name, Phone, Email, Message — with a strong CTA heading |
| 8 | **Footer** | Address, phone, email, trading hours, copyright |

### 4. H1 format — service + location
For local business sites the H1 must capture the service and location so it reads like a search intent:

> "Plumbing Services in Bristol"
> "Yoga Studio in Exeter"
> "Family Dentist in Cheltenham"

The subheading under the H1 can be warmer and more persuasive.

### 5. Dual CTA — phone + form
Every local business hero must have two CTAs:
- **Primary:** `Call us: 01234 567890` — a real `tel:` link, styled as the main button
- **Secondary:** `Get a Free Quote` — smooth-scrolls to the contact form

If no phone number is provided, use `01234 567890` as placeholder and note it clearly in a comment.

### 6. Reviews section
**Always include a reviews/testimonials section.** If the client has not provided real reviews, use realistic placeholder data (believable UK names, specific and credible quote text, real-sounding locations). Mark placeholders with an HTML comment `<!-- PLACEHOLDER: replace with real reviews -->`.

### 7. No schema markup / structured data
Do not add JSON-LD or any structured data. These are demo sites — keep the code clean and focused on the visual design.

---

## Quality bar — visual design

Every site should look **genuinely impressive and professionally designed**. The goal is for a prospective client to look at the demo and think: *"I want that — this is better than everything my competitors have online."*

Standards to hit:
- Typography that feels intentional: strong font pairing, clear hierarchy, considered sizing
- Colour palette that suits the business type — not generic, not safe
- Generous whitespace — do not crowd elements
- Subtle depth: shadows, borders, background layering — not flat, not overdone
- Hero sections that feel big and confident
- Mobile responsive — test mentally at 375px and 1280px
- No generic stock photo vibes in the copy or layout — write as if there's a real brand behind it

### Design inspiration
The user maintains a folder of reference websites outside this project. When building a new demo, ask if they have any relevant examples to share. Reference them for layout, typographic mood, and colour direction — do not copy, use as inspiration.

---

## Images

### Where to place site-specific images
When the user provides images for a demo site, place them at:

```
public/images/[demo-name]/hero.jpg
public/images/[demo-name]/about.jpg
public/images/[demo-name]/service-1.jpg
```

Reference them in the page as `/images/[demo-name]/filename.jpg`.

### When no images are provided
Use CSS backgrounds (gradients, solid colours) or a clearly commented placeholder div. Do not hotlink external images. Write the layout so images can be dropped in later without restructuring the HTML.

---

## Adding a new demo to the index

After building a demo, register it in `src/data/sites.js`:

```js
{ name: 'Business Name', path: '/demo-name', screenshot: '/screenshots/demo-name.svg' }
```

Screenshot placeholder SVGs are stored in `public/screenshots/`. When the user takes a real screenshot they update the filename in `sites.js`.

---

## Folder structure reference

```
src/
  data/
    sites.js              ← register all demo sites here
  pages/
    index.astro           ← home page / card grid
    [demo-name]/
      index.astro         ← one file per demo, fully self-contained

public/
  screenshots/            ← card thumbnails for the index page
  images/
    [demo-name]/          ← images provided by the user for a specific demo
```
