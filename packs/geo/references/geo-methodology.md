# GEO Methodology Reference

> Index file. Core thesis, composite scoring, and pointers to detailed reference files.

## Core Thesis

AI search is restructuring web traffic distribution. Traditional SEO optimizes for Google's link-based ranking. GEO optimizes for **AI citability** — whether AI systems extract and quote your content as a source.

Key data points:
- Brand mentions correlate ~3x more with AI visibility than backlinks (Ahrefs Dec 2025, 75K brands)
- YouTube mention correlation with AI citation: ~0.737 vs backlinks: ~0.266
- Only 11% of domains are cited by both ChatGPT and Google AIO for the same query
- GEO-optimized content: 30-115% higher visibility in AI responses (Princeton/Georgia Tech/IIT Delhi 2024)

---

## Composite GEO Score (0-100)

| Category | Weight | What It Measures | Detailed Reference |
|----------|--------|------------------|--------------------|
| AI Citability & Visibility | 25% | Passage scoring, answer blocks, AI crawler access | `citability-rubrics.md` |
| Brand Authority Signals | 20% | YouTube, Reddit, Wikipedia, LinkedIn presence | `brand-authority.md` |
| Content Quality & E-E-A-T | 20% | Experience, Expertise, Authoritativeness, Trustworthiness | `eeat-content.md` |
| Technical Foundations | 15% | SSR, CWV, crawlability, mobile, security | `technical-scoring.md` |
| Structured Data | 10% | Schema completeness, sameAs links, JSON-LD validation | `schema-templates.md` |
| Platform Optimization | 10% | Per-platform readiness scores averaged | `platform-rubrics.md` |

```
GEO_Score = (Citability * 0.25) + (Brand * 0.20) + (Content * 0.20)
          + (Technical * 0.15) + (Schema * 0.10) + (Platform * 0.10)
```

### Score Interpretation

| Range | Rating |
|-------|--------|
| 85-100 | Dominant — highly likely to be cited across AI platforms |
| 70-84 | Strong — solid AI presence with specific gaps |
| 50-69 | Moderate — inconsistent AI visibility |
| 30-49 | Weak — significant GEO gaps |
| 0-29 | Minimal — fundamental strategy overhaul needed |

---

## AI Crawler Reference

### Tier 1: Critical for AI Search (ALLOW)

| Crawler | Operator | User-Agent | Purpose |
|---------|----------|-----------|---------|
| GPTBot | OpenAI | `GPTBot` | ChatGPT search + browsing (300M+ weekly users) |
| OAI-SearchBot | OpenAI | `OAI-SearchBot` | Search-only, no training use |
| ChatGPT-User | OpenAI | `ChatGPT-User` | User-initiated URL visits |
| ClaudeBot | Anthropic | `ClaudeBot` | Web search + analysis |
| PerplexityBot | Perplexity | `PerplexityBot` | AI search with source attribution (best referral traffic) |

### Tier 2: Broader Ecosystem (ALLOW)

| Crawler | Operator | Notes |
|---------|----------|-------|
| Google-Extended | Google | Gemini features. Does NOT affect search ranking. |
| GoogleOther | Google | Research + experimental features |
| Applebot-Extended | Apple | Apple Intelligence (2B+ devices) |
| Amazonbot | Amazon | Alexa + Amazon AI |
| FacebookBot (Meta) | Meta | Meta AI (3B+ app users). Actual UA string: `facebookexternalhit` |

### Tier 3: Training-Only (Context-Dependent)

| Crawler | Recommendation | Notes |
|---------|---------------|-------|
| CCBot | Allow/Block | Common Crawl dataset. No live search impact. |
| anthropic-ai | Allow/Block | Training only. ClaudeBot handles live features. |
| Bytespider | **Block** | Aggressive crawling, minimal benefit for Western markets |
| cohere-ai | Allow/Block | Low priority |

### Full User-Agent Strings

| Crawler | Full UA String |
|---------|---------------|
| GPTBot | `Mozilla/5.0 AppleWebKit/537.36 (KHTML, like Gecko; compatible; GPTBot/1.2; +https://openai.com/gptbot)` |
| OAI-SearchBot | `Mozilla/5.0 AppleWebKit/537.36 (KHTML, like Gecko; compatible; OAI-SearchBot/1.0; +https://docs.openai.com/bots/overview)` |
| ChatGPT-User | `Mozilla/5.0 AppleWebKit/537.36 (KHTML, like Gecko; compatible; ChatGPT-User/1.0; +https://openai.com/bot)` |
| ClaudeBot | `ClaudeBot/1.0; +https://www.anthropic.com/claude-bot` |
| PerplexityBot | `Mozilla/5.0 AppleWebKit/537.36 (KHTML, like Gecko; compatible; PerplexityBot/1.0; +https://perplexity.ai/perplexitybot)` |
| Amazonbot | `Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_1) AppleWebKit/600.2.5 (KHTML, like Gecko) Version/8.0.2 Safari/600.2.5 (compatible; Amazonbot/0.1; +https://developer.amazon.com/support/amazonbot)` |
| CCBot | `CCBot/2.0 (https://commoncrawl.org/faq/)` |

### Recommendation Matrix

| Crawler | Tier | Recommendation | Impact of Blocking |
|---------|------|---------------|-------------------|
| GPTBot | 1 | **ALLOW** | Invisible in ChatGPT Search |
| OAI-SearchBot | 1 | **ALLOW** | Not in ChatGPT search results |
| ChatGPT-User | 1 | **ALLOW** | Users can't browse your pages via ChatGPT |
| ClaudeBot | 1 | **ALLOW** | Not accessible to Claude web search |
| PerplexityBot | 1 | **ALLOW** | Not in Perplexity results (loses referral traffic) |
| Google-Extended | 2 | **ALLOW** | May reduce Gemini/AIO presence |
| GoogleOther | 2 | **ALLOW** | Reduced Google AI research inclusion |
| Applebot-Extended | 2 | **ALLOW** | Not in Apple Intelligence features |
| Amazonbot | 2 | **ALLOW** | Not in Alexa voice responses |
| FacebookBot (Meta) | 2 | **ALLOW** | Not accessible to Meta AI. UA: `facebookexternalhit` |
| CCBot | 3 | Context | No live search impact |
| anthropic-ai | 3 | Context | No live search impact |
| Bytespider | 3 | **BLOCK** | Minimal impact, aggressive crawling |
| cohere-ai | 3 | Context | Minimal consumer impact |

### robots.txt Template

For a complete robots.txt template with AI crawler directives, see `actions-technical.md`.

---

## Business Type Detection

| Type | Signals |
|------|---------|
| **SaaS** | Pricing page, "Sign up", "Free trial", "/app", "/dashboard", API docs |
| **Local Service** | Phone number, address, "Near me", Google Maps embed, service area |
| **E-commerce** | Product pages, cart, "Add to cart", price elements, product schema |
| **Publisher** | Blog, articles, bylines, publication dates, article schema |
| **Agency** | Portfolio, case studies, "Our services", client logos, testimonials |
| **Other** | Default — apply general GEO best practices |

---

## Key Research Citations

- **Optimal passage length**: 134-167 words (Bortolato 2025 analysis of AI Overview passages)
- **Definition patterns**: +2.1x citation rate (Georgia Tech 2024)
- **Statistics in passages**: +40% citation (Princeton GEO study 2024)
- **Authority quotations**: +115% in certain categories (IIT Delhi 2024)
- **Fluency optimization**: +30% average visibility across all query types
- **Source citations**: +20-25% citation rate by Perplexity and ChatGPT
- **Brand mentions vs backlinks**: ~3x stronger correlation with AI visibility (Ahrefs Dec 2025, 75K brands)
- **AI crawler blocking**: 35%+ of top 1,000 websites block at least one major AI crawler (Originality.ai 2025)

---

## Severity Classification

| Level | Definition | Example |
|-------|-----------|---------|
| Critical | Blocking AI visibility entirely | All Tier 1 crawlers blocked, site is 100% client-rendered |
| High | Significantly reducing AI citations | No schema.org, no author info, thin content |
| Medium | Missing optimization opportunities | No llms.txt, incomplete sameAs, stale content |
| Low | Nice-to-have improvements | Tier 3 crawler access, minor CWV improvements |
