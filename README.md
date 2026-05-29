# Web Design Agency — Demo Sites

A portfolio of demo websites built with [Astro](https://astro.build). Each demo lives at its own path and is fully independent. The home page (`/`) shows a card grid of all demos.

## Running locally

```bash
npm install
npm run dev
```

Then open [http://localhost:4321](http://localhost:4321) in your browser.

## How to add a new demo site

### Step 1 — Create the page file

Create a new folder inside `src/pages/` with your demo name, then add an `index.astro` file inside it:

```
src/pages/restaurant/index.astro
```

Copy the structure from an existing demo (e.g. `src/pages/bakery/index.astro`) and customise it. Each demo is fully self-contained — you can use any fonts, colours, or layout you like.

### Step 2 — Add a screenshot

Take a screenshot of your demo site and save it as a `.jpg` (or `.png`, `.svg`) inside:

```
public/screenshots/restaurant.jpg
```

Recommended screenshot size: **1600 × 1000px** (or any 16:10 ratio).

### Step 3 — Register it in the data file

Open `src/data/sites.js` and add a new entry:

```js
export const sites = [
  { name: 'The Artisan Bakery', path: '/bakery',     screenshot: '/screenshots/bakery.svg' },
  { name: 'Peak Performance Gym', path: '/gym',       screenshot: '/screenshots/gym.svg'    },
  { name: 'La Cucina',           path: '/restaurant', screenshot: '/screenshots/restaurant.jpg' }, // ← add this
];
```

That's it. The home page will automatically show the new card.

## Where to put screenshots

All screenshots go in `public/screenshots/`. They are served at `/screenshots/filename.jpg` in the browser.

- Use `.svg` for placeholder/generated images
- Use `.jpg` or `.png` for real screenshots
- Update the `screenshot` field in `src/data/sites.js` to match the filename you used

## Deploying to Cloudflare Pages

### Build settings (enter these in the Cloudflare Pages dashboard)

| Setting | Value |
|---|---|
| **Build command** | `npm run build` |
| **Build output directory** | `dist` |
| **Node.js version** | `20` (set under Settings → Environment variables as `NODE_VERSION = 20`) |

### Steps

1. Push this repo to GitHub
2. Go to [Cloudflare Pages](https://pages.cloudflare.com) → Create a project → Connect to Git
3. Select your repository
4. Enter the build settings from the table above
5. Click **Save and Deploy**

Cloudflare Pages will build and deploy automatically on every push to your main branch.
