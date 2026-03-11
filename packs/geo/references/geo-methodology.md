---
date: 2026-03-11
topic: GEO (Generative Engine Optimization)
category: Marketing/SEO
source: Synthesized from geo-seo-claude (MIT), Ahrefs Dec 2025 study, Princeton/Georgia Tech/IIT Delhi 2024 GEO research
---

# GEO Methodology Reference

> AI search optimization methodology. Referenced by geo-audit, geo-citability, geo-optimize skills.

## Core Thesis

AI search is restructuring web traffic distribution. Traditional SEO optimizes for Google's link-based ranking. GEO optimizes for **AI citability** — whether AI systems extract and quote your content as a source.

Key data points:
- Brand mentions correlate ~3x more with AI visibility than backlinks (Ahrefs Dec 2025, 75K brands)
- YouTube mention correlation with AI citation: ~0.737 vs backlinks: ~0.266
- Only 11% of domains are cited by both ChatGPT and Google AIO for the same query
- GEO-optimized content: 30-115% higher visibility in AI responses (Princeton/Georgia Tech/IIT Delhi 2024)

---

## 1. Citability Scoring Framework

> **SSOT**: Full scoring rubrics (per-dimension score bands, examples, detection patterns, analysis procedure) are in `../geo-citability/SKILL.md`. Below is the summary only.

### 5 Dimensions

| Dimension | Weight |
|-----------|--------|
| Answer Block Quality | 30% |
| Self-Containment | 25% |
| Structural Readability | 20% |
| Statistical Density | 15% |
| Uniqueness & Original Data | 10% |

### Key Research Data

- **Optimal length**: 134-167 words (Bortolato 2025)
- **Definition patterns**: +2.1x citation (Georgia Tech 2024)
- **Statistics**: +40% citation (Princeton 2024)
- **Authority quotations**: +115% in some categories (IIT Delhi 2024)
- **Fluency optimization**: +30% average visibility
- **Source citations**: +20-25% citation by Perplexity and ChatGPT

---

## 2. AI Crawler Reference

### Tier 1: Critical for AI Search (ALLOW)

| Crawler | Operator | User-Agent | Purpose |
|---------|----------|-----------|---------|
| GPTBot | OpenAI | `GPTBot` | ChatGPT search + browsing |
| OAI-SearchBot | OpenAI | `OAI-SearchBot` | Search-only, no training |
| ChatGPT-User | OpenAI | `ChatGPT-User` | User-initiated URL visits |
| ClaudeBot | Anthropic | `ClaudeBot` | Web search + analysis |
| PerplexityBot | Perplexity | `PerplexityBot` | AI search with source attribution |

### Tier 2: Broader Ecosystem (ALLOW)

| Crawler | Operator | Notes |
|---------|----------|-------|
| Google-Extended | Google | Gemini features. Does NOT affect search ranking. |
| GoogleOther | Google | Research + experimental features |
| Applebot-Extended | Apple | Apple Intelligence (2B+ devices) |
| Amazonbot | Amazon | Alexa + Amazon AI |
| FacebookBot | Meta | Meta AI (3B+ app users) |

### Tier 3: Training-Only (Context-Dependent)

| Crawler | Recommendation | Notes |
|---------|---------------|-------|
| CCBot | Allow/Block | Common Crawl dataset. No live search impact. |
| anthropic-ai | Allow/Block | Training only. ClaudeBot handles live features. |
| Bytespider | **Block** | Aggressive crawling, minimal benefit for Western markets |
| cohere-ai | Allow/Block | Low priority |

### robots.txt Template (Maximum AI Visibility)

```
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

User-agent: Bytespider
Disallow: /
```

---

## 3. Platform-Specific Optimization

### Google AI Overviews (AIO)

- 92% of AIO citations from pages already ranking top 10
- 47% from pages ranking below position 5 (AIO has own selection logic)
- Strongly favors: question headings, direct answers, tables, lists, FAQ sections
- Featured snippet optimization has ~70% overlap with AIO optimization

**Priority checklist**: Top-10 ranking → Question H2s → Direct answers → Tables/lists → FAQ section → Statistics with sources → Visible dates → Author byline

### ChatGPT Web Search

- Uses **Bing's index** (not Google)
- Top sources: Wikipedia (47.9%), Reddit (11.3%), YouTube, major news
- Heavily weights **entity recognition** — Wikipedia/Wikidata presence critical
- Prefers comprehensive content (2000+ words)

**Priority checklist**: Wikipedia/Wikidata entity → Bing Webmaster Tools → Reddit authority → YouTube → Authoritative backlinks (.edu, .gov) → Entity consistency → Comprehensive content

### Perplexity AI

- Top sources: **Reddit (46.7%)**, Wikipedia, YouTube, publications
- Heaviest emphasis on **community validation**
- Freshness is strong ranking signal
- Cites 5-15 sources per answer (more opportunity for mid-authority sites)

**Priority checklist**: Active Reddit presence → Forum/community mentions → Content freshness → Original research → YouTube with transcripts → Multi-source claim validation

### Google Gemini

- Uses Google's index + **strong Google ecosystem weighting**
- YouTube weighted significantly more than in standard Search
- Direct access to Google Business Profile and Knowledge Graph
- Multi-modal: references images, videos, text together

**Priority checklist**: Knowledge Panel → Google Business Profile → YouTube with chapters → Schema.org (comprehensive) → Google ecosystem (Scholar, News, Maps) → Image optimization → E-E-A-T

### Bing Copilot

- Bing's index (shared infra with ChatGPT, different ranking)
- Supports **IndexNow** for near-instant indexing
- Microsoft ecosystem: LinkedIn, GitHub, Microsoft Learn
- Weights meta descriptions more than Google does

**Priority checklist**: IndexNow → Bing Webmaster Tools → LinkedIn company page → Meta descriptions → Exact-match keywords → Fast page load (<2s)

### Cross-Platform Priorities

| Priority | AIO | ChatGPT | Perplexity | Gemini | Copilot |
|----------|-----|---------|------------|--------|---------|
| #1 | Top-10 ranking | Wikipedia | Reddit | YouTube | IndexNow |
| #2 | Q&A structure | Entity graph | Original research | Knowledge Panel | Bing WMT |
| #3 | Tables/lists | Bing SEO | Freshness | Schema.org | LinkedIn |

### Universal Actions (help ALL platforms)

1. Wikipedia/Wikidata entity presence
2. YouTube channel with relevant content
3. Well-structured content with clear headings
4. Schema.org (Organization + sameAs)
5. Fast page load + clean HTML
6. Author pages with credentials + sameAs
7. Regular content updates with visible dates

---

## 4. Schema Strategy for GEO

### sameAs — The Most Important GEO Property

`sameAs` tells AI: "This entity on my site IS the same entity as these profiles." Creates the entity graph AI uses to verify, trust, and cite.

**Priority order:**
1. Wikipedia article
2. Wikidata item (Q-number)
3. LinkedIn (company/personal)
4. YouTube channel
5. Twitter/X
6. Facebook page
7. Crunchbase (startups/tech)
8. GitHub (tech companies)
9. Google Scholar / ORCID (academics)

### GEO-Specific Schema Properties

| Property | Schema Type | Why It Matters |
|----------|------------|---------------|
| `sameAs` | Organization, Person | Entity graph — AI identity verification |
| `knowsAbout` | Organization, Person | Tells AI what topics this entity is expert in |
| `speakable` | Article, WebPage | Marks passages for voice/AI assistant extraction |
| `dateModified` | Article | Freshness signal — AI deprioritizes stale content |

### Business-Type Schema Map

| Type | Required Schemas |
|------|-----------------|
| All | Organization + WebSite + SearchAction |
| SaaS | + SoftwareApplication with featureList |
| Local | + LocalBusiness with geo, hours, reviews |
| E-commerce | + Product with offers, shipping, returns |
| Publisher | + Article + Author (Person) with speakable |

### Deprecated/Changed Schemas

| Schema | Status (2024+) | GEO Relevance |
|--------|---------------|--------------|
| HowTo | Rich results deprecated | Still useful for AI parsing |
| FAQPage | Restricted to govt/health | Still parsed by AI platforms |
| SpecialAnnouncement | Deprecated | Remove |

---

## 5. E-E-A-T for GEO

Per Google Dec 2025 QRG update: E-E-A-T now applies to ALL competitive queries, not just YMYL.

### Scoring (25 points each)

**Experience**: First-person accounts, original research, case studies, process demonstrations
**Expertise**: Author credentials, technical depth, methodology, data-backed claims
**Authoritativeness**: External citations, media mentions, awards, topical coverage breadth
**Trustworthiness**: Contact info, privacy policy, editorial standards, accuracy, disclosures

### AI Content Quality Signals

**Low-quality flags**: "In today's fast-paced world...", generic advice, no first-hand experience, hedging overload, filler content
**High-quality signals**: Original data, specific examples, contrarian views backed by reasoning, first-person experience, practical recommendations

---

## 6. Technical GEO Requirements

### SSR is Mandatory

AI crawlers (GPTBot, ClaudeBot, PerplexityBot) do **NOT execute JavaScript**. Client-rendered SPAs are invisible to AI search. Check with `curl -s [URL]` — if content is missing from raw HTML, AI crawlers can't see it.

### Core Web Vitals Thresholds

| Metric | Good | Poor |
|--------|------|------|
| LCP | <2.5s | >4.0s |
| INP | <200ms | >500ms |
| CLS | <0.1 | >0.25 |

### IndexNow

Open protocol for instant Bing/Yandex/Seznam indexing. ChatGPT and Copilot use Bing's index — faster Bing indexing = faster AI visibility on two major platforms.

### llms.txt

Emerging standard (Jeremy Howard) for AI crawler guidance. Place at site root. Contains: title, description, sections with categorized internal links. Helps AI crawlers understand site structure.

---

## 7. Composite GEO Score Weights

| Category | Weight |
|----------|--------|
| AI Citability & Visibility | 25% |
| Brand Authority Signals | 20% |
| Content Quality & E-E-A-T | 20% |
| Technical Foundations | 15% |
| Structured Data | 10% |
| Platform Optimization | 10% |

### Score Interpretation

| Range | Rating |
|-------|--------|
| 85-100 | Dominant — highly likely to be cited across AI platforms |
| 70-84 | Strong — solid AI presence with specific gaps |
| 50-69 | Moderate — inconsistent AI visibility |
| 30-49 | Weak — significant GEO gaps |
| 0-29 | Minimal — fundamental strategy overhaul needed |
