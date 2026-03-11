---
name: geo-audit
description: >
  GEO multi-dimension audit for AI search visibility. Use when auditing a website's
  discoverability across AI platforms (ChatGPT, Perplexity, Gemini, Google AIO, Copilot).
  Triggers on "GEO audit", "AI search optimization", "AI visibility audit", "SEO for AI",
  "audit site for AI", "how visible is my site to AI". Produces a weighted composite score
  across 6 dimensions with prioritized action plan.
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

> Generative Engine Optimization audit -- score a website's AI search visibility across 6 dimensions.

## Quick Reference

| Command | What It Does |
|---------|-------------|
| `/geo-audit <url>` | Full multi-dimension GEO audit |
| `/geo-audit <url> quick` | 60-second snapshot (citability + crawlers only) |

---

## References

Read `../references/geo-methodology.md` first for composite weights, crawler lists, and severity levels.

Each subagent reads specific references before scoring:

| Agent | Must Read Before Scoring |
|-------|-------------------------|
| Agent 1: AI Visibility | `../references/citability-rubrics.md`, `../references/brand-authority.md` |
| Agent 2: Platform | `../references/platform-rubrics.md` |
| Agent 3: Technical | `../references/technical-scoring.md` |
| Agent 4: Content | `../references/eeat-content.md` |
| Agent 5: Schema | `../references/schema-templates.md` |

For Phase 3 (recommendations), read `../references/action-playbook.md` to generate specific, actionable improvement steps with effort/impact/timeline for each finding.

Resolve all paths relative to this SKILL.md's parent directory.

---

## Audit Flow

### Phase 1: Discovery (Sequential)

1. **Fetch homepage** via WebFetch
2. **Detect business type** from page signals (SaaS, Local, E-commerce, Publisher, Agency, Other). See `../references/geo-methodology.md` for signal table.
3. **Extract key pages** from sitemap.xml or internal links (max 20 pages)

### Phase 2: Parallel Analysis (5 Subagents)

Pass Phase 1 context to every subagent:

```
Context to include in each agent prompt:
- Target URL: [the URL being audited]
- Business Type: [detected type from Phase 1]
- Key Pages: [list of up to 20 URLs extracted from sitemap/internal links]
- Homepage HTML summary: [key meta tags, heading structure, detected schemas]
```

Spawn 5 agents simultaneously:

```
Agent 1: AI Visibility   -> Citability scoring + AI crawler access + brand mentions
Agent 2: Platform         -> Per-platform optimization (AIO, ChatGPT, Perplexity, Gemini, Copilot)
Agent 3: Technical        -> SSR, Core Web Vitals, crawlability, security, mobile
Agent 4: Content          -> E-E-A-T assessment, content quality, freshness
Agent 5: Schema           -> JSON-LD detection, validation, sameAs audit, generation
```

### Error Handling

| Failure | Action |
|---------|--------|
| WebFetch fails for a page | Skip that page, note in report, score based on accessible pages |
| robots.txt not found | Treat as "no restrictions" (all crawlers allowed), note in report |
| Subagent times out | Use partial results if available, mark category as "Incomplete" |
| Site is fully client-rendered | Agent 3 flags as Critical, other agents note limited analysis from raw HTML |

### Phase 3: Synthesis (Sequential)

1. Collect all agent reports
2. Calculate composite GEO Score using formula below
3. Generate prioritized action plan by severity

---

## Composite GEO Score (0-100)

| Category | Weight | Subagent |
|----------|--------|----------|
| AI Citability & Visibility | 25% | Agent 1 |
| Brand Authority Signals | 20% | Agent 1 |
| Content Quality & E-E-A-T | 20% | Agent 4 |
| Technical Foundations | 15% | Agent 3 |
| Structured Data | 10% | Agent 5 |
| Platform Optimization | 10% | Agent 2 |

```
GEO_Score = (Citability * 0.25) + (Brand * 0.20) + (Content * 0.20)
          + (Technical * 0.15) + (Schema * 0.10) + (Platform * 0.10)
```

---

## Subagent Instructions

### Agent 1: AI Visibility

Read `../references/citability-rubrics.md` for the 5-dimension rubrics (answer quality 30%, self-containment 25%, structure 20%, stats 15%, uniqueness 10%).

Read `../references/brand-authority.md` for platform scoring rubrics and composite formula (YouTube 25%, Reddit 25%, Wikipedia 20%, LinkedIn 15%, Other 15%).

Tasks:
- Score content blocks on 5 citability dimensions
- Identify top 3 strongest and bottom 3 weakest blocks
- Fetch robots.txt, check all 14 AI crawlers (see `../references/geo-methodology.md`)
- Check Wikipedia/Wikidata via API (see detection method in brand-authority.md)
- Score brand presence across YouTube, Reddit, Wikipedia, LinkedIn, other platforms

### Agent 2: Platform Analysis

Read `../references/platform-rubrics.md` for per-platform 0-100 scoring rubrics.

Score each platform using the point tables in the reference. Report per-platform scores and the single biggest gap for each.

### Agent 3: Technical

Read `../references/technical-scoring.md` for the 8-category breakdown (100 points total).

Score across: Crawlability (15pts), Indexability (12pts), Security (10pts), URL Structure (8pts), Mobile (10pts), Core Web Vitals (15pts), SSR (15pts -- GEO critical), Page Speed (15pts).

### Agent 4: Content

Read `../references/eeat-content.md` for E-E-A-T signal tables (25pts each) and content quality metrics.

Score all 4 E-E-A-T dimensions. Assess content freshness, AI content signals, readability. Apply topical authority modifier (+10 to -5).

### Agent 5: Schema

Read `../references/schema-templates.md` for schema types, sameAs strategy, and scoring rubric.

Detect all JSON-LD/Microdata/RDFa. Validate against Schema.org. Audit sameAs links. Check for GEO-specific properties (knowsAbout, speakable). Generate ready-to-paste JSON-LD for missing schemas. Flag deprecated schemas.

---

## Output Format

Generate `GEO-AUDIT-REPORT.md`:

```markdown
# GEO Audit Report -- [Domain]
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
