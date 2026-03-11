# Citability Scoring Rubrics

> 5-dimension scoring rubrics for AI citability. Used by geo-citability and geo-audit skills.

## Scoring Formula

```
Block_Score = (AnswerQuality * 0.30) + (SelfContain * 0.25)
            + (Structure * 0.20) + (StatsDensity * 0.15) + (Uniqueness * 0.10)
```

Page-level score = average of all block scores.

---

## Dimension 1: Answer Block Quality (30%)

Does content contain clear, quotable answer passages that AI systems can extract verbatim?

### Score Bands

| Score | Criteria |
|-------|---------|
| **90-100** | Every major section opens with a 1-2 sentence direct answer. Uses "X is..." or "X refers to..." patterns. First 40-60 words of each section can stand alone as a complete answer. |
| **70-89** | Most sections have clear answer openings. Some definition patterns present. Answers are identifiable but may need minor context. |
| **50-69** | Some sections have answer-like openings but many bury the answer in the middle or end of paragraphs. Few explicit definition patterns. |
| **30-49** | Answers are generally buried in long paragraphs. No consistent definition patterns. Content is narrative-driven rather than answer-driven. |
| **0-29** | No identifiable answer blocks. Content is entirely narrative, conversational, or fragmented. AI would struggle to extract any quotable passage. |

### Detection Patterns

- **Definition patterns:** "X is [definition]." / "X refers to [explanation]." / "X means [meaning]."
- **Answer-first structure:** The answer appears in the first sentence, followed by supporting detail.
- **Quantified answers:** "The average cost of X is $Y" rather than "Many factors affect the cost of X."
- **Comparison answers:** "X differs from Y in three ways: [list]" rather than "X and Y are often confused."
- **Attribution answers:** "According to [Source], [specific claim with data]."

### Examples

**High-citability (Score: 85+):**
```
Content delivery networks (CDNs) are distributed server systems that cache and serve
web content from locations geographically close to end users. A CDN reduces latency
by 50-70% on average by serving assets from edge servers rather than a single origin
server. The three largest CDN providers as of 2025 are Cloudflare (serving approximately
20% of all websites), Amazon CloudFront, and Akamai Technologies.
```
Analysis: 58 words. Self-contained: Yes. Facts: 3 specific data points. Definition pattern: Yes.

**Low-citability (Score: 15-):**
```
If you've ever wondered why some websites load faster than others, the answer might
surprise you. There's this amazing technology that has been around for a while now.
It's changed the way we think about web performance. Let me explain how it works and
why you should care about it for your business.
```
Analysis: 52 words. Self-contained: No (no topic identified). Facts: 0. Definition pattern: No.

---

## Dimension 2: Passage Self-Containment (25%)

Can individual passages be extracted and understood without needing the surrounding content?

### Score Bands

| Score | Criteria |
|-------|---------|
| **90-100** | 80%+ of content blocks are fully self-contained. Each passage names its subject explicitly. No reliance on pronouns referencing earlier content. Contains specific facts within the passage. |
| **70-89** | 60-79% of content blocks are self-contained. Most passages name their subject. Occasional pronoun references that require context. |
| **50-69** | 40-59% of content blocks are self-contained. Mixed use of explicit subjects and pronouns. Some passages require reading prior sections. |
| **30-49** | 20-39% of content blocks are self-contained. Heavy reliance on pronouns and contextual references. Most passages need surrounding text. |
| **0-29** | Under 20% self-contained. Content reads as a continuous narrative where extracting any paragraph loses meaning. |

### Self-Containment Checklist (per passage)

1. Does the passage explicitly name the subject (not "it," "this," "they")?
2. Can someone understand the main point reading ONLY this passage?
3. Does the passage contain at least one specific fact, statistic, or named entity?
4. Is the passage between 50-200 words (the optimal extraction length)?
5. Does the passage avoid starting with conjunctions ("But," "However," "And") that imply prior context?

---

## Dimension 3: Structural Readability (20%)

Structural formatting that helps AI systems parse and segment content.

### Score Bands

| Score | Criteria |
|-------|---------|
| **90-100** | Clean H1 > H2 > H3 hierarchy. Question-based headings for informational content. Short paragraphs (2-4 sentences). Tables for comparisons. Ordered lists for processes. Unordered lists for features/options. |
| **70-89** | Good heading hierarchy with minor skips. Some question-based headings. Mostly short paragraphs. Some use of tables and lists. |
| **50-69** | Heading hierarchy present but inconsistent. Few question-based headings. Mix of short and long paragraphs. Limited tables/lists. |
| **30-49** | Minimal heading structure. No question-based headings. Long paragraphs dominate. Rare use of tables/lists. |
| **0-29** | No heading structure or severely broken hierarchy. Wall-of-text paragraphs. No tables or lists. |

### Best Practices

- **Heading hierarchy:** H1 (page title) > H2 (major sections) > H3 (subsections). Never skip levels.
- **Question-based headings:** "What is [topic]?" and "How does [topic] work?" are directly matchable to AI queries.
- **Paragraph length:** 2-4 sentences per paragraph. AI systems parse short paragraphs more reliably.
- **Tables:** Use for any comparison of 3+ items. AI systems extract table data with high accuracy.
- **Lists:** Use ordered lists for sequential processes, unordered lists for non-sequential items.
- **Bold key terms:** Bold the first use of important terms. This aids AI entity recognition.

---

## Dimension 4: Statistical Density (15%)

Presence of specific, verifiable data points that AI systems prioritize when selecting citation sources.

### Score Bands

| Score | Criteria |
|-------|---------|
| **90-100** | 5+ specific statistics per 500 words. All claims backed by named sources or dates. Uses exact numbers (not "many" or "several"). Includes percentages, dollar amounts, timeframes, and named studies. |
| **70-89** | 3-4 statistics per 500 words. Most claims have sources. Mostly specific numbers with occasional vague quantifiers. |
| **50-69** | 1-2 statistics per 500 words. Some claims sourced. Mix of specific and vague numbers. |
| **30-49** | Less than 1 statistic per 500 words. Few sourced claims. Predominantly vague quantifiers. |
| **0-29** | No statistics. No sourced claims. All quantifiers are vague ("many," "most," "a lot"). |

### What Counts as a Statistic

- Specific percentages: "73% of marketers report..."
- Dollar amounts: "The average cost is $4,500 per month"
- Timeframes: "Implementation takes 6-8 weeks on average"
- Named studies: "According to the 2025 HubSpot State of Marketing Report..."
- Specific counts: "The platform integrates with 340+ tools"
- Comparison data: "40% faster than the industry average"

### What Does NOT Count

- "Many companies use..." (vague)
- "A significant percentage..." (vague)
- "Studies show that..." (no named source)
- "Experts agree..." (no named experts)
- "Recently..." (no specific timeframe)

---

## Dimension 5: Uniqueness & Original Data (10%)

Whether the content provides information that AI systems cannot find elsewhere, making it a necessary citation source.

### Score Bands

| Score | Criteria |
|-------|---------|
| **90-100** | Contains first-party research, proprietary data, original surveys, or unique datasets. Presents analysis or insights not found on any other page. Clear methodological descriptions. |
| **70-89** | Contains some original insights or unique analysis of existing data. Offers a distinct perspective with original examples. |
| **50-69** | Mostly synthesizes existing information but adds some unique commentary or examples. |
| **30-49** | Largely derivative content that restates common knowledge with minimal original contribution. |
| **0-29** | Entirely derivative. All information is available (often verbatim) on higher-authority sources. |

### Signals of Unique Content

- "Our analysis of [X] data found..."
- "We surveyed [N] [professionals] and found..."
- "Based on our experience with [N] clients..."
- Custom charts, graphs, or data visualizations
- Case studies with specific named outcomes
- Original frameworks, methodologies, or taxonomies

---

## AI System Citation Preferences

| AI System | Citation Preference |
|-----------|-------------------|
| **ChatGPT (Search)** | Prefers passages with explicit definitions, named sources, and recent dates. Tends to cite 2-4 sources per response. |
| **Perplexity** | Heavily favors fact-dense passages with statistics. Cites 4-8 sources per response. Values recency highly. |
| **Claude** | Prefers well-structured, comprehensive passages. Values nuance and accuracy over brevity. |
| **Gemini (AI Overviews)** | Prefers concise answer blocks (40-60 words). Values content already ranking in top 10 organic results. |
| **Copilot (Bing)** | Similar to Gemini. Prefers passages from high-authority domains with clear factual claims. |

---

## Key Research Data

- **Optimal length for AI citation:** 134-167 words (Bortolato 2025 analysis of AI Overview passages)
- **Definition patterns increase citation rate by:** 2.1x (Georgia Tech 2024)
- **Adding statistics to passages increases citation by:** 40% (Princeton GEO study 2024)
- **Adding quotations from authorities increases citation by:** 115% in certain categories (IIT Delhi 2024)
- **Fluency optimization increases visibility by:** 30% on average across all query types
- **Content with source citations is cited:** 20-25% more often by Perplexity and ChatGPT
