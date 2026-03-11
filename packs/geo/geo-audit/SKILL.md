---
name: geo-audit
description: >
  GEO multi-dimension audit for AI search visibility. Use when auditing a website's
  discoverability across AI platforms (ChatGPT, Perplexity, Gemini, Google AIO, Copilot).
  Triggers on "GEO audit", "AI search optimization", "AI visibility audit", "SEO for AI",
  "audit site for AI", "how visible is my site to AI". Scores citability, brand authority,
  technical foundations, schema, content quality, and platform-specific readiness with
  weighted composite scoring.
model: sonnet
allowed-tools:
  - Read
  - Grep
  - Glob
  - Bash
  - WebFetch
  - Write
  - Agent
---

# GEO Audit Skill

> Generative Engine Optimization audit — score a website's AI search visibility across 6 dimensions.

## References

Before starting, read the methodology reference for scoring rubrics, crawler lists, and platform criteria. The file is a sibling directory to this skill:

```
../references/geo-methodology.md
```

Resolve relative to this SKILL.md's parent directory. For example, if this skill is at `~/.claude/skills/geo-audit/SKILL.md` (symlinked to `~/.skm/cache/geo/packs/geo/geo-audit/SKILL.md`), the reference is at `~/.skm/cache/geo/packs/geo/references/geo-methodology.md`.

## Quick Reference

| Command | What It Does |
|---------|-------------|
| `/geo-audit <url>` | Full multi-dimension GEO audit |
| `/geo-audit <url> quick` | 60-second snapshot (citability + crawlers only) |

---

## Audit Flow

### Phase 1: Discovery (Sequential)

1. **Fetch homepage** via WebFetch
2. **Detect business type** from signals:

| Type | Signals |
|------|---------|
| SaaS | Pricing page, "Sign up", "Free trial", "/app", "/dashboard", API docs |
| Local | Phone, address, "Near me", Google Maps embed, service area |
| E-commerce | Product pages, cart, price elements, product schema |
| Publisher | Blog, articles, bylines, publication dates, article schema |
| Agency | Portfolio, case studies, "Our services", client logos |

3. **Extract key pages** from sitemap.xml or internal links (max 20 pages)

### Phase 2: Parallel Analysis (5 Subagents)

Spawn 5 agents simultaneously:

```
Agent 1: AI Visibility   → Citability scoring + AI crawler access + brand mentions
Agent 2: Platform         → Per-platform optimization (AIO, ChatGPT, Perplexity, Gemini, Copilot)
Agent 3: Technical        → SSR, Core Web Vitals, crawlability, security, mobile
Agent 4: Content          → E-E-A-T assessment, content quality, freshness
Agent 5: Schema           → JSON-LD detection, validation, sameAs audit, generation
```

Each agent should read `../references/geo-methodology.md` (resolved from this skill's directory) for scoring rubrics and platform-specific criteria.

### Phase 3: Synthesis (Sequential)

1. Collect all agent reports
2. Calculate composite GEO Score using weights below
3. Generate prioritized action plan by severity

---

## Composite GEO Score (0-100)

| Category | Weight | What It Measures |
|----------|--------|-----------------|
| AI Citability & Visibility | 25% | Passage scoring, answer blocks, AI crawler access, llms.txt |
| Brand Authority Signals | 20% | YouTube (~0.737 correlation), Reddit, Wikipedia, LinkedIn presence |
| Content Quality & E-E-A-T | 20% | Experience, Expertise, Authoritativeness, Trustworthiness |
| Technical Foundations | 15% | SSR (critical for AI crawlers), CWV, crawlability, mobile, security |
| Structured Data | 10% | Schema completeness, sameAs links, JSON-LD validation |
| Platform Optimization | 10% | Per-platform readiness scores averaged |

```
GEO_Score = (Citability * 0.25) + (Brand * 0.20) + (Content * 0.20)
          + (Technical * 0.15) + (Schema * 0.10) + (Platform * 0.10)
```

---

## Subagent Instructions

### Agent 1: AI Visibility

Analyze:

**Citability** (use geo-citability skill rubric):
- Score content blocks on 5 dimensions: Answer Block Quality (30%), Self-Containment (25%), Structural Readability (20%), Statistical Density (15%), Uniqueness (10%)
- Optimal passage length: 134-167 words
- Identify top 3 strongest and bottom 3 weakest blocks

**AI Crawler Access**:
- Fetch robots.txt, check all 14 AI crawlers (see geo-methodology.md for full list)
- Tier 1 (must allow): GPTBot, OAI-SearchBot, ChatGPT-User, ClaudeBot, PerplexityBot
- Tier 2 (should allow): Google-Extended, GoogleOther, Applebot-Extended, Amazonbot, FacebookBot
- Tier 3 (context-dependent): CCBot, anthropic-ai, Bytespider, cohere-ai
- Check meta robots tags and X-Robots-Tag headers on sample pages
- Check for llms.txt presence

**Brand Mentions**:
- Check Wikipedia/Wikidata via API (most reliable method)
- Check YouTube, Reddit, LinkedIn, other platforms for brand presence
- Score with weights: YouTube 25%, Reddit 25%, Wikipedia 20%, LinkedIn 15%, Other 15%

### Agent 2: Platform Analysis

Score each platform 0-100 using platform-specific rubrics from geo-methodology.md:

| Platform | #1 Priority | #2 Priority | #3 Priority |
|----------|-------------|-------------|-------------|
| Google AIO | Top-10 ranking | Q&A structure + tables | Featured snippet patterns |
| ChatGPT | Wikipedia entity | Bing index + entity graph | Reddit + comprehensive content |
| Perplexity | Reddit presence (46.7% citations) | Original research | Freshness + community validation |
| Gemini | YouTube content | Knowledge Panel + Schema.org | Google ecosystem presence |
| Copilot | IndexNow protocol | Bing Webmaster Tools | LinkedIn + meta descriptions |

Cross-platform universal actions: Wikipedia/Wikidata entity, YouTube, structured content, Schema.org (Organization + sameAs), fast load, author pages, visible dates.

### Agent 3: Technical

Score 0-100 across 8 categories:
- Crawlability (15pts): robots.txt, sitemap, internal linking
- Indexability (12pts): Canonicals, duplicates, pagination
- Security (10pts): HTTPS, security headers
- URL Structure (8pts): Clean URLs, redirect chains
- Mobile (10pts): Viewport, tap targets, font sizes
- Core Web Vitals (15pts): LCP <2.5s, INP <200ms, CLS <0.1
- **SSR (15pts — GEO critical)**: AI crawlers do NOT execute JS. If content requires JS rendering, AI crawlers see empty pages.
- Page Speed (15pts): TTFB, resource optimization, CDN

### Agent 4: Content

Score E-E-A-T (25pts each dimension = 100 total + topical authority modifier):
- **Experience**: First-person accounts, original research, case studies, screenshots
- **Expertise**: Author credentials, technical depth, methodology, data-backed claims
- **Authoritativeness**: External citations, media mentions, awards, topical coverage
- **Trustworthiness**: Contact info, privacy policy, editorial standards, accuracy

Also assess: content freshness, AI content quality signals, readability, paragraph structure.

### Agent 5: Schema

- Detect all JSON-LD, Microdata, RDFa on key pages
- Validate against Schema.org specs
- Audit sameAs links (the single most important GEO property)
- Check for: Organization, Article+Author, business-type-specific schemas
- Check for GEO-specific properties: `knowsAbout`, `speakable`, complete sameAs
- Generate ready-to-paste JSON-LD for missing schemas
- Flag deprecated schemas (HowTo rich results, FAQPage restrictions)

---

## Output Format

Generate `GEO-AUDIT-REPORT.md`:

```markdown
# GEO Audit Report — [Domain]
Date: [Date]
Business Type: [Detected Type]

## GEO Score: XX/100

## Score Breakdown
| Category | Score | Weight | Weighted | Status |
|----------|-------|--------|----------|--------|
| AI Citability & Visibility | XX/100 | 25% | XX | [Strong/Moderate/Weak] |
| Brand Authority Signals | XX/100 | 20% | XX | ... |
| Content Quality & E-E-A-T | XX/100 | 20% | XX | ... |
| Technical Foundations | XX/100 | 15% | XX | ... |
| Structured Data | XX/100 | 10% | XX | ... |
| Platform Optimization | XX/100 | 10% | XX | ... |

## AI Platform Readiness
| Platform | Score | Key Gap |
|----------|-------|---------|
| Google AIO | XX/100 | [One-line gap] |
| ChatGPT | XX/100 | ... |
| Perplexity | XX/100 | ... |
| Gemini | XX/100 | ... |
| Copilot | XX/100 | ... |

## Critical Issues (fix immediately)
1. [Issue with specific URL and evidence]

## Quick Wins (this week)
1. [Action with expected impact]

## Medium-Term (this month)
1. [Action]

## Strategic (this quarter)
1. [Action]

## Detailed Findings
[Per-category breakdown with evidence]
```

---

## Quick Audit Mode

When user adds `quick`:
1. Only run citability + crawler access (no subagents)
2. Fetch homepage only
3. Score citability on homepage content blocks
4. Check robots.txt for AI crawlers
5. Output inline summary (no file), ~60 seconds

---

## Severity Classification

| Level | Definition | Example |
|-------|-----------|---------|
| Critical | Blocking AI visibility entirely | All Tier 1 crawlers blocked, site is 100% client-rendered |
| High | Significantly reducing AI citations | No schema.org, no author info, thin content |
| Medium | Missing optimization opportunities | No llms.txt, incomplete sameAs, stale content |
| Low | Nice-to-have improvements | Tier 3 crawler access, minor CWV improvements |
