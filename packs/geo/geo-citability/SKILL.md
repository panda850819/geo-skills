---
name: geo-citability
description: >
  AI citability scoring for web content. Use when analyzing how likely AI systems will
  cite or quote passages from a page. Triggers on "citability", "citation readiness",
  "passage scoring", "content citability", "will AI cite this", "how citable is this".
  Scores on 5 dimensions with block-level rewrite suggestions. Works standalone or as
  part of geo-audit.
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

## Usage

```
/geo-citability <url>           # Score a page
/geo-citability <url> --block   # Score + show per-block breakdown
```

Also callable from `geo-audit` as part of the full audit flow.

---

## References

Read `../references/citability-rubrics.md` before scoring. It contains the complete 5-dimension rubrics with score bands, detection patterns, examples, and AI system citation preferences.

For rewrite suggestions with specific improvement actions, see `../references/actions-content.md`.

Resolve all paths relative to this SKILL.md's parent directory.

---

## Core Insight

AI models cite passages that are **extractable** -- self-contained, fact-rich, answer-first blocks that make sense without surrounding context. GEO-optimized content achieves 30-115% higher visibility in AI responses (Princeton/Georgia Tech/IIT Delhi 2024).

AI systems preferentially cite passages that are:
- **134-167 words** long (optimal extraction length)
- **Self-contained** (understandable without context)
- **Fact-rich** (specific statistics, dates, named entities)
- **Answer-first** (direct answer in first 1-2 sentences)

---

## Scoring Formula

```
Block_Score = (AnswerQuality * 0.30) + (SelfContain * 0.25)
            + (Structure * 0.20) + (StatsDensity * 0.15) + (Uniqueness * 0.10)
```

| Dimension | Weight | What It Measures |
|-----------|--------|-----------------|
| Answer Block Quality | 30% | Clear, quotable answer passages with definition patterns |
| Self-Containment | 25% | Passages understandable without surrounding context |
| Structural Readability | 20% | Heading hierarchy, paragraph length, tables/lists |
| Statistical Density | 15% | Specific data points with named sources |
| Uniqueness & Original Data | 10% | Information AI cannot find elsewhere |

See `../references/citability-rubrics.md` for per-dimension score bands (0-100), detection patterns, and examples.

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

Apply the 5-dimension rubrics from `../references/citability-rubrics.md` to each block. Calculate weighted block score.

### Step 4: Page-Level Score

- Average of all block scores
- Identify top 3 (strengths) and bottom 3 (rewrite priority)
- Calculate "citability coverage" = % of blocks scoring 70+

### Step 5: Rewrite Suggestions

For each block scoring below 60:
1. Identify primary weakness (buried answer, no facts, poor structure, context-dependent)
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
### 1. "[Heading]" -- Score: XX/100
> [First 2 sentences]
**Why it works:** [Explanation]

## Weakest Blocks (Rewrite Priority)
### 1. "[Heading]" -- Score: XX/100
**Current:** > [First 2 sentences]
**Problem:** [Specific issue]
**Suggested rewrite:** > [Rewritten opening]
**Improvements:** - [Add table] - [Include statistic about...]

## Quick Wins
1. [Recommendation] -- Expected lift: +X points

## Per-Section Scores
| Section Heading | Words | Answer | Self-Cont | Structure | Stats | Unique | Overall |
|-----------------|-------|--------|-----------|-----------|-------|--------|---------|
| [H2 heading] | [N] | [X] | [X] | [X] | [X] | [X] | [X] |
```

---

Key research data: see `../references/geo-methodology.md` Research Citations.
