# Little Boracay — Astro + Cloudflare Pages

Official website for **littleboracay.com** — built with Astro, deployed on Cloudflare Pages via GitHub Actions.

## Stack
- **Framework:** [Astro](https://astro.build/) v4
- **Hosting:** [Cloudflare Pages](https://pages.cloudflare.com/)
- **CI/CD:** GitHub Actions (auto-deploy on push to `main`)
- **Integrations:** `@astrojs/sitemap`, `@astrojs/mdx`

---

## Local Development

```bash
npm install
npm run dev
```

Site runs at `http://localhost:4321`

---

## Build

```bash
npm run build
```

Output goes to `/dist`

---

## Deploy to Cloudflare Pages

### 1. Create Cloudflare Pages project

1. Log in to [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. Go to **Workers & Pages → Create → Pages**
3. Connect your GitHub repository
4. Set build settings:
   - **Framework preset:** Astro
   - **Build command:** `npm run build`
   - **Build output directory:** `dist`

### 2. Add GitHub Secrets

In your GitHub repo → Settings → Secrets and variables → Actions, add:

| Secret | Value |
|--------|-------|
| `CLOUDFLARE_API_TOKEN` | Your Cloudflare API token (with Pages:Edit permission) |
| `CLOUDFLARE_ACCOUNT_ID` | Your Cloudflare Account ID |

**To get your Cloudflare API Token:**
1. Go to [dash.cloudflare.com/profile/api-tokens](https://dash.cloudflare.com/profile/api-tokens)
2. Click **Create Token**
3. Use **Edit Cloudflare Workers** template OR create custom token with `Pages: Edit` permission
4. Copy token into GitHub secret

**To get your Account ID:**
- Found in Cloudflare Dashboard right sidebar, or URL: `dash.cloudflare.com/<ACCOUNT_ID>`

### 3. Push to main

Every push to `main` automatically builds and deploys to Cloudflare Pages.

---

## Site Structure

```
src/
  layouts/
    BaseLayout.astro       # SEO head, OG tags, schema, shell nav/footer
                           # Pass noShell={true} to skip shell (used by index)
  pages/
    index.astro            # ★ SINGLE-PAGE SITE — all sections with #anchor nav
                           #   Sections: #hero #about #activities #visit
                           #            #reviews #faq #contact
                           #   Includes: Plan Your Visit form + Contact form
    visit.astro            # Standalone travel guide (blog/SEO use)
    sandbar.astro          # Sandbar deep-dive page
    cottages.astro         # Floating cottages page
    about.astro            # About page
    faq.astro              # Full FAQ with schema markup
    blog/
      index.astro          # Blog listing
      how-to-get-to-little-boracay.astro  # Key SEO blog post
  styles/
    global.css             # Global styles + BaseLayout shell utilities
public/
  logo.png                 # Little Boracay circular logo
  favicon.svg
  robots.txt
.github/
  workflows/
    deploy.yml             # Auto-deploy to Cloudflare Pages on push to main
```

## Single-Page Navigation

The homepage (`index.astro`) is a **single-page site** using `#anchor` links for all navigation:

| Section | Anchor | Content |
|---------|--------|---------|
| Hero | `#hero` | Full-width hero with logo, headline, stats |
| About | `#about` | Destination info + quick facts card |
| Activities | `#activities` | 6 activity cards |
| Plan a Visit | `#visit` | Step-by-step guide + Plan Your Visit form |
| Reviews | `#reviews` | TripAdvisor reviews + ratings card |
| FAQ | `#faq` | 8 FAQs with schema markup |
| Contact | `#contact` | Contact channels + Contact form |

All nav links, footer links, and CTAs use `href="#section"` with smooth-scroll JS.

---

## SEO / AEO / GEO Features

- ✅ Full structured data (TouristAttraction, FAQPage, HowTo, Article schemas)
- ✅ Open Graph + Twitter Card meta tags
- ✅ Geo meta tags (region, placename, coordinates)
- ✅ Auto-generated XML sitemap via `@astrojs/sitemap`
- ✅ Robots.txt with sitemap reference
- ✅ Speakable content markup for AI assistant citation
- ✅ Canonical URLs on every page
- ✅ Mobile-responsive design
- ✅ Semantic HTML with proper heading hierarchy
- ✅ Fast Cloudflare CDN delivery (Core Web Vitals optimized)

---

## Adding New Blog Posts

Create a new `.astro` file in `src/pages/blog/`:

```astro
---
import BaseLayout from '../../layouts/BaseLayout.astro';
---
<BaseLayout title="Post Title" description="Post description">
  <!-- Article content -->
</BaseLayout>
```

Then add it to the blog index in `src/pages/blog/index.astro`.

---

## Custom Domain

1. In Cloudflare Pages → Your project → Custom domains
2. Add `littleboracay.com` and `www.littleboracay.com`
3. Cloudflare will handle DNS automatically if domain is on Cloudflare

---

## Support

For destination information: [facebook.com/littleboracay](https://facebook.com/littleboracay)
For visitor community: [facebook.com/groups/littleboracay](https://facebook.com/groups/littleboracay)
