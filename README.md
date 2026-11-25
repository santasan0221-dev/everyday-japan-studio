# Everyday Japan Studio — website

A plain static HTML/CSS site (no build step, no external assets) for the
Everyday Japan Studio Gumroad shop: a product index plus free articles drawn
from the same verified research as the guides.

## Files

| File | Purpose |
|---|---|
| `index.html` | Shop intro + product grid + article index |
| `style.css` | The one shared stylesheet |
| `tax-free-refund-2026.html` | Article: the refund-style tax-free system |
| `jr-pass-worth-it.html` | Article: JR Pass break-even math |
| `onsen-with-tattoos.html` | Article: tattoos at onsen — house rule, not law |
| `goshugi-amounts.html` | Article: wedding cash gift amounts |
| `ho-ren-so.html` | Article: the ho-ren-so reporting system |
| `izakaya-otoshi.html` | Article: the otoshi seat charge |
| `sitemap.xml` / `robots.txt` / `feed.xml` | SEO + RSS |
| `.github/workflows/pages.yml` | GitHub Pages deployment (Actions source) |

## ⚠ URLs assume a specific repo name — check before deploying

All canonical URLs, the sitemap, `robots.txt` and the RSS feed are written for:

```
https://santasan0221-dev.github.io/everyday-japan-studio/
```

That means the GitHub repository must be named **`everyday-japan-studio`**
under the account **`santasan0221-dev`** for the URLs to be correct as-is.

If you use a different repo name (or a custom domain), update the base URL in
every file first:

```bash
grep -rl "santasan0221-dev.github.io/everyday-japan-studio" . | \
  xargs sed -i 's#santasan0221-dev.github.io/everyday-japan-studio#YOUR-NEW-BASE#g'
```

(Replace `YOUR-NEW-BASE` with e.g. `santasan0221-dev.github.io/my-repo` or
your custom domain, without a trailing slash.)

## Deployment steps (GitHub Pages)

1. **Create a public repository** named `everyday-japan-studio` on GitHub
   (github.com/new). Do not initialise it with a README — this folder already
   has one.
2. **Push this folder** to it:

   ```bash
   cd everyday-japan-site
   git init
   git add .
   git commit -m "Everyday Japan Studio site"
   git branch -M main
   git remote add origin https://github.com/santasan0221-dev/everyday-japan-studio.git
   git push -u origin main
   ```

3. **Enable Pages with the Actions source:** in the repo, go to
   **Settings → Pages → Build and deployment → Source: GitHub Actions**.
   (Do *not* pick "Deploy from a branch" — the workflow in
   `.github/workflows/pages.yml` does the publishing.)
4. **Wait for the workflow:** the **Actions** tab shows a
   "Deploy static site to GitHub Pages" run; when it is green, the site is
   live at `https://santasan0221-dev.github.io/everyday-japan-studio/`.
   Every later push to `main` redeploys automatically.

## After it is live (optional but recommended)

- **Verify the pages render:** open the home page and one article; check the
  stylesheet loads (colours/fonts) and that article links work.
- **Google Search Console:** add a property for the site URL, verify
  ownership (the HTML-tag method: paste the meta tag into `index.html`'s
  `<head>`, push, then verify), and submit `sitemap.xml` under
  **Sitemaps**. This is what gets the articles indexed.
- **When the three "coming soon" guides are published on Gumroad,** replace
  their cards in `index.html` with linked cards (same pattern as the others)
  and update the CTAs at the bottom of `goshugi-amounts.html` and
  `ho-ren-so.html` to point at the product pages.
- **When facts change** (pass prices, tax-free rules, facility policies),
  update the affected article and its `<lastmod>` in `sitemap.xml`, and the
  item order/dates in `feed.xml` if you add new articles.

## Content rules for this site

- Facts come only from the verified product manuscripts; sources are the
  official Japanese ones listed inside the guides.
- No testimonials, ratings, sales figures or review claims — none exist to
  quote, and none may be invented.
- Articles are original prose, not excerpts of the paid guides; each article
  ends with a clearly-labelled CTA to our own product.
