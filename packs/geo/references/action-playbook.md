# GEO Action Playbook

Practical, prioritized actions to improve your GEO score across all dimensions. Every action includes effort level, expected impact, timeline, and specific tools. Start with Critical severity items, then High, Medium, Low.

## Table of Contents

1. [Citability Quick Wins](#1-citability-quick-wins)
2. [AI Crawler Access](#2-ai-crawler-access)
3. [Brand Authority Building](#3-brand-authority-building)
4. [Schema Implementation](#4-schema-implementation)
5. [Technical Fixes](#5-technical-fixes)
6. [E-E-A-T Improvement](#6-e-e-a-t-improvement)
7. [Platform-Specific Onboarding](#7-platform-specific-onboarding)
8. [Monitoring and Iteration](#8-monitoring-and-iteration)

---

## 1. Citability Quick Wins

Citability is 25% of the composite GEO score. These actions target Answer Block Quality, Self-Containment, and Statistical Density — the three highest-weighted citability dimensions.

### Action Summary

| Action | Effort | Impact | Timeline | Tools |
|--------|--------|--------|----------|-------|
| Rewrite intros to answer-first pattern | Low | +10-15 pts citability | 1-2 weeks | Hemingway Editor |
| Add question-based H2/H3 headings | Low | +5-10 pts citability | 1 week | Google PAA, AlsoAsked |
| Insert statistics with named sources | Medium | +5-10 pts citability | 2-4 weeks | Statista, Clearscope |
| Convert comparisons to tables | Low | +3-5 pts citability | 1 week | Markdown/HTML editor |
| Add definition patterns for key terms | Low | +5-8 pts citability | 1 week | — |
| Restructure paragraphs to 2-4 sentences | Low | +3-5 pts structure | 1-2 weeks | Surfer SEO |

### Rewrite Content for Answer-First Pattern

AI systems extract the first 40-60 words of each section as a citation candidate. Bury the answer and you lose the citation.

**Before (Score: 15):**
```
If you've been thinking about improving your website's performance, you
might have heard about content delivery networks. There are many options
available, and the right choice depends on your specific needs. Let me
walk you through how CDNs work and why they matter.
```

**After (Score: 85+):**
```
A content delivery network (CDN) is a distributed server system that
caches and serves web content from locations geographically close to
end users. CDNs reduce latency by 50-70% on average (Cloudflare 2025
Performance Report). The three largest providers are Cloudflare (20% of
all websites), Amazon CloudFront, and Akamai Technologies.
```

**What changed:**
- Sentence 1: definition pattern ("X is...")
- Sentence 2: specific statistic with named source
- Sentence 3: concrete data points (names, numbers)
- No filler, no preamble, no "let me explain"

**Rewriting process (per section):**
1. Identify the core question the section answers
2. Write a 1-2 sentence direct answer as the opening
3. Add one statistic with a named source
4. Add one specific example (names, numbers, dates)
5. Run through Hemingway Editor — target Grade 8-9 reading level

### Add Statistics to Existing Content

Statistics increase citation rate by 40% (Princeton GEO study 2024). Target 3-5 statistics per 500 words.

**Where to find statistics:**
- Statista (statista.com) — general industry data
- Clearscope — shows what top-ranking content cites
- Google Scholar — academic studies
- Industry annual reports (HubSpot, Gartner, McKinsey, Ahrefs)
- Government sources (census.gov, bls.gov, SEC filings)

**Format for AI extraction:**
```
According to [Named Source] ([Year]), [specific claim with number].
```

Examples:
- "According to Gartner (2025), traditional search traffic will decline 50% by 2028."
- "The average implementation cost is $4,500/month (Forrester 2025 SaaS Benchmark)."

**Do this now:**
1. Pick your top 5 pages by traffic
2. For each page, add at least 3 sourced statistics
3. Replace every vague quantifier ("many", "most", "several") with a specific number
4. Run Clearscope or Surfer SEO to identify statistical gaps vs. competitors

### WordPress Plugins for Structured Headings

| Plugin | What It Does | Price |
|--------|-------------|-------|
| Yoast SEO | Flags heading hierarchy issues, readability analysis | Free / $99/yr |
| Rank Math | Heading structure analysis, content AI suggestions | Free / $59/yr |
| Table of Contents Plus | Auto-generates TOC from headings (aids AI parsing) | Free |
| TablePress | Create structured HTML tables (AIO loves tables) | Free / $79/yr |

---

## 2. AI Crawler Access

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

Replace your robots.txt with this (adapt paths as needed):

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

User-agent: FacebookBot
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

## 3. Brand Authority Building

Brand authority is 20% of the composite GEO score. Brand mentions correlate ~3x more with AI visibility than backlinks (Ahrefs Dec 2025, 75K brands).

**Timeline expectation:** Brand authority takes 3-12 months to build. These are not quick wins. Start now and compound over time.

### Action Summary

| Action | Effort | Impact | Timeline | Tools |
|--------|--------|--------|----------|-------|
| Create minimum viable YouTube channel | High | +15-25 pts brand | 3-6 months | YouTube Studio, Descript |
| Build authentic Reddit presence | Medium | +10-20 pts brand | 2-6 months | Reddit, Gummy Search |
| Create Wikidata entry | Medium | +10-15 pts brand | 1-4 weeks | wikidata.org |
| Optimize LinkedIn company page | Low | +5-10 pts brand | 1 week | LinkedIn |
| Pursue Wikipedia article | High | +15-20 pts brand | 6-12 months | Wikipedia consultant |

### YouTube: Minimum Viable Channel

YouTube mention correlation with AI citation: 0.737 — the strongest signal. Even a small channel helps.

**3-5 starter videos (pick based on your business):**

| Video Type | Purpose | Example Title |
|------------|---------|---------------|
| "What is [Your Category]" explainer | Capture definition queries | "What is Revenue Operations? Explained in 5 Minutes" |
| "How to [Core Task]" tutorial | Capture how-to queries | "How to Set Up a CI/CD Pipeline with GitHub Actions" |
| "[Product] vs [Competitor]" comparison | Capture comparison queries | "Notion vs Obsidian: Which Note App in 2026?" |
| "[Your Topic] for Beginners" guide | Capture beginner queries | "Kubernetes for Beginners: Your First Deployment" |
| Customer success story / case study | Build social proof | "How [Client] Reduced Costs 40% with [Product]" |

**Production checklist (keep it simple):**
- Screen recording + voiceover is fine (no need for studio production)
- Tools: Descript ($24/mo), Loom (free tier), OBS Studio (free)
- Include brand name in: title, description, spoken audio (transcripts matter)
- Add timestamps/chapters in the description
- Upload closed captions (auto-generated + manual correction)

**How to get mentioned by others:**
- Send product to relevant YouTubers for review (micro-influencers: 5K-50K subs)
- Guest on industry YouTube channels
- Create content that others reference (original data, frameworks, tools)

### Reddit: Authentic Participation Strategy

Reddit mentions are the second strongest AI citation signal. Perplexity cites Reddit in 46.7% of responses.

**Step 1: Identify your subreddits (use Gummy Search — gummysearch.com)**
- Search your industry keywords
- Find 3-5 subreddits where your audience asks questions
- Check subreddit rules before posting

**Step 2: Participation framework (DO NOT shill)**

| Week | Activity | Time |
|------|----------|------|
| 1-2 | Lurk. Read top posts. Understand culture. | 30 min/day |
| 3-4 | Comment helpfully on relevant questions. No brand mentions yet. | 30 min/day |
| 5-8 | Create value-first posts (guides, tips, data). Mention brand only if directly relevant. | 1 hr/week |
| 9+ | Participate in recommendation threads. Share expertise naturally. | 1 hr/week |

**AMA guide:**
- Post in a relevant subreddit (check rules — some require mod approval)
- Title format: "I'm [Name], [Role] at [Brand]. We [notable thing]. AMA!"
- Prepare answers to top 10 likely questions beforehand
- Answer for 2+ hours. Be genuine. Admit limitations.
- Cross-post announcement to your community channels

**Rules:**
- Never create fake accounts to promote your brand
- Never pay for upvotes or astroturf
- Reddit communities detect and permanently ban shills
- One genuine helpful comment outweighs 100 promotional ones

### Wikipedia: Notability and Wikidata

**Notability criteria (do you qualify for a Wikipedia article?):**
- Significant coverage in multiple reliable, independent sources
- Press coverage in major publications (NYT, TechCrunch, Forbes, WSJ, etc.)
- Academic citations or industry reports mentioning the brand
- Annual revenue typically >$10M or significant industry impact

**If you DO NOT meet notability criteria yet:**
1. Focus on getting press coverage first (PR campaigns, thought leadership)
2. Create a Wikidata entry (lower bar than Wikipedia — see below)
3. Get cited as a reference in existing Wikipedia articles

**Wikidata entry creation (step by step):**

1. Go to https://www.wikidata.org/wiki/Special:NewItem
2. Create account if needed
3. Fill in:
   - **Label**: Your brand name
   - **Description**: "software company" / "marketing agency" / etc.
   - **Aliases**: Alternative names, abbreviations
4. Add properties (click "add statement"):
   - `instance of` (P31): "business" (Q4830453) or more specific type
   - `official website` (P856): your URL
   - `inception` (P571): founding date
   - `headquarters location` (P159): city
   - `industry` (P452): your industry
   - `founded by` (P112): founder name(s)
   - `social media links`: LinkedIn (P4264), YouTube (P2397), Twitter (P2002), GitHub (P2037)
5. Save and note your Q-number (e.g., Q12345678)
6. Add this Q-number URL to your Organization schema `sameAs`

**When to hire a Wikipedia consultant:**
- Revenue >$10M and clear notability signals
- Budget $5,000-$15,000 for article creation + maintenance
- Reputable firms: Beutler Ink, Rhiannon Ruff, WikiExperts
- NEVER edit your own Wikipedia article (conflict of interest policy)

### LinkedIn: Company Page Optimization

**Complete these fields (takes 30-60 minutes):**

1. **Header image**: branded, professional (1128x191 px)
2. **Description**: 2-3 paragraphs with keywords (2,000 char max)
3. **Website URL**: verified
4. **Industry**: correct classification
5. **Company size**: accurate range
6. **Headquarters**: full address
7. **Founded**: year
8. **Specialties**: list all (up to 20)

**Employee thought leadership program:**
- Ask 3-5 leaders to post 1x/week about industry topics
- Content should mention brand naturally, not promotionally
- Engage with industry discussions and tag company page
- Publish LinkedIn Articles (long-form) monthly on core expertise topics

---

## 4. Schema Implementation

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

2. **Generate the JSON-LD** (use Merkle generator or write manually):

```json
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "@id": "https://yourdomain.com/#organization",
  "name": "Your Brand Name",
  "url": "https://yourdomain.com",
  "logo": {
    "@type": "ImageObject",
    "url": "https://yourdomain.com/logo.png",
    "width": 600,
    "height": 60
  },
  "description": "One-sentence description of what your company does.",
  "foundingDate": "2020-01-15",
  "sameAs": [
    "https://en.wikipedia.org/wiki/Your_Brand",
    "https://www.wikidata.org/wiki/Q12345",
    "https://www.linkedin.com/company/yourbrand",
    "https://www.youtube.com/@yourbrand",
    "https://twitter.com/yourbrand",
    "https://github.com/yourbrand"
  ],
  "knowsAbout": [
    "Your Expertise Area 1",
    "Your Expertise Area 2",
    "Your Expertise Area 3"
  ]
}
</script>
```

3. **Place in HTML `<head>`** — NOT injected via JavaScript (AI crawlers do not execute JS)
4. **Validate** at https://search.google.com/test/rich-results
5. **Verify each sameAs URL resolves** (no 404s)

### Step-by-Step: Article + Author Schema with speakable

```json
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Your Article Title",
  "datePublished": "2026-03-01T08:00:00Z",
  "dateModified": "2026-03-10T14:30:00Z",
  "image": "https://yourdomain.com/images/article-hero.jpg",
  "author": {
    "@type": "Person",
    "@id": "https://yourdomain.com/about/author-name#person",
    "name": "Author Name",
    "url": "https://yourdomain.com/about/author-name",
    "jobTitle": "Senior Engineer",
    "worksFor": { "@id": "https://yourdomain.com/#organization" },
    "knowsAbout": ["Topic 1", "Topic 2"],
    "sameAs": [
      "https://www.linkedin.com/in/authorname",
      "https://twitter.com/authorname",
      "https://scholar.google.com/citations?user=XXXX"
    ]
  },
  "publisher": { "@id": "https://yourdomain.com/#organization" },
  "speakable": {
    "@type": "SpeakableSpecification",
    "cssSelector": [".article-summary", ".key-takeaway", "h2 + p"]
  }
}
</script>
```

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

## 5. Technical Fixes

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

---

## 6. E-E-A-T Improvement

E-E-A-T is 20% of the composite GEO score. Per Google's Dec 2025 Quality Rater Guidelines, E-E-A-T now applies to ALL competitive queries.

### Action Summary

| Action | Effort | Impact | Timeline | Tools |
|--------|--------|--------|----------|-------|
| Create author pages | Medium | +9 pts E-E-A-T | 1-2 days | CMS |
| Add first-person experience to content | Medium | +5-10 pts E-E-A-T | 2-4 weeks | — |
| Create editorial policy page | Low | +3 pts E-E-A-T | 1-2 hours | Template below |
| Add disclosure templates | Low | +3 pts E-E-A-T | 30 min | Template below |
| Build external citations | High | +5-10 pts E-E-A-T | 3-6 months | HARO, Qwoted, PR |

### Author Page Template

Create a dedicated page at `/about/[author-name]` with this structure:

```markdown
# [Author Name]

[Author Name] is the [Job Title] at [Company], where [he/she/they]
[what they do]. With [N] years of experience in [field], [Author Name]
has [key accomplishment or credential].

## Credentials
- [Degree], [University], [Year]
- [Certification], [Issuing Body]
- [Professional License]

## Experience
- [Current Role] at [Company] ([Year]-Present)
- [Previous Role] at [Previous Company] ([Years])
- [Key achievement with specific numbers]

## Published Work
- "[Article Title]" — [Publication Name] ([Year])
- "[Article Title]" — [Publication Name] ([Year])

## Speaking
- [Conference Name] — "[Talk Title]" ([Year])
- [Podcast Name] — Episode [N]: "[Title]" ([Year])

## Connect
- LinkedIn: [URL]
- Twitter: [URL]
- GitHub: [URL]
```

**Important:** Link this author page from every article byline AND include the URL in your Person schema's `url` property.

### Editorial Policy Template

Create at `/editorial-policy`:

```markdown
# Editorial Policy

## Our Standards
All content published on [Site Name] undergoes editorial review for
accuracy, clarity, and completeness. We are committed to providing
trustworthy, well-researched information.

## Fact-Checking Process
- All statistics are verified against primary sources
- Claims are cross-referenced with at least two independent sources
- Technical content is reviewed by subject matter experts
- Publication dates and "last updated" dates are displayed on all content

## Corrections Policy
If you find an error in our content, please contact us at
[corrections@yourdomain.com]. We will:
1. Acknowledge the report within 48 hours
2. Investigate and verify the claim
3. Issue a correction with a visible note on the article if warranted
4. Update the "last modified" date

## Author Qualifications
All authors on [Site Name] have demonstrated expertise in their subject
areas. See individual author pages for credentials and background.

## Conflicts of Interest
We disclose all affiliate relationships, sponsored content, and material
conflicts of interest. See our [Disclosure Policy](/disclosure).
```

### Adding First-Person Experience to Existing Content

AI platforms increasingly distinguish between "content about a topic" and "content from someone who has done it." Add experience signals:

**Phrases to weave into existing content:**
- "When we implemented [X] for [client/our team], we found..."
- "I've tested [product] over [timeframe] and the results were..."
- "Based on our experience with [N] deployments, the biggest challenge is..."
- "Here's a screenshot from our actual [dashboard/setup/process]:"
- "The mistake we made initially was [specific error], which taught us..."

**Per article, add at least:**
- 1 first-person account of direct experience
- 1 specific example with names, numbers, or dates
- 1 lesson learned from personal experience
- 1 screenshot or photo showing direct involvement (if applicable)

### Getting Cited by Authoritative Sources

This is the hardest but highest-impact E-E-A-T action.

**Reactive methods (respond to journalist requests):**
- HARO (helpareporter.com) — journalists requesting expert sources, free
- Qwoted (qwoted.com) — similar to HARO, more tech/business focused
- Terkel (terkel.io) — expert quote marketplace
- Response time matters: reply within 2 hours of the query

**Proactive methods:**
- Publish original research that journalists will cite (surveys, benchmarks, analyses)
- Create embeddable assets (infographics, data visualizations, calculators)
- Offer exclusive data to industry publications
- Write guest posts for authoritative sites in your field

### Disclosure Templates

**Affiliate disclosure (add to relevant pages):**
```markdown
**Disclosure:** Some links in this article are affiliate links. We may
earn a commission if you make a purchase through these links, at no
additional cost to you. This does not influence our editorial opinions.
See our full [Disclosure Policy](/disclosure).
```

**Sponsored content disclosure (add at top of sponsored posts):**
```markdown
**Sponsored Content:** This article was created in partnership with
[Brand Name]. While [Brand Name] sponsored this content, all opinions
and editorial decisions are our own. See our [Editorial Policy](/editorial-policy).
```

**Do this now:**
1. Create author pages for your top 3 content creators
2. Add the editorial policy page (copy template above, customize)
3. Add disclosure statements to any pages with affiliate links

---

## 7. Platform-Specific Onboarding

Platform optimization is 10% of the composite GEO score. Each platform has different priorities. Here is a "getting started in 30 minutes" checklist for each.

### Google AIO: 30-Minute Onboarding

| Step | Action | Time |
|------|--------|------|
| 1 | Verify site in Google Search Console (search.google.com/search-console) | 5 min |
| 2 | Submit XML sitemap in GSC | 2 min |
| 3 | Check "Pages" report for indexing issues | 5 min |
| 4 | Pick your top 3 pages. Add question-based H2 headings that match "People Also Ask" | 10 min |
| 5 | For each question heading, write a direct 1-2 sentence answer as the first paragraph | 8 min |

**Ongoing:** Convert one comparison to a table per week. Add one FAQ section per week.

### ChatGPT: 30-Minute Onboarding

| Step | Action | Time |
|------|--------|------|
| 1 | Register at Bing Webmaster Tools (bing.com/webmasters) | 5 min |
| 2 | Submit XML sitemap to Bing | 2 min |
| 3 | Search your brand on Wikidata (wikidata.org). Create entry if missing. | 10 min |
| 4 | Verify robots.txt allows GPTBot and OAI-SearchBot | 3 min |
| 5 | Check entity consistency: is brand name identical on website, LinkedIn, Wikidata? | 5 min |
| 6 | Search your brand in ChatGPT — note what it knows and what's wrong | 5 min |

**Ongoing:** Build toward Wikipedia notability. Maintain Reddit presence.

### Perplexity: 30-Minute Onboarding

| Step | Action | Time |
|------|--------|------|
| 1 | Verify robots.txt allows PerplexityBot | 2 min |
| 2 | Search your brand on Perplexity — note current citations | 5 min |
| 3 | Identify 3 subreddits where your audience is active (use Gummy Search) | 10 min |
| 4 | Create Reddit account if needed. Start lurking in those subreddits. | 3 min |
| 5 | Check publication dates on your top pages. Add visible dates if missing. | 5 min |
| 6 | Pick one page and add 3 sourced statistics | 5 min |

**Ongoing:** Post helpful content on Reddit weekly. Publish original data monthly.

### Gemini: 30-Minute Onboarding

| Step | Action | Time |
|------|--------|------|
| 1 | Claim Google Business Profile (business.google.com) if applicable | 5 min |
| 2 | Create or verify YouTube channel. Upload at least one video. | 10 min |
| 3 | Add Organization schema with sameAs (include YouTube, Wikipedia, LinkedIn) | 10 min |
| 4 | Search your brand on Google — check if Knowledge Panel appears. If yes, claim it. | 3 min |
| 5 | Verify robots.txt allows Google-Extended | 2 min |

**Ongoing:** Upload YouTube content monthly. Optimize GBP with photos and posts weekly.

### Copilot: 30-Minute Onboarding

| Step | Action | Time |
|------|--------|------|
| 1 | Register at Bing Webmaster Tools (if not done for ChatGPT step) | 5 min |
| 2 | Implement IndexNow (install plugin or create key file) | 10 min |
| 3 | Optimize meta descriptions on top 5 pages (Bing weights these heavily) | 10 min |
| 4 | Verify LinkedIn company page is complete | 3 min |
| 5 | Register at Bing Places (bingplaces.com) if local business | 2 min |

**Ongoing:** Keep IndexNow active. Post on LinkedIn weekly.

---

## 8. Monitoring and Iteration

### Re-Audit Frequency

| Site Activity Level | Re-Audit Frequency | Focus |
|--------------------|-------------------|-------|
| Publishing 4+ posts/week | Monthly | Citability, freshness, new page schema |
| Publishing 1-3 posts/week | Every 6 weeks | Full audit |
| Publishing < 1 post/week | Quarterly | Full audit |
| After major site changes | Immediately | Technical + schema |

### Track AI Traffic in GA4

AI platforms show up as referral sources. Set up a custom report:

1. Go to GA4 > Reports > Acquisition > Traffic Acquisition
2. Add secondary dimension: "Session source/medium"
3. Filter for AI sources:

| Source | What It Indicates |
|--------|------------------|
| `chatgpt.com / referral` | ChatGPT cited you with a link |
| `perplexity.ai / referral` | Perplexity cited you |
| `gemini.google.com / referral` | Gemini sent traffic |
| `copilot.microsoft.com / referral` | Copilot cited you |
| `bing.com / referral` (with AI indicators) | Bing Copilot inline citations |

**Set up a GA4 custom channel group:**
1. Admin > Data display > Channel groups > Create new
2. Add rule: Source matches regex `chatgpt|perplexity|gemini|copilot|claude`
3. Name it "AI Search"
4. Now you can track AI search as a distinct channel

### Manual Citation Checks

Until automated tools mature, manually check AI citations monthly:

1. **ChatGPT:** Ask "What is [your brand]?" and "What are the best [your category] tools?" Note if and how you're cited.
2. **Perplexity:** Search your brand name and your top keywords. Check sources listed.
3. **Google AIO:** Search your target keywords on Google. Check if AI Overview appears and whether you're cited.
4. **Gemini:** Ask Gemini about your brand and category. Note responses.

**Track in a spreadsheet:**

| Date | Platform | Query | Cited? | Position | Notes |
|------|----------|-------|--------|----------|-------|
| 2026-03-11 | ChatGPT | "best CDN providers" | Yes | Source 2 | Cited pricing page |
| 2026-03-11 | Perplexity | "best CDN providers" | No | — | Reddit thread cited instead |

### Prioritization Framework

Fix issues in this order — severity determines sequence, not dimension:

| Priority | Severity | Examples | Expected Lift |
|----------|----------|----------|---------------|
| 1 | Critical | AI crawlers blocked, site 100% client-rendered, HTTPS missing | +20-40 pts composite |
| 2 | High | No schema, no author info, thin content, no sameAs links | +10-20 pts composite |
| 3 | Medium | No llms.txt, stale content, incomplete schema, missing CWV optimization | +5-10 pts composite |
| 4 | Low | Tier 3 crawler access, minor CWV improvements, secondary platform presence | +1-5 pts composite |

### Monthly Action Cycle

| Week | Focus |
|------|-------|
| Week 1 | Re-audit top 5 pages. Fix any new Critical/High issues. |
| Week 2 | Content updates — add statistics, refresh dates, improve citability. |
| Week 3 | Brand building — Reddit participation, YouTube upload, LinkedIn post. |
| Week 4 | Technical check — schema validation, CWV monitoring, crawler access verification. |

**Do this now:**
1. Set a monthly calendar reminder for GEO re-audit
2. Set up the GA4 custom channel group for AI traffic
3. Do one manual citation check across all 5 platforms
4. Create the tracking spreadsheet
