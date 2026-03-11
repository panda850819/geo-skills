# Technical SEO Scoring

> 8-category technical SEO scoring (100 points total). Used by geo-audit (Agent 3: Technical).

## Overview

Technical SEO forms the foundation of both traditional search visibility and AI search citation. A technically broken site cannot be crawled, indexed, or cited by any platform. This reference covers 8 categories with specific attention to GEO requirements — most critically, **server-side rendering** (AI crawlers do not execute JavaScript) and **AI crawler access** (many sites inadvertently block AI crawlers in robots.txt).

### Score Interpretation

| Score | Rating |
|-------|--------|
| 90-100 | Excellent — technically sound for both traditional SEO and GEO |
| 70-89 | Good — minor issues to address but fundamentally solid |
| 50-69 | Needs Work — significant technical debt impacting visibility |
| 30-49 | Poor — major issues blocking crawling, indexing, or AI visibility |
| 0-29 | Critical — fundamental technical failures requiring immediate attention |

### Status per Category

- Pass = 80%+ of category points
- Warn = 50-79%
- Fail = <50%

---

## Category 1: Crawlability (15 points)

### 1.1 robots.txt Validity (3 pts)
- Fetch `https://[domain]/robots.txt`
- Check for syntactic validity: proper `User-agent`, `Allow`, `Disallow` directives
- Check for common errors: missing User-agent, wildcards blocking important paths, Disallow: / blocking entire site
- Verify XML sitemap is referenced: `Sitemap: https://[domain]/sitemap.xml`

### 1.2 AI Crawler Access (5 pts) — CRITICAL FOR GEO
Check robots.txt for directives targeting AI crawlers:

| Crawler | User-Agent | Platform |
|---------|-----------|---------|
| GPTBot | GPTBot | ChatGPT / OpenAI |
| Google-Extended | Google-Extended | Gemini / Google AI training |
| Googlebot | Googlebot | Google Search + AI Overviews |
| Bingbot | bingbot | Bing Copilot + ChatGPT (via Bing) |
| PerplexityBot | PerplexityBot | Perplexity AI |
| ClaudeBot | ClaudeBot | Anthropic Claude |
| Amazonbot | Amazonbot | Alexa / Amazon AI |
| CCBot | CCBot | Common Crawl (used by many AI models) |
| FacebookBot | FacebookExternalHit | Meta AI |
| Bytespider | Bytespider | TikTok / ByteDance AI |
| Applebot-Extended | Applebot-Extended | Apple Intelligence |

**Scoring for AI crawler access:**
- All major AI crawlers allowed: 5 points
- Some blocked but Googlebot + Bingbot allowed: 3 points
- GPTBot or PerplexityBot blocked: 1 point (significant GEO impact)
- Googlebot blocked: 0 points (fatal)

**Important nuance**: Blocking Google-Extended does NOT block Googlebot. Google-Extended only controls AI training data usage, not search indexing. However, blocking Google-Extended may reduce presence in AI Overviews.

### 1.3 XML Sitemaps (3 pts)
- Fetch sitemap (check robots.txt for location, or try `/sitemap.xml`, `/sitemap_index.xml`)
- Validate XML syntax
- Check for `<lastmod>` dates (should be present and accurate)
- Count URLs — compare to expected number of indexable pages
- Check for sitemap index if large site (50,000+ URLs per sitemap max)
- Verify sample sitemap URLs return 200 status codes

### 1.4 Crawl Depth (2 pts)
- Homepage = depth 0. All important pages reachable within **3 clicks** (depth 3)
- Pages at depth 4+ receive significantly less crawl budget and are less likely to be cited by AI
- Check internal linking: are key content pages linked from homepage or main navigation?

### 1.5 Noindex Management (2 pts)
- Check for `<meta name="robots" content="noindex">` on pages that SHOULD be indexed
- Check for `X-Robots-Tag: noindex` HTTP headers
- Common mistakes: noindex on paginated pages, category pages, or key landing pages

**Category scoring summary:**
| Check | Points |
|-------|--------|
| robots.txt valid and complete | 3 |
| AI crawlers allowed | 5 |
| XML sitemap present and valid | 3 |
| Crawl depth within 3 clicks | 2 |
| No erroneous noindex directives | 2 |

---

## Category 2: Indexability (12 points)

### 2.1 Canonical Tags (3 pts)
- Every indexable page must have `<link rel="canonical" href="...">`
- Canonical must point to itself (self-referencing) for the authoritative version
- Check for conflicting canonicals (HTML vs. HTTP header)
- Check for canonical chains (A->B->C should be A->C)

### 2.2 Duplicate Content (3 pts)
- www vs. non-www (one should redirect)
- HTTP vs. HTTPS (HTTP should redirect to HTTPS)
- Trailing slash consistency (pick one, redirect the other)
- Parameter-based duplicates (`?sort=price` creating duplicates)

### 2.3 Pagination (2 pts)
- Check for `rel="next"` / `rel="prev"` (Google ignores since 2019, Bing still uses)
- Preferred: `rel="canonical"` on paginated pages to view-all or first page
- Ensure paginated pages with unique content are not noindexed

### 2.4 Hreflang — International Sites (2 pts)
- Check for `<link rel="alternate" hreflang="xx">`
- Validate reciprocal hreflang (if A points to B, B must point to A)
- Validate x-default fallback exists
- Check language/region code validity (ISO 639-1 / ISO 3166-1)

### 2.5 Index Bloat (2 pts)
- Estimate indexed pages (sitemap count, `site:domain.com`)
- Compare to actual valuable content pages
- Flag if indexed significantly exceeds content (bloat from thin/duplicate/parameter pages)

**Category scoring summary:**
| Check | Points |
|-------|--------|
| Canonical tags correct on all pages | 3 |
| No duplicate content issues | 3 |
| Pagination handled correctly | 2 |
| Hreflang correct (if applicable) | 2 |
| No index bloat | 2 |

---

## Category 3: Security (10 points)

### 3.1 HTTPS Enforcement (4 pts)
- Site loads over HTTPS
- HTTP redirects to HTTPS (301)
- No mixed content warnings
- SSL/TLS certificate valid and not expired

### 3.2 Security Headers (6 pts)
| Header | Required Value | Points |
|--------|---------------|--------|
| `Strict-Transport-Security` | `max-age=31536000; includeSubDomains` | 2 |
| `X-Content-Type-Options` | `nosniff` | 1 |
| `X-Frame-Options` | `DENY` or `SAMEORIGIN` | 1 |
| `Referrer-Policy` | `strict-origin-when-cross-origin` or stricter | 1 |
| `Content-Security-Policy` | Appropriate policy | 1 |

---

## Category 4: URL Structure (8 points)

### 4.1 Clean URLs (2 pts)
- Human-readable: `/blog/seo-guide` not `/blog?id=12345`
- No session IDs in URLs
- Lowercase only
- Hyphens for word separation (not underscores)
- No special characters or encoded spaces

### 4.2 Logical Hierarchy (2 pts)
- URL path reflects site architecture: `/category/subcategory/page`
- Flat where appropriate
- Consistent pattern across site

### 4.3 Redirect Chains (2 pts)
- No redirect chains (A->B->C)
- Maximum 1 hop recommended
- No redirect loops
- All redirects should be 301 (not 302) unless intentionally temporary

### 4.4 Parameter Handling (2 pts)
- Parameters should not create duplicate indexable pages
- Use canonical tags or robots.txt for parameter variations
- Configure handling in GSC and Bing Webmaster Tools

---

## Category 5: Mobile Optimization (10 points)

### Critical Context
As of **July 2024**, Google crawls ALL sites exclusively with mobile Googlebot. No desktop crawling. If your site does not work on mobile, it does not work for Google.

### 5.1 Responsive Design (6 pts)
- `<meta name="viewport" content="width=device-width, initial-scale=1">` present (3 pts)
- Content must not require horizontal scrolling on mobile (3 pts)

### 5.2 Tap Targets (2 pts)
- Interactive elements at least 48x48 CSS pixels
- Minimum 8px spacing between tap targets

### 5.3 Font Sizes (2 pts)
- Base font size at least 16px
- No text requiring zoom
- Sufficient contrast ratio (WCAG AA: 4.5:1 normal, 3:1 large)

### 5.4 Mobile Content Parity
- All desktop content visible on mobile
- No hidden content behind toggles Googlebot cannot expand
- Images and media load on mobile

---

## Category 6: Core Web Vitals (15 points)

### 2026 Metrics and Thresholds

Core Web Vitals use the **75th percentile** of real user data (field data) as the benchmark.

| Metric | Good | Needs Improvement | Poor | Points |
|--------|------|-------------------|------|--------|
| **LCP** (Largest Contentful Paint) | < 2.5s | 2.5s - 4.0s | > 4.0s | 5 |
| **INP** (Interaction to Next Paint) | < 200ms | 200ms - 500ms | > 500ms | 5 |
| **CLS** (Cumulative Layout Shift) | < 0.1 | 0.1 - 0.25 | > 0.25 | 5 |

Note: INP replaced FID in March 2024. Measures ALL interactions, not just first.

### Estimation Without CrUX Data
- **LCP**: Check largest above-fold element. Image (check size/format)? Text (check web font loading)? TTFB?
- **INP**: Check for heavy JavaScript. Long tasks (>50ms) block interactivity. Third-party scripts?
- **CLS**: Images without width/height? Dynamically inserted content above fold? Web fonts causing FOUT/FOIT?

### Common Fixes

**LCP:**
1. Optimize hero images: WebP/AVIF, correct sizing, preload with `<link rel="preload">`
2. Reduce TTFB (< 800ms)
3. Eliminate render-blocking CSS/JS
4. Preconnect to critical third-party origins

**INP:**
1. Break long tasks (>50ms) using `requestIdleCallback` or `scheduler.yield()`
2. Reduce third-party JavaScript
3. Use `content-visibility: auto` for off-screen content
4. Debounce/throttle event handlers

**CLS:**
1. Include `width` and `height` on images and videos
2. Reserve space for ads/embeds with `aspect-ratio` or explicit dimensions
3. Use `font-display: swap` with size-adjusted fallback fonts
4. Avoid inserting content above existing content after page load

---

## Category 7: Server-Side Rendering (15 points) — CRITICAL FOR GEO

### Why SSR Is Mandatory for AI Visibility

AI crawlers (GPTBot, PerplexityBot, ClaudeBot, etc.) do **NOT execute JavaScript**. They fetch raw HTML and parse it. If content is rendered client-side by React, Vue, Angular, or any JS framework, AI crawlers see an empty page.

Even Googlebot, which does execute JavaScript, deprioritizes JS-rendered content. Google processes JS rendering in a separate "rendering queue" that can delay indexing by days or weeks.

### Detection Method
1. Fetch page with curl (no JS execution): `curl -s [URL]`
2. Compare raw HTML to rendered DOM (via browser)
3. If key content (headings, paragraphs, article text) is MISSING from curl output, the site relies on client-side rendering

### What to Check
- **Main content text**: Article body / product description in raw HTML? (8 pts)
- **Meta tags + structured data**: Title, description, canonical, OG tags, JSON-LD in raw HTML? (4 pts)
- **Internal links**: Navigation and content links in raw HTML? (3 pts)

### SSR Solutions

| Framework | SSR Solution |
|-----------|-------------|
| React | Next.js (SSR/SSG), Remix, Gatsby (SSG) |
| Vue | Nuxt.js (SSR/SSG) |
| Angular | Angular Universal |
| Svelte | SvelteKit |
| Generic | Prerender.io (prerendering service), Rendertron |

### Scoring Detail
- All key content server-rendered: 15 points
- Main content SSR but some elements JS-only: 10 points
- Critical content requires JS (product info, article text): 5 points
- Entire page is client-rendered (empty body in raw HTML): 0 points

---

## Category 8: Page Speed & Server Performance (15 points)

### 8.1 TTFB (3 pts)
- Target: **< 800ms** (ideally < 200ms)
- Measure: `curl -o /dev/null -s -w 'TTFB: %{time_starttransfer}s\n' [URL]`
- If > 800ms: check server location, caching, database queries, CDN usage

### 8.2 Page Weight (2 pts)
- Total page weight target: **< 2MB** (critical pages < 1MB)
- Check for uncompressed resources (gzip/brotli)
- Check for unminified CSS and JavaScript
- Check for unused CSS/JS

### 8.3 Image Optimization (3 pts)
- Formats: WebP or AVIF preferred over JPEG/PNG
- Sizing: Images not larger than display size
- Lazy loading: Below-fold images have `loading="lazy"`
- Dimensions: Explicit width/height attributes (prevents CLS)
- Above-fold images should NOT be lazy loaded (harms LCP)

### 8.4 JavaScript Bundles (2 pts)
- Code-split so each page loads only what it needs
- Warning: > 200KB compressed. Critical: > 500KB compressed.
- Third-party scripts load async (`async` or `defer`)
- No render-blocking resources in `<head>`

### 8.5 Compression (2 pts)
- `Cache-Control` headers on static resources
- Static assets: `max-age=31536000` with content-hashed filenames
- HTML: shorter cache or `no-cache` with `ETag`/`Last-Modified` validation
- gzip/brotli compression enabled

### 8.6 CDN (1 pt)
- Static resources served from CDN?
- CDN headers: `CF-Ray` (Cloudflare), `X-Cache` (CloudFront), `X-Served-By` (Fastly)
- For global audience, CDN is critical

**Category scoring summary:**
| Check | Points |
|-------|--------|
| TTFB < 800ms | 3 |
| Page weight < 2MB | 2 |
| Images optimized (format, size, lazy) | 3 |
| JS bundles < 200KB compressed | 2 |
| Compression enabled (gzip/brotli) | 2 |
| Cache headers on static resources | 2 |
| CDN in use | 1 |

---

## IndexNow Protocol

### What It Is
Open protocol for instant search engine notification when content is created, updated, or deleted. Supported by Bing, Yandex, Seznam, Naver. Google does NOT support IndexNow but monitors the protocol.

### Why It Matters for GEO
ChatGPT uses Bing's index. Bing Copilot uses Bing's index. Faster Bing indexing = faster AI visibility on two major platforms.

### Implementation Check
1. Check for IndexNow key file: `https://[domain]/.well-known/indexnow-key.txt`
2. Check if CMS has IndexNow plugin (WordPress: IndexNow plugin; many modern CMS platforms support natively)
3. If not implemented, recommend adding

---

## Overall Scoring Summary

| Category | Max Points |
|----------|-----------|
| Crawlability | 15 |
| Indexability | 12 |
| Security | 10 |
| URL Structure | 8 |
| Mobile Optimization | 10 |
| Core Web Vitals | 15 |
| Server-Side Rendering | 15 |
| Page Speed & Server | 15 |
| **Total** | **100** |
