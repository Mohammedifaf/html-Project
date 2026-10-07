# IfafWebStudio — SEO & GEO upgrade (V9)

The website is in [`IfafWebStudio/`](IfafWebStudio/). Deploy **that folder** as the site root (Netlify / Cloudflare Pages "publish directory", or upload its contents to `public_html` on cPanel/Hostinger).

Local preview: `cd IfafWebStudio && python3 -m http.server 8000`, then open http://localhost:8000/. Links now use clean folder URLs (`/services/`, `/work/` …), so double-clicking `index.html` from a file manager will not navigate correctly. Use a local server.

---

## What was changed on the website

### Technical SEO
- **Internal links fixed.** Every page used to link to `services.html`, `portfolio.html` and other old URLs that 301-redirect to the canonical clean URLs, which wastes crawl budget and link equity. All links now point straight to `/services/`, `/work/`, `/about/` and `/contact/`.
- **Duplicate pages removed.** The root `services.html`, `portfolio.html`, `about.html` and `contact.html` copies were deleted, and the redirects in `_redirects` and `.htaccess` still catch old links.
- **`.htaccess` added.** The README said it existed, but it was missing. It forces HTTPS and non-www, redirects old URLs and `/index.html`, sets the 404 page, and adds compression and browser caching.
- **`_headers`** for Netlify and Cloudflare: caching and security headers.
- **`sitemap.xml`** now lists all 12 pages with `lastmod`.
- **`404.html`** added: noindex, with links back into the site.
- **Core Web Vitals:**
  - The hero image now loads first (`fetchpriority="high"`; it was lazy-loaded before, which hurt LCP).
  - `preconnect` added for remote image hosts.
  - AMB Guest House images now use responsive AVIF/WebP `<picture>`. The AVIF files existed but were never used.
- Titles and H1s now include the target keywords (Manipal, Udupi, service names), and every title and description is unique and the right length.
- Added `x-default` hreflang, `aria-current` on the nav and breadcrumbs, and a `tel:` link.

### Structured data (schema.org)
- Business entity now includes:
  - geo coordinates and PIN code
  - `priceRange` and `knowsAbout`
  - `alternateName` ("Ifaf Web Studio")
  - logo `ImageObject`
  - a service catalogue linked to the new service pages
- Every page now has a linked `WebPage`, `BreadcrumbList`, `dateModified` and `primaryImageOfPage`.
- Each new page has its own `Service` schema with area served, audience and contact channel.
- **The FAQ schema now matches the visible FAQ.** Before, the homepage schema had 9 questions but only 4 were visible on the page, which breaks Google's guidelines.
- About page is now `AboutPage` + `ProfilePage` with Mohammed Ifaf as `mainEntity`. Portfolio uses an `ItemList` of the live `WebSite` projects.

### GEO / AEO (visibility in ChatGPT, Gemini, Perplexity, Google AI Overviews, Claude)
- **`robots.txt`** explicitly allows AI crawlers:
  - GPTBot, OAI-SearchBot and ChatGPT-User
  - ClaudeBot and Claude-SearchBot
  - PerplexityBot
  - Google-Extended and Applebot-Extended
  - Bingbot and others
- **`llms.txt`** rewritten in the standard format: a summary, key facts, and links to every page and project.
- **`llms-full.txt`** (new): plain-text content of every page, so AI assistants can read the whole site in one request.
- **"In short" answer blocks** on every new page: one factual paragraph naming the studio, founder, location and services, which is easy for an AI to quote.
- **"At a glance" facts section** on the About page.
- Clear definitions of GEO and AEO on the SEO page, and question-style FAQs on every page.

### New keyword-targeted pages (7)
These pages are the main driver for growing traffic, because each one targets a search that the old 5-page site could not rank for:

| Page | Targets searches like |
|---|---|
| `/services/hotel-resort-website-development/` | hotel / resort / homestay website Manipal, Udupi |
| `/services/restaurant-website-qr-menu/` | restaurant website, QR menu Manipal / Udupi |
| `/services/taxi-travel-website-development/` | taxi / travel website developer |
| `/services/local-seo-google-business-profile/` | local SEO, Google Business Profile, GEO, AEO Manipal |
| `/services/ai-chatbot-whatsapp-automation/` | AI chatbot, WhatsApp automation for business |
| `/services/wordpress-website-development/` | WordPress website developer, website redesign |
| `/website-developer-udupi/` | website developer / web designer in Udupi |

All the new pages are linked from the homepage, the Services page, the portfolio and the footer. Their content uses only facts already on your site, with no invented reviews, numbers or awards.

> **Please check:**
> - The pricing answer ("budget ranges from ₹20,000–₹30,000 upward") and the schema `priceRange: ₹20,000+` come from your contact form's budget options. Edit them if that's not right.
> - Business coordinates are set to central Manipal (13.35, 74.79).

---

## V10 fixes after the SEOptimer audit (Links F, Usability D)

**Fixed in the code**
- **`vercel.json` added.** Vercel ignores `_redirects`, `_headers` and `.htaccess`, so the redirects, trailing slashes, caching and security headers now also work on Vercel.
- **Email privacy.** The email address no longer appears as plain text in the page source, which SEOptimer flags as a spam risk. It is HTML-encoded and still shows and clicks normally for visitors.
- **Tap targets and font sizes.** Footer, breadcrumb and text links have 44px+ touch areas on phones, and small labels are at least 12px on mobile.
- **Mobile footer bug.** The "© 2026" line no longer breaks onto three lines.
- **Faster mobile images.** Unsplash images now load a 480/800/1200px version that fits the screen, instead of always loading 1000–1500px. CSS is properly minified.

**Links = F is about backlinks, not code.** SEOptimer grades how many other websites link to yours. A new site on `*.vercel.app` has almost none, so it gets an F whatever the code does. To raise it:
1. Add "Website by IfafWebStudio" with a link on all 5 client websites (the fastest win).
2. Create a Google Business Profile, a LinkedIn company page, a Facebook page, and Justdial / Sulekha / Clutch / GoodFirms listings, all linking to your site.
3. Link the website from your Instagram bio.

**Connect your real domain in Vercel.** The site is currently audited at `ifafwebstudiocom-omega.vercel.app`, but every page tells Google the official address is `https://ifafwebstudio.com/`.
- If you own `ifafwebstudio.com`, go to Vercel → Project → Settings → **Domains**, add `ifafwebstudio.com` and `www.ifafwebstudio.com` (set www to redirect to the main one), then update the DNS records Vercel shows you.
- Then run SEOptimer on `https://ifafwebstudio.com`, not the vercel.app address.
- Backlinks also need to point at your real domain to count.
- If you use a different domain, tell me and I'll update every canonical URL, the sitemap and llms.txt.

**Social and analytics (shown in SEOptimer's Social and Technology sections).**
- Link real Facebook, LinkedIn and YouTube profiles if you have them; send them to me and I'll add them to the footer and schema.
- Turn on **Vercel Web Analytics** (Project → Analytics) or create a Google Analytics 4 property and send me the `G-XXXX` ID to add.

---

## What YOU need to do next (off-site, these matter as much as the code)

### This week
1. **Google Search Console:**
   - Add `https://ifafwebstudio.com` and verify it.
   - Submit `https://ifafwebstudio.com/sitemap.xml`.
   - Use "URL inspection → Request indexing" for the homepage and the 7 new pages.
2. **Bing Webmaster Tools:** import from Search Console and submit the sitemap. ChatGPT search and Copilot use Bing's index, so this matters a lot for GEO.
3. **Google Business Profile.** This is the single biggest local ranking factor.
   - Create or claim the profile with category "Website designer" (secondary categories: "Internet marketing service", "Marketing agency").
   - Use exactly the same name, phone and location as the website: IfafWebStudio · +91 96860 44715 · Manipal, Karnataka.
   - Add services, photos, the website link and a description.
   - Then **add the profile URL to `sameAs` in the schema**: search for `"sameAs":["https://www.instagram.com/ifafwebstudio/"]` in the HTML files and add the Google Maps link.
4. **If you use Cloudflare:** check Security → Bots and turn **off** "Block AI bots / AI Scrapers". Otherwise ChatGPT, Perplexity and Claude can't read the site, even with the new robots.txt.

### Next 1–3 months
5. **Reviews:** ask every past client (East West Travels, AMB Guest House, Island Resort, Golden Riveria, EazyRide Cab) for a Google review. Reviews drive both local SEO and AI recommendations.
6. **Backlinks from your own work:** add a footer credit "Website by IfafWebStudio" linking to `https://ifafwebstudio.com/` on all 5 client sites. These are relevant, easy and powerful links.
7. **Citations:** list the business with the identical name, phone and address on:
   - Justdial, Sulekha, IndiaMART
   - Bing Places, Apple Business Connect
   - LinkedIn (company page + Mohammed Ifaf's profile)
   - Facebook page, Clutch / GoodFirms

   Then add those profile URLs to `sameAs` too. Consistent mentions across the web are what AI engines use to trust an entity.
8. **Content:** publish case-study pages for each portfolio project (the problem, what was built, screenshots, client quote) and short guides people actually ask about, such as "How much does a website cost in Udupi?" and "Hotel website vs OTA listing". Fresh, specific, factual content is what gets cited in AI answers.
9. **Instagram & social:** post your projects regularly and link back to the matching service page.
10. **Track it:**
    - Search Console → Performance shows queries and pages.
    - Re-test monthly by asking ChatGPT, Perplexity and Gemini "best website developer in Manipal / Udupi".

### When you edit the site later
- Keep the name, phone and address identical everywhere: website, schema, Google Business Profile and directories.
- When you add a page, add it to `sitemap.xml`, `llms.txt` and the footer.
- Update `dateModified` in the page's JSON-LD and `lastmod` in the sitemap when content changes.
- Validate structured data at https://validator.schema.org/ and https://search.google.com/test/rich-results.
