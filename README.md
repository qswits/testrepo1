# Quick Smart Wash — SEO Audit

Date: 2026-02-09

## Executive summary

- **Snapshot:** Project includes site-level metadata and Organization JSON-LD in `src/app/layout.js`, a sitemap at `public/sitemap.xml`, and an open `robots.txt` in `public/robots.txt`.
- **Primary opportunities:** unique page metadata & canonicals, image optimisation (enable Next image), richer structured data (Service, Breadcrumb, FAQ, Article), Core Web Vitals improvements (LCP/CLS/INP), targeted content & internal linking, and local SEO (LocalBusiness markup + Google Business Profile).

## Scope & methodology

- Files inspected: `src/app/layout.js`, `src/app/page.js`, `src/components/Header.jsx`, `public/robots.txt`, `public/sitemap.xml`, `public/manifest.json`, `next.config.mjs`, `package.json`, and `Actual_Website_Content.md`.
- Recommendations combine technical checks, content & keyword guidance, on-page schema and prioritized implementation tasks.

## Technical SEO findings & fixes (actionable)

- **Site metadata:** Good site-level metadata exists in `src/app/layout.js`. Action: make metadata page-specific (title, description, OG, twitter) for every route.
- **Canonical tags:** Add `<link rel="canonical">` to every page to normalize URLs (account for `trailingSlash: true`).
- **Sitemap:** `public/sitemap.xml` lists major pages. Recommendation: generate and auto-update sitemap (especially for blog posts) and submit to Google Search Console and Bing Webmaster Tools.
- **Robots:** `public/robots.txt` allows crawling — keep this and ensure no accidental `noindex` meta tags.
- **Images:** `next.config.mjs` currently uses `images.unoptimized: true` — disable that to use Next Image optimization and configure allowed domains or use the built-in loader to serve WebP/AVIF and reduce LCP.
- **Server & caching:** Ensure Brotli/Gzip, cache headers, and CDN for static assets. Add `Cache-Control` for long-lived images and assets.
- **Trailing slashes:** `trailingSlash: true` in `next.config.mjs` — ensure internal links and canonical tags use the same canonical form.

## Content & keyword recommendations

- **Page intent & titles:** Each page needs a concise, keyword-rich `title` (60–70 chars) and `meta description` (110–160 chars). Use B2B + industry modifiers: `linen management`, `commercial laundry`, `hospital linen`, `hotel linen rental`, `campus laundry`.
- **H1 & structure:** Ensure one `h1` per page, with supporting `h2`/`h3` subsections for scannability and semantic structure.
- **Service pages:** Expand services with benefits, KPIs (e.g., `23 processing units`, `2+ lac garments daily`), process steps, and CTAs. Add short case-study excerpts linked to full case studies.
- **Blog strategy:** Use topic clusters from `Actual_Website_Content.md` (e.g., `Linen Rental ROI`, `Sustainability in Healthcare Linen`) and interlink to pillar service pages.
- **Alt text & filenames:** Ensure all images have descriptive `alt` text and keyword-friendly file names. Provide `width` & `height` attributes to avoid CLS.

## Structured data & social

- **Organization schema:** Present in `src/app/layout.js` — keep it.
- **Additions to implement:**
  - `BreadcrumbList` on hierarchical pages.
  - `Service` or `LocalBusiness` for services & contact pages.
  - `FAQPage` on `/faq` (include top FAQs from `Actual_Website_Content.md`).
  - `Article` schema for blog posts (include `author`, `datePublished`, `image`).
  - `Review` schema if you add client testimonials/reviews.
- **Open Graph / Twitter:** Ensure each page has `og:title`, `og:description`, `og:image` (1200×630 ideally) and matching `twitter:card` (`summary_large_image`). Use absolute URLs.

### Sample JSON-LD snippets (templates)

Service schema (insert into services pages):

```json
{
  "@context": "https://schema.org",
  "@type": "ProfessionalService",
  "name": "Quick Smart Wash",
  "url": "https://quicksmartwash.com/services",
  "logo": "https://quicksmartwash.com/logo/qsw_logo.png",
  "description": "End-to-end linen management and commercial laundry services for healthcare, hospitality, and education.",
  "areaServed": "IN",
  "contactPoint": [{ "@type": "ContactPoint", "telephone": "+919116010967", "contactType": "customer service" }]
}
```

FAQ schema (for `/faq`):

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What is the difference between Linen Rental and Laundry Services?",
      "acceptedAnswer": { "@type": "Answer", "text": "Linen Rental is end-to-end: we supply, manage and replace linen. Laundry Services is washing-only for your supplied linen." }
    }
  ]
}
```

Article schema template (for blog posts):

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Article title",
  "image": "https://quicksmartwash.com/path/to/image.jpg",
  "author": { "@type": "Person", "name": "Author Name" },
  "publisher": { "@type": "Organization", "name": "Quick Smart Wash", "logo": { "@type": "ImageObject", "url": "https://quicksmartwash.com/logo/qsw_logo.png" } },
  "datePublished": "2024-10-01"
}
```

## Performance & Core Web Vitals

- **Next Image:** Remove `images.unoptimized: true` from `next.config.mjs` and use Next `<Image>` with `priority` for hero assets.
- **Fonts:** `next/font` usage is correct — keep system fonts where possible to avoid FOIT.
- **Third-party JS:** Audit `framer-motion` and any analytics for bundle impact. Defer non-critical scripts and code-split animations.
- **Preload & preconnect:** Preload hero images and preconnect to CDNs/analytics.
- **Lighthouse checks:** Run Lighthouse for mobile and desktop; prioritize fixes for LCP (optimize hero image), CLS (add width/height or CSS aspect-ratio), and INP (defer heavy JS).

## Accessibility & UX

- **Navigation:** Current header uses `<a>` anchors. Use Next `<Link>` for client routing to reduce full page loads and ensure focus management.
- **ARIA & keyboard:** Ensure mobile menu toggles and CTA buttons are keyboard accessible and have ARIA labels.
- **Forms:** Add proper `<label>` elements, server-side validation, and accessible error messages on contact form.

## Local SEO & citations

- Add `LocalBusiness` schema to contact page and embed Google Map.
- Verify and optimise Google Business Profile; include consistent NAP across site and directories.

## Page-by-page metadata suggestions (ready-to-deploy)

- **Home (`/`)**
  - Title: `Quick Smart Wash — Linen Management & Commercial Laundry Services | India`
  - Description: `Trusted B2B linen management for healthcare, hospitality & education. 23+ processing units, Japanese partnership, infection-control processes. Contact us for a quote.`
  - Canonical: `https://quicksmartwash.com/`

- **About (`/about`)**
  - Title: `About Quick Smart Wash — B2B Linen Management Experts`
  - Description: `11+ years of experience delivering linen management solutions across hospitals, hotels and campuses. Learn about our mission and footprint.`

- **Services (`/services`)**
  - Title: `Commercial Laundry & Linen Management Services — Quick Smart Wash`
  - Description: `End-to-end linen rental and laundry solutions for hospitals, hotels and campuses. Eliminate CapEx, improve hygiene, and ensure timely delivery.`

- **Contact (`/contact`)**
  - Title: `Contact Quick Smart Wash — Request Quote & Partnership`
  - Description: `Get a custom linen management proposal. Phone: +91 9116010967 — Serving healthcare, hospitality and education across India.`

- **Blog (`/blog`)**
  - Title: `Insights — Quick Smart Wash Blog`
  - Description: `Industry insights on linen management, sustainability, infection control and operational efficiency.`

- (Repeat pattern for `/faq`, `/case-studies`, `/clients`, `/caring-second-skin`, `/highlights`, `/career`, `/privacy`, `/sustainability`.)

## Priority roadmap (what to implement first)

1. Quick wins (1–2 weeks)
   - Add unique page titles, meta descriptions and canonical tags for all pages.
   - Enable Next image optimisation and update hero images to `<Image>`.
   - Add page-level Open Graph images (1200×630).
   - Add `BreadcrumbList` and `FAQPage` schema for `/faq`.

2. Medium (2–6 weeks)
   - Run Lighthouse & fix LCP/CLS/INP issues.
   - Expand services pages with case studies and KPIs.
   - Add LocalBusiness schema and embed Google Map.

3. Longer term (ongoing)
   - Publish blog topic cluster and outreach for backlinks.
   - Implement advanced schema for reviews, case studies, and pricing (if applicable).

## Implementation checklist (developer-friendly)

- [ ] Add per-page metadata (title, description, canonical) using Next metadata API.
- [ ] Remove `images.unoptimized: true` from `next.config.mjs` and use Next `<Image>`.
- [ ] Add JSON-LD snippets for Service, BreadcrumbList, FAQ, and Article where applicable.
- [ ] Add OG images (1200×630) for main pages.
- [ ] Submit sitemap to Google Search Console and Bing Webmaster Tools.
- [ ] Audit Lighthouse and address Core Web Vitals.

## Next steps I can help with

- I can generate the per-page metadata files (ready-to-drop) for every route.
- I can open a PR that implements the high-priority fixes (metadata, canonical tags, Next Image change, sample JSON-LD).

---

File created by the SEO audit — let me know if you want a PR that implements the high-priority fixes now.
