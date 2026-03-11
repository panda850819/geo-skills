# GEO Actions: Content

> Content-focused improvement actions for GEO scores. Covers citability quick wins and E-E-A-T improvement.

## Table of Contents

1. [Citability Quick Wins](#1-citability-quick-wins)
2. [E-E-A-T Improvement](#2-e-e-a-t-improvement)

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

## 2. E-E-A-T Improvement

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
