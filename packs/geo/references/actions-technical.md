# GEO Actions: Technical

> Technical improvement actions for GEO scores. Covers AI crawler access, schema implementation, and technical fixes.

## Table of Contents

1. [AI Crawler Access](#1-ai-crawler-access)
2. [Schema Implementation](#2-schema-implementation)
3. [Technical Fixes](#3-technical-fixes)

---

## 1. AI Crawler Access

Blocking AI crawlers is a Critical severity issue. 35%+ of top 1,000 websites accidentally block at least one major AI crawler.

### Action Summary

| Action | Effort | Impact | Timeline | Tools |
|--------|--------|--------|----------|-------|
| Audit robots.txt for AI crawler blocks | Low | Critical (binary) | Immediate | curl, robots.txt validators |
| Update robots.txt to allow Tier 1 crawlers | Low | +15-20 pts technical | Immediate | Text editor |
| Set up Cloudflare AI Crawl Control | Low | +5 pts technical | 30 min | Cloudflare dashboard |
| Implement llms.txt | Medium | +3-5 pts technical | 1-2 hours | Text editor |
| Set up IndexNow | Low | +15 pts Copilot score | 30 min | WordPress plugin or manual |

### Check If You're Blocking AI Bots

Run this immediately:

```bash
# Fetch your robots.txt
curl -s https://yourdomain.com/robots.txt

# Check for specific blocks
curl -s https://yourdomain.com/robots.txt | grep -i -E "gptbot|claudebot|perplexitybot|google-extended|bingbot"
```

**Red flags to look for:**
- `User-agent: *` with `Disallow: /` — blocks everything including AI
- `User-agent: GPTBot` with `Disallow: /` — invisible to ChatGPT
- `User-agent: PerplexityBot` with `Disallow: /` — invisible to Perplexity
- No explicit `Allow` directives for AI crawlers

### robots.txt for Maximum AI Visibility

Replace your robots.txt with this (adapt paths as needed). For the full crawler list with user-agent strings, see `geo-methodology.md` Section 2.

```
# AI Search Crawlers — ALLOW
User-agent: GPTBot
Allow: /

User-agent: OAI-SearchBot
Allow: /

User-agent: ChatGPT-User
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: PerplexityBot
Allow: /

User-agent: Google-Extended
Allow: /

User-agent: Applebot-Extended
Allow: /

User-agent: Amazonbot
Allow: /

User-agent: facebookexternalhit
Allow: /

# Block aggressive crawlers with minimal benefit
User-agent: Bytespider
Disallow: /

# Standard crawlers
User-agent: *
Allow: /

# Sitemap
Sitemap: https://yourdomain.com/sitemap.xml
```

**Tools for generating robots.txt:**
- Merkle robots.txt Tester: https://technicalseo.com/tools/robots-txt/
- Google robots.txt Tester in Search Console
- Screaming Frog (crawl simulation with specific user-agents)

### Cloudflare AI Crawl Control Setup

1. Log in to Cloudflare Dashboard
2. Go to **Security > Bots**
3. Find **AI Crawlers and Scrapers** section
4. Toggle individual AI crawlers on/off:
   - Enable: GPTBot, OAI-SearchBot, ClaudeBot, PerplexityBot, Google-Extended, Applebot-Extended
   - Disable: Bytespider (aggressive, minimal benefit)
5. Note: Cloudflare controls override robots.txt — check both

### Implement llms.txt

The `llms.txt` file is a proposed standard for providing AI-friendly site information. Place at your domain root.

Create `https://yourdomain.com/llms.txt`:

```
# YourBrand

> One-sentence description of what your company does.

## About
YourBrand is [what you do] for [whom]. Founded in [year], headquartered in [city].

## Key Topics
- Topic 1: [brief description]
- Topic 2: [brief description]
- Topic 3: [brief description]

## Important Pages
- [Homepage](https://yourdomain.com/)
- [About](https://yourdomain.com/about)
- [Blog](https://yourdomain.com/blog)
- [Documentation](https://yourdomain.com/docs)

## Contact
- Website: https://yourdomain.com
- Email: contact@yourdomain.com
```

### Set Up IndexNow

IndexNow notifies Bing (and by extension ChatGPT/Copilot) instantly when content changes. Worth +15 points on the Copilot platform score.

**WordPress:**
1. Install the "IndexNow" plugin by Microsoft (free)
2. Activate — it auto-generates a key and submits on publish/update
3. Verify in Bing Webmaster Tools under "IndexNow" tab

**Manual (any framework):**

1. Generate a key (any UUID): `uuidgen` or use an online generator
2. Create key file at `https://yourdomain.com/.well-known/indexnow-key.txt` containing just the key
3. Ping on content publish:

```bash
curl "https://api.indexnow.org/indexnow?url=https://yourdomain.com/new-page&key=YOUR-KEY"
```

4. For batch submissions:

```bash
curl -X POST "https://api.indexnow.org/indexnow" \
  -H "Content-Type: application/json" \
  -d '{
    "host": "yourdomain.com",
    "key": "YOUR-KEY",
    "urlList": [
      "https://yourdomain.com/page1",
      "https://yourdomain.com/page2"
    ]
  }'
```

**Do this now:**
1. Check your robots.txt right now — `curl -s https://yourdomain.com/robots.txt`
2. Fix any AI crawler blocks immediately
3. Install IndexNow plugin (WordPress) or create the key file (other platforms)

---

## 2. Schema Implementation

Schema is 10% of the composite GEO score, but it amplifies every other dimension by helping AI systems understand your entity.

### Action Summary

| Action | Effort | Impact | Timeline | Tools |
|--------|--------|--------|----------|-------|
| Add Organization schema with sameAs | Low | +15 pts schema | 1-2 hours | Schema generator, Rank Math |
| Add Article + Author schema | Medium | +10 pts schema | 2-4 hours | Yoast, next-seo |
| Add speakable property | Low | +5 pts schema | 30 min | JSON-LD editor |
| Add knowsAbout property | Low | +5 pts schema | 15 min | JSON-LD editor |
| Validate all schema | Low | +10 pts schema | 30 min | Google Rich Results Test |

### Tools

| Tool | URL | Purpose |
|------|-----|---------|
| Google Rich Results Test | search.google.com/test/rich-results | Validate schema, preview rich results |
| Schema.org Validator | validator.schema.org | Validate against Schema.org spec |
| Merkle Schema Generator | technicalseo.com/tools/schema-markup-generator/ | Generate JSON-LD without coding |
| JSON-LD Playground | json-ld.org/playground/ | Debug JSON-LD syntax |

### WordPress Plugins

| Plugin | Schema Features | Price |
|--------|----------------|-------|
| Yoast SEO | Organization, Article, Author, Breadcrumb (auto) | Free / $99/yr |
| Rank Math | All above + Video, Local, Product, FAQ | Free / $59/yr |
| Schema Pro | Full schema control, custom types, conditions | $79/yr |

### Next.js / React Implementation

```bash
npm install next-seo
# or
npm install react-schemaorg schema-dts
```

**next-seo example (pages/_app.tsx or layout.tsx):**
```tsx
import { DefaultSeo, OrganizationJsonLd } from 'next-seo';

// In your layout or _app:
<OrganizationJsonLd
  type="Organization"
  id="https://yourdomain.com/#organization"
  name="Your Brand"
  url="https://yourdomain.com"
  logo="https://yourdomain.com/logo.png"
  sameAs={[
    'https://www.wikidata.org/wiki/Q12345',
    'https://www.linkedin.com/company/yourbrand',
    'https://www.youtube.com/@yourbrand',
    'https://twitter.com/yourbrand',
    'https://github.com/yourbrand',
  ]}
/>
```

**react-schemaorg example:**
```tsx
import { JsonLd } from 'react-schemaorg';
import { Organization } from 'schema-dts';

<JsonLd<Organization>
  item={{
    "@context": "https://schema.org",
    "@type": "Organization",
    name: "Your Brand",
    url: "https://yourdomain.com",
    knowsAbout: ["Topic 1", "Topic 2", "Topic 3"],
    sameAs: ["https://linkedin.com/company/...", "https://youtube.com/@..."]
  }}
/>
```

### Step-by-Step: Organization Schema with sameAs

See `schema-templates.md` for full JSON-LD templates (Organization, Article+Author, Product, LocalBusiness, SoftwareApplication).

1. **Collect all your platform URLs:**
   - Wikipedia article URL (if exists)
   - Wikidata item URL (e.g., `https://www.wikidata.org/wiki/Q12345`)
   - LinkedIn company page
   - YouTube channel
   - Twitter/X profile
   - GitHub organization
   - Crunchbase profile
   - Facebook page
   - Instagram profile

2. **Generate the JSON-LD** using the Organization template in `schema-templates.md` or the Merkle generator

3. **Place in HTML `<head>`** — NOT injected via JavaScript (AI crawlers do not execute JS)
4. **Validate** at https://search.google.com/test/rich-results
5. **Verify each sameAs URL resolves** (no 404s)

### Step-by-Step: Article + Author Schema with speakable

See `schema-templates.md` for the full Article + Author template with speakable.

**Key points:**
- `speakable` tells AI assistants which passages to extract for citation or voice
- Point `cssSelector` at your article summary, key takeaways, and first paragraph after each H2
- `knowsAbout` on both Organization AND Person schemas is a strong GEO signal
- `dateModified` is critical — AI platforms deprioritize stale content

### Step-by-Step: Adding knowsAbout

The `knowsAbout` property tells AI systems what topics your organization or authors are expert in. It directly maps to query-entity matching.

1. List 5-15 topics your brand has deep expertise in
2. Use the exact terms people search for (not internal jargon)
3. Add to both Organization and Person schemas:

```json
"knowsAbout": [
  "content delivery networks",
  "web performance optimization",
  "edge computing",
  "DDoS protection",
  "serverless computing"
]
```

**Do this now:**
1. Check if you have Organization schema: View Source > search for `application/ld+json`
2. If missing, generate with Merkle tool and add to your `<head>`
3. If present, add `sameAs` and `knowsAbout` properties
4. Validate at Google Rich Results Test

---

## 3. Technical Fixes

Technical foundations are 15% of the composite GEO score. SSR and CWV are the highest-weighted categories.

### Action Summary

| Action | Effort | Impact | Timeline | Tools |
|--------|--------|--------|----------|-------|
| Check if site is server-rendered | Low | Diagnostic | 5 min | curl |
| Migrate SPA to SSR/SSG | High | +15 pts technical (critical) | 4-12 weeks | Next.js, Nuxt, prerender.io |
| Optimize Core Web Vitals | Medium | +15 pts technical | 2-6 weeks | PageSpeed Insights, WebPageTest |
| Add security headers | Low | +6 pts technical | 15 min | Cloudflare / nginx / Vercel config |
| Enforce HTTPS | Low | +4 pts technical | 30 min | Hosting provider |
| Mobile optimization fixes | Medium | +10 pts technical | 1-3 weeks | Lighthouse, Chrome DevTools |

### SSR Check and Migration Paths

**Check if AI crawlers can see your content:**

```bash
# If main content is missing from this output, you have a critical SSR problem
curl -s https://yourdomain.com | grep -o '<h1[^>]*>.*</h1>'
curl -s https://yourdomain.com | grep -c '<p>'
```

If `curl` returns an empty `<div id="root"></div>` or `<div id="app"></div>` with no content, your site is client-rendered and invisible to AI crawlers.

**Migration paths:**

| Current Stack | Migration Target | Effort | Notes |
|---------------|-----------------|--------|-------|
| React (CRA) | Next.js | High (4-8 weeks) | Most common migration. Pages router is simpler. |
| React (CRA) | prerender.io | Low (1 day) | Quick fix. Serves pre-rendered HTML to bots. $20-$200/mo. |
| Vue | Nuxt.js | High (4-8 weeks) | Similar to React->Next.js migration. |
| Angular | Angular Universal | High (6-12 weeks) | More complex. Consider Analog.js as alternative. |
| Any SPA | prerender.io | Low (1 day) | Universal quick fix. Add middleware or Cloudflare Worker. |
| Any SPA | Rendertron | Medium (1 week) | Self-hosted prerendering. Free but requires server. |

**prerender.io quick setup (any framework):**
1. Sign up at prerender.io
2. Add middleware to your server (Node.js example):
```javascript
app.use(require('prerender-node').set('prerenderToken', 'YOUR_TOKEN'));
```
3. Or use Cloudflare Worker to route bot traffic to prerender.io
4. Verify: `curl -A "GPTBot" https://yourdomain.com` should return full HTML

### Core Web Vitals Quick Fixes

**LCP (Largest Contentful Paint) — target < 2.5s:**

```html
<!-- Preload hero image -->
<link rel="preload" as="image" href="/hero.webp" fetchpriority="high">

<!-- Preconnect to critical third parties -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://cdn.yourdomain.com">

<!-- Convert images to WebP/AVIF -->
<picture>
  <source srcset="/hero.avif" type="image/avif">
  <source srcset="/hero.webp" type="image/webp">
  <img src="/hero.jpg" alt="Description" width="1200" height="630">
</picture>
```

**CLS (Cumulative Layout Shift) — target < 0.1:**

```html
<!-- Always set dimensions on images -->
<img src="/photo.webp" width="800" height="450" alt="Description">

<!-- Reserve space for ads/embeds -->
<div style="aspect-ratio: 16/9; min-height: 250px;">
  <!-- Ad or embed loads here -->
</div>

<!-- Font loading without layout shift -->
<style>
  @font-face {
    font-family: 'CustomFont';
    src: url('/fonts/custom.woff2') format('woff2');
    font-display: swap;
    size-adjust: 105%;  /* Match fallback font metrics */
  }
</style>
```

**INP (Interaction to Next Paint) — target < 200ms:**
- Audit third-party scripts: remove unused trackers and widgets
- Defer non-critical JavaScript: `<script src="..." defer></script>`
- Break long tasks: use `requestIdleCallback` for non-urgent work

**Tools:**
- PageSpeed Insights (pagespeed.web.dev) — field + lab data
- WebPageTest (webpagetest.org) — waterfall analysis
- Chrome DevTools > Performance tab — identify specific bottlenecks
- Lighthouse CI — automated CWV monitoring in CI/CD

### Security Headers One-Liner

**Cloudflare (Workers or Transform Rules):**

In Cloudflare Dashboard > Rules > Transform Rules > Modify Response Header:
```
Strict-Transport-Security: max-age=31536000; includeSubDomains
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Referrer-Policy: strict-origin-when-cross-origin
```

**nginx:**
```nginx
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
add_header X-Content-Type-Options "nosniff" always;
add_header X-Frame-Options "SAMEORIGIN" always;
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
```

**Vercel (vercel.json):**
```json
{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "Strict-Transport-Security", "value": "max-age=31536000; includeSubDomains" },
        { "key": "X-Content-Type-Options", "value": "nosniff" },
        { "key": "X-Frame-Options", "value": "SAMEORIGIN" },
        { "key": "Referrer-Policy", "value": "strict-origin-when-cross-origin" }
      ]
    }
  ]
}
```

**Next.js (next.config.js):**
```javascript
const securityHeaders = [
  { key: 'Strict-Transport-Security', value: 'max-age=31536000; includeSubDomains' },
  { key: 'X-Content-Type-Options', value: 'nosniff' },
  { key: 'X-Frame-Options', value: 'SAMEORIGIN' },
  { key: 'Referrer-Policy', value: 'strict-origin-when-cross-origin' },
];

module.exports = {
  async headers() {
    return [{ source: '/(.*)', headers: securityHeaders }];
  },
};
```

### Mobile Optimization Checklist

- [ ] `<meta name="viewport" content="width=device-width, initial-scale=1">` present
- [ ] No horizontal scroll on any page (test at 375px width)
- [ ] Tap targets at least 48x48 CSS pixels with 8px spacing
- [ ] Base font size >= 16px
- [ ] All desktop content visible on mobile (no hidden-on-mobile sections)
- [ ] Images responsive with `max-width: 100%`
- [ ] No interstitials or pop-ups covering content on mobile

### HTTPS Enforcement

Most hosting providers handle this automatically. If not:

1. Get a free SSL certificate from Let's Encrypt (certbot)
2. Configure 301 redirect from HTTP to HTTPS
3. Update all internal links to HTTPS
4. Update canonical tags to HTTPS
5. Update sitemap URLs to HTTPS
6. Check for mixed content warnings in browser console
