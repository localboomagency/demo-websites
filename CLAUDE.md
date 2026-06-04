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
| 1 | **Nav** | Logo/business name, 3–5 page-anchor menu links, phone number (click-to-call) |
| 2 | **Hero** | H1 + subheading + 3–4 benefit bullets + Google review widget + dual CTA — all above the fold |
| 3 | **Trust bar** | Fast-scan social proof: years trading, jobs done, review score, key accreditation |
| 4 | **Services** | What they offer — 3–6 cards with icon, name, short description |
| 5 | **Reviews** | Star rating, review count, 3 testimonial cards with name and location |
| 6 | **Why us / About** | Short differentiator copy — what makes them trustworthy and the best choice |
| 7 | **Contact / Quote form** | Simple form: Name, Phone, Email, Message — with a strong CTA heading |
| 8 | **Footer** | Address, phone, email, trading hours, 2–5 social icons (no links), copyright |

### 4. H1 format — service + location
For local business sites the H1 must capture the service and location so it reads like a search intent:

> "Plumbing Services in Bristol"
> "Yoga Studio in Exeter"
> "Family Dentist in Cheltenham"

The subheading under the H1 can be warmer and more persuasive.

### 4a. H1 location — Devon, UK
Unless the user specifies a different location, all demo sites must use a town or city in Devon, UK. Default to higher-population locations when no preference is given. Suitable defaults, in rough population order: Exeter, Plymouth, Torquay, Paignton, Barnstaple, Exmouth, Newton Abbot, Tiverton, Bideford, Sidmouth.

Examples from this project:
- Gym: "Independent Private Gym in Exeter"
- Bakery: "Artisanal Bakery in Plymouth City Centre"

If the user supplies a specific location (Devon or otherwise), use that instead.

### 5. Hero — above the fold
The entire hero must be visible without scrolling on both desktop (1280×800) and mobile (375×667). This means:
- Keep H1 font sizes confident but not oversized — `clamp(2rem, 5vw, 3.25rem)` is a safe ceiling for most sites
- Include 3–4 short benefit bullets (one line each, tick or icon prefix)
- Include the Google review widget (see rule 8)
- Both CTA buttons must be visible — no scrolling required

Reduce hero top/bottom padding if needed to fit everything. The goal is a complete, convincing first impression at a glance.

### 6. Dual CTA — phone + form
Every local business hero must have two CTAs:
- **Primary:** `Call us: 01234 567890` — a real `tel:` link, styled as the main button
- **Secondary:** `Get a Free Quote` — smooth-scrolls to the contact form

If no phone number is provided, use `01234 567890` as placeholder and note it clearly in a comment.

### 7. Nav menu links
The nav must include 3–5 menu links that scroll to sections on the page (e.g. `href="#services"`, `href="#reviews"`, `href="#contact"`). These should reflect the actual sections on the page. They are page-anchor links — not links to separate pages. Style them as normal nav items.

### 7a. Mobile nav — hamburger icon
On mobile (≤768px) the nav links hide and a hamburger icon button must appear on the right. The mobile header order left to right is: **logo | phone button | hamburger icon**.

Implementation pattern:
- Add `<button class="nav-hamburger" aria-label="Open menu">` with a 3-line SVG icon as the last child of `.nav-inner` (after the phone button)
- Default: `display: none`
- At 768px: show the hamburger (`display: flex`), switch `.nav-inner` to `display: flex; justify-content: space-between; align-items: center`, and reset `justify-self: auto` on `.nav-phone`
- The hamburger is a **visual placeholder only** — it does not need to open a dropdown in demo sites
- Style it to match the site's theme: no background, a border matching the nav's border colour, and `cursor: pointer`

### 8. Google review widget in the hero
Place a compact review widget inside the hero, above or below the benefit bullets but before the CTAs. It must include:
- The Google "G" logo (inline SVG, use the real Google brand colours: blue #4285F4, red #EA4335, yellow #FBBC05, green #34A853)
- Star rating rendered as filled gold stars (★)
- Review count and score (e.g. "4.9 · 214 reviews on Google")

If no real data is provided, invent a plausible score (4.7–4.9) and review count (80–400). Mark with `<!-- PLACEHOLDER: replace with real Google review data -->`.

### 9. Reviews section
**Always include a reviews/testimonials section.** If the client has not provided real reviews, use realistic placeholder data (believable UK names, specific and credible quote text, real-sounding locations). Mark placeholders with an HTML comment `<!-- PLACEHOLDER: replace with real reviews -->`.

### 10. Social icons in the footer
Include 2–5 social media icons in the footer. Use inline SVG for the icons (Facebook, Instagram, X/Twitter, LinkedIn, TikTok — pick what suits the business type). Do **not** add `href` attributes — leave them as decorative placeholder icons. Style them subtly, consistent with the footer palette.

### 11. No schema markup / structured data
Do not add JSON-LD or any structured data. These are demo sites — keep the code clean and focused on the visual design.

---

### 12. Container width consistency
Keep a single, consistent content container width across the page layout. The header, main content and footer must share the same centered container class (for example `.container`) with the same `max-width`, horizontal padding and alignment. Use full-bleed sections only when intentionally designed (e.g. background bands), but ensure inner content in those sections still aligns to the shared container.

Recommended CSS pattern:

```
.container { max-width: 1200px; margin: 0 auto; padding: 0 1rem; }
header .container, main .container, footer .container { /* same container, reused */ }
```

This keeps visual rhythm and ensures the logo, hero content, service cards, and footer information line up vertically across breakpoints.

### 13. No "back" links on demos
Do not add any "Back", "Back to demo", "Back to site" or similar links on individual demo pages. Demo pages are single-file homepages intended to stand alone; navigation within the page should use anchor links (e.g. `#services`, `#contact`) and the global index (`/`) will list all demos. Do not include links that encourage returning to the index — the index itself handles demo discovery.

### 14. Floating WhatsApp button
Every demo site must include a floating WhatsApp button fixed to the bottom-right of the viewport. It must:
- Stay in position on scroll (`position: fixed; bottom: 1.5rem; right: 1.5rem; z-index: 9999`)
- Use the official WhatsApp green (`#25D366`) as the background
- Contain the WhatsApp logo as an inline SVG (white icon on green circle)
- Link to `https://wa.me/[phone]` — use the business phone number with country code and no spaces/symbols (e.g. `https://wa.me/441234567890`). If no real number is provided, use `https://wa.me/441234567890` as a placeholder and mark with `<!-- PLACEHOLDER: replace with real WhatsApp number -->`
- Include a short visible label "WhatsApp" on desktop, hidden on mobile (use `display: none` below 480px)
- Have a `border-radius: 50px` pill shape (or `50%` if icon-only on mobile), a subtle `box-shadow`, and a smooth `:hover` lift effect (`transform: translateY(-2px)`)
- Be placed just before the closing `</body>` tag so it overlays all content

### 15. No emojis — SVG icons only
Never use emoji characters anywhere in demo sites. For decorative icons (service cards, class cards, contact detail rows, etc.), use inline SVG only. If a suitable SVG icon does not exist for the concept, omit the icon entirely rather than substituting an emoji.


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
- **No em dashes** — never use em dashes (—) in any generated copy. Use a comma, colon, or rewrite the sentence instead.

### Design inspiration
Reference screenshots are stored in the `reference/` folder at the project root, organised by business type:

```
reference/
  bakery/       ← bakery, café, deli, food retail
  gym/          ← gym, fitness studio, personal training
  plumber/      ← plumber, trades, home services
  general/      ← layout patterns, hero styles, typography — applies to any demo
```

When starting a new demo, check the relevant subfolder (and `general/`) for inspiration. Also ask the user if they have new examples to add. Use reference screenshots for layout, typographic mood, and colour direction — do not copy, use as inspiration.

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

### Location pill must match the H1
The `location` field in `sites.js` must be copied exactly from the location text used in the site's H1. For example, if the H1 reads "Artisanal Bakery in Plymouth City Centre", the location must be `'Plymouth City Centre'` — not just `'Plymouth'`. Check the H1 before registering the entry.

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

reference/                ← design inspiration screenshots (not web-served)
  bakery/
  gym/
  plumber/
  general/                ← layout / hero / typography patterns for any demo
```
