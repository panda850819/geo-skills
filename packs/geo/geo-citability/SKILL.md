---
name: geo-citability
description: >
  AI citability scoring for web content. Use when analyzing how likely AI systems
  will cite or quote passages from a page. Scores on 5 dimensions (answer quality,
  self-containment, structure, stats density, uniqueness) with rewrite suggestions.
  Works standalone or as part of geo-audit.
model: sonnet
allowed-tools:
  - Read
  - Grep
  - Glob
  - Bash
  - WebFetch
  - Write
---

# AI Citability Scoring

> Score content for AI citation readiness. How extractable and quotable are your passages?

## References

For full scoring rubrics, AI system citation preferences, and research data:

```
knowledge/Marketing/geo-methodology.md
```

## Core Insight

AI models cite passages that are **extractable** — self-contained, fact-rich, answer-first blocks that make sense without surrounding context. Research (Princeton, Georgia Tech, IIT Delhi 2024) found GEO-optimized content achieves 30-115% higher visibility in AI responses.

Key finding: AI systems preferentially cite passages that are:
- **134-167 words** long (optimal extraction length)
- **Self-contained** (understandable without context)
- **Fact-rich** (specific statistics, dates, named entities)
- **Answer-first** (direct answer in first 1-2 sentences)

This is fundamentally different from traditional SEO copywriting. GEO optimizes for **extractability**, not keyword density.

---

## Usage

```
/geo-citability <url>           # Score a page
/geo-citability <url> --block   # Score + show per-block breakdown
```

Also callable from `geo-audit` as part of the full audit flow.

---

## Scoring Rubric (0-100)

### Category 1: Answer Block Quality (30%)

Does content contain clear, quotable answer passages?

| Score | Criteria |
|-------|---------|
| 90-100 | Every section opens with 1-2 sentence direct answer. Uses "X is..." patterns. First 40-60 words stand alone. |
| 70-89 | Most sections have clear answer openings. Some definition patterns. |
| 50-69 | Some answer-like openings but many bury the answer mid-paragraph. |
| 30-49 | Answers generally buried. Narrative-driven, not answer-driven. |
| 0-29 | No identifiable answer blocks. AI would struggle to extract quotable passages. |

**Detection patterns:**
- Definition: "X is [definition]" / "X refers to [explanation]"
- Quantified: "The average cost of X is $Y"
- Comparison: "X differs from Y in three ways: [list]"
- Attribution: "According to [Source], [claim]"

**High-citability example:**
> Content delivery networks (CDNs) are distributed server systems that cache and serve web content from locations geographically close to end users. A CDN reduces latency by 50-70% on average by serving assets from edge servers rather than a single origin server. The three largest CDN providers as of 2025 are Cloudflare (serving approximately 20% of all websites), Amazon CloudFront, and Akamai Technologies.

58 words. Self-contained. 3 data points. Definition pattern. Score: 85+.

**Low-citability example:**
> If you've ever wondered why some websites load faster than others, the answer might surprise you. There's this amazing technology that has been around for a while now. Let me explain how it works and why you should care about it for your business.

52 words. Not self-contained (no topic named). 0 facts. No definition. Score: 15-.

### Category 2: Passage Self-Containment (25%)

Can passages be extracted and understood without surrounding context?

| Score | Criteria |
|-------|---------|
| 90-100 | 80%+ blocks fully self-contained. Each names its subject. No pronoun reliance. |
| 70-89 | 60-79% self-contained. Most name their subject. Occasional pronoun references. |
| 50-69 | 40-59% self-contained. Mixed explicit subjects and pronouns. |
| 30-49 | Heavy pronoun reliance. Most passages need surrounding text. |
| 0-29 | Continuous narrative. Extracting any paragraph loses meaning. |

**Checklist per passage:**
1. Names the subject explicitly (not "it", "this", "they")?
2. Main point understandable reading ONLY this passage?
3. Contains at least one fact, statistic, or named entity?
4. Between 50-200 words?
5. Avoids starting with conjunctions implying prior context ("But", "However")?

### Category 3: Structural Readability (20%)

Formatting that helps AI parse and segment content.

| Score | Criteria |
|-------|---------|
| 90-100 | Clean H1>H2>H3 hierarchy. Question headings. Short paragraphs (2-4 sentences). Tables for comparisons. Lists for processes. |
| 70-89 | Good hierarchy with minor skips. Some question headings. Mostly short paragraphs. |
| 50-69 | Inconsistent hierarchy. Few question headings. Mixed paragraph lengths. |
| 30-49 | Minimal structure. Long paragraphs dominate. |
| 0-29 | No heading structure. Wall-of-text. |

**Best practices:**
- Question headings ("What is X?" / "How does X work?") map directly to AI queries
- 2-4 sentences per paragraph — AI parses short paragraphs more reliably
- Tables for 3+ item comparisons — AI extracts table data with high accuracy
- Bold first use of key terms — aids AI entity recognition

### Category 4: Statistical Density (15%)

Specific, verifiable data points that AI prioritizes when selecting citation sources.

| Score | Criteria |
|-------|---------|
| 90-100 | 5+ statistics per 500 words. Named sources. Exact numbers. |
| 70-89 | 3-4 per 500 words. Most sourced. Mostly specific. |
| 50-69 | 1-2 per 500 words. Some sourced. |
| 30-49 | <1 per 500 words. Few sources. Vague quantifiers. |
| 0-29 | No statistics. All vague ("many", "most", "a lot"). |

**Counts as statistic:** "73% of marketers report...", "$4,500/month", "6-8 weeks", "According to 2025 HubSpot Report..."
**Does NOT count:** "Many companies...", "A significant percentage...", "Studies show..." (unnamed)

### Category 5: Uniqueness & Original Data (10%)

Information AI can't find elsewhere — making your content a necessary citation source.

| Score | Criteria |
|-------|---------|
| 90-100 | First-party research, proprietary data, original surveys. |
| 70-89 | Original insights or unique analysis of existing data. |
| 50-69 | Synthesizes existing info with some unique commentary. |
| 30-49 | Largely derivative. Restates common knowledge. |
| 0-29 | Entirely derivative. Available verbatim on higher-authority sources. |

**Signals:** "Our analysis found...", "We surveyed N professionals...", custom charts, case studies with named outcomes, original frameworks.

---

## Analysis Procedure

### Step 1: Fetch and Parse

1. WebFetch target URL
2. Extract main content (exclude nav, footer, sidebar, ads)
3. Preserve heading structure, paragraph boundaries, lists, tables
4. Calculate total word count

### Step 2: Segment into Blocks

Split at each H2/H3. For each block, record:
- Heading text, full content, word count
- Paragraph count, list/table count
- Statistics count, definition patterns present
- Whether first 60 words form standalone answer

### Step 3: Score Each Block

```
Block_Score = (AnswerQuality * 0.30) + (SelfContain * 0.25)
            + (Structure * 0.20) + (StatsDensity * 0.15) + (Uniqueness * 0.10)
```

### Step 4: Page-Level Score

- Average of all block scores
- Identify top 3 (strengths) and bottom 3 (rewrite priority)
- Calculate "citability coverage" = % of blocks scoring 70+

### Step 5: Rewrite Suggestions

For each block scoring below 60:
1. Identify primary weakness
2. Propose rewritten opening using answer-first / definition pattern
3. Suggest specific statistics or facts to add
4. Recommend structural improvements (add table, split paragraph, add list)

---

## Output Format

Generate `GEO-CITABILITY-SCORE.md`:

```markdown
# AI Citability Analysis: [Page Title]

**URL:** [URL]
**Date:** [Date]
**Overall Citability Score: XX/100**
**Citability Coverage:** XX% of blocks score 70+

## Score Summary
| Category | Score | Weight | Weighted |
|----------|-------|--------|----------|
| Answer Block Quality | XX/100 | 30% | XX |
| Self-Containment | XX/100 | 25% | XX |
| Structural Readability | XX/100 | 20% | XX |
| Statistical Density | XX/100 | 15% | XX |
| Uniqueness | XX/100 | 10% | XX |
| **Overall** | | | **XX/100** |

## Strongest Blocks
### 1. "[Heading]" — Score: XX/100
> [First 2 sentences]
**Why it works:** [Explanation]

## Weakest Blocks (Rewrite Priority)
### 1. "[Heading]" — Score: XX/100
**Current:** > [First 2 sentences]
**Problem:** [Specific issue]
**Suggested rewrite:** > [Rewritten opening]
**Improvements:** - [Add table] - [Include statistic about...]

## Quick Wins
1. [Recommendation] — Expected lift: +X points
```

---

## AI System Citation Preferences

| AI System | Preference |
|-----------|-----------|
| ChatGPT Search | Explicit definitions, named sources, recent dates. Cites 2-4 sources. |
| Perplexity | Fact-dense with statistics. Cites 4-8 sources. Values recency. |
| Gemini (AIO) | Concise answer blocks (40-60 words). Needs top-10 organic ranking. |
| Copilot | High-authority domains, clear factual claims. |

---

## Reference Data

- Optimal AI citation length: 134-167 words (Bortolato 2025)
- Definition patterns increase citation: 2.1x (Georgia Tech 2024)
- Adding statistics increases citation: 40% (Princeton 2024)
- Adding authority quotations: +115% in some categories (IIT Delhi 2024)
- Fluency optimization: +30% visibility average
- Source citations: +20-25% citation rate by Perplexity and ChatGPT
