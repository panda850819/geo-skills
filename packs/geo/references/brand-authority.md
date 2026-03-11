# Brand Authority Scoring

> Platform-specific brand presence scoring for AI visibility. YouTube/Reddit/Wikipedia/LinkedIn correlation data, rubrics, and composite formula. Used by geo-audit (Agent 1: AI Visibility).

## Core Insight

Brand mentions correlate approximately 3x more strongly with AI visibility than traditional backlinks. An Ahrefs study published in December 2025, analyzing 75,000 brands across AI search platforms, found that **unlinked brand mentions** — references to a brand name without a hyperlink — are a stronger predictor of whether AI systems cite and recommend a brand than Domain Rating or backlink count.

The critical finding: **the platform where the mention appears matters enormously.** Not all mentions are equal. A mention on YouTube or Reddit carries far more weight for AI citation than a mention on a low-authority blog, because AI training data and retrieval systems disproportionately index high-engagement platforms.

---

## Correlation Data (Ahrefs Dec 2025, 75K Brands)

| Signal | Correlation with AI Citation | Traditional SEO Value |
|--------|----------------------------|----------------------|
| YouTube mentions | ~0.737 | Low (not a ranking factor) |
| Reddit mentions | High (exact coefficient not published) | Low |
| Wikipedia presence | High | Moderate (trust signal) |
| LinkedIn presence | Moderate | Low |
| Domain Rating | ~0.266 | Very High |
| Backlink count | ~0.266 | Very High |
| Organic traffic | Moderate | Very High |

**Key insight:** The signals that matter most for AI visibility (YouTube, Reddit) are almost irrelevant in traditional SEO, and the signals that matter most for traditional SEO (backlinks, DR) are weak predictors of AI visibility.

---

## Composite Brand Authority Score

### Formula

| Platform | Weight | Rationale |
|----------|--------|-----------|
| YouTube Presence | 25% | Strongest correlation with AI citation (0.737) |
| Reddit Presence | 25% | Second strongest correlation; critical for product recommendations |
| Wikipedia / Wikidata | 20% | Entity recognition foundation; AI training data cornerstone |
| LinkedIn Authority | 15% | Professional authority signals; B2B relevance |
| Other Platforms | 15% | Supplementary signals from Quora, GitHub, news, forums, podcasts |

```
Brand_Authority_Score = (YouTube * 0.25) + (Reddit * 0.25) + (Wikipedia * 0.20) + (LinkedIn * 0.15) + (Other * 0.15)
```

### Score Interpretation

| Score Range | Rating | Interpretation |
|-------------|--------|---------------|
| 85-100 | Dominant | Brand is a well-recognized entity across AI platforms. Highly likely to be cited and recommended by AI systems. |
| 70-84 | Strong | Brand has solid cross-platform presence. AI systems likely recognize and cite it for relevant queries. |
| 50-69 | Moderate | Brand has presence on some platforms but gaps exist. AI citation is inconsistent. |
| 30-49 | Weak | Brand has limited platform presence. AI systems may not recognize it as a distinct entity. |
| 0-29 | Minimal | Brand has negligible platform presence. AI systems are unlikely to cite or recommend it. |

---

## YouTube Scoring (0-100)

### Why YouTube Matters Most

- AI training datasets heavily incorporate YouTube transcripts, descriptions, and metadata.
- Google's Gemini and AI Overviews directly reference YouTube content; Perplexity and ChatGPT also index and cite it.
- YouTube transcripts contain natural language mentions in conversational context, making them high-signal for AI citation.

### What to Check

- **Brand YouTube channel:** Active channel? Subscriber count? Video count? Upload frequency?
- **Third-party video mentions:** Other YouTubers mentioning the brand in reviews, tutorials, comparisons?
- **Video descriptions:** Brand name in video descriptions of industry-relevant content?
- **Video transcripts:** Brand mentioned in spoken content? (AI models index transcripts)
- **YouTube search presence:** Results when searching "[brand name]" on YouTube?
- **Comment mentions:** Brand mentioned in comments on relevant industry videos?

### Score Bands

| Score | Criteria |
|-------|---------|
| 90-100 | Active channel with 10K+ subscribers, regular uploads, brand mentioned in 20+ third-party videos, appears in YouTube search results for industry terms |
| 70-89 | Active channel with 1K+ subscribers, brand mentioned in 10-19 third-party videos, some YouTube search presence |
| 50-69 | Channel exists with some content, brand mentioned in 5-9 third-party videos, limited YouTube search presence |
| 30-49 | Channel exists but inactive, brand mentioned in 1-4 third-party videos |
| 10-29 | No channel or empty channel, brand mentioned in 1-2 videos only |
| 0-9 | No YouTube presence whatsoever |

---

## Reddit Scoring (0-100)

### Why Reddit Matters

- Google's $60M/year Reddit licensing deal (2024) confirms heavy AI training data inclusion.
- "Reddit" appended to ~10-15% of Google searches by users seeking authentic opinions.
- Perplexity cites Reddit threads frequently; ChatGPT and Claude reference Reddit for product/service questions.

### What to Check

- **Subreddit presence:** Brand discussed in relevant subreddits? Which ones?
- **Mention volume:** Thread count? Trend (increasing/decreasing)?
- **Sentiment:** Mostly positive, negative, or neutral? Common praise points and complaints?
- **Official presence:** Official Reddit account? Participating in discussions? AMAs?
- **Recommendation threads:** Brand appears in "What do you recommend for X?" threads?
- **Own subreddit:** Brand has its own subreddit? How active?

### Score Bands

| Score | Criteria |
|-------|---------|
| 90-100 | Frequently recommended in relevant subreddits, predominantly positive sentiment, active official presence, own subreddit with 5K+ members, appears in top recommendations for industry queries |
| 70-89 | Regularly mentioned in relevant subreddits, mostly positive sentiment, some official presence, appears in multiple recommendation threads |
| 50-69 | Mentioned in several relevant threads, mixed sentiment, brand name is recognized by community members |
| 30-49 | Occasional mentions, limited to 1-2 subreddits, no official presence |
| 10-29 | Rare mentions, brand largely unknown on Reddit |
| 0-9 | No Reddit presence |

---

## Wikipedia Scoring (0-100)

### Why Wikipedia Matters

- All major AI models trained on Wikipedia dumps; primary source for entity recognition.
- Wikidata provides machine-readable facts for AI knowledge graph construction.
- Having a Wikipedia page is a strong signal of notability to AI systems.

### What to Check

- **Wikipedia page:** Brand/company has own article? Marked for deletion or quality issues?
- **Founder page:** Founder/CEO has Wikipedia page? (Strong authority signal)
- **Wikipedia citations:** Brand's website cited as reference in Wikipedia articles?
- **Wikidata entry:** Brand has Wikidata item (Q-number)? How complete?
- **Wikipedia mentions:** Brand mentioned in other articles (industry, competitor, category pages)?
- **Article quality:** Stub, start-class, or higher?

### Wikipedia Detection Method

**Method 1 — Python API check (MOST RELIABLE, do this FIRST):**
```bash
python3 -c "
import requests, json
from urllib.parse import quote_plus
brand = '[Brand_Name]'
api_url = f'https://en.wikipedia.org/w/api.php?action=query&list=search&srsearch={quote_plus(brand)}&format=json'
r = requests.get(api_url, headers={'User-Agent': 'GEO-Audit/1.0'}, timeout=15)
data = r.json()
results = data.get('query', {}).get('search', [])
if results and brand.lower() in results[0].get('title', '').lower():
    print(f'WIKIPEDIA PAGE EXISTS: {results[0][\"title\"]}')
    print(f'URL: https://en.wikipedia.org/wiki/{results[0][\"title\"].replace(\" \", \"_\")}')
else:
    print('No direct Wikipedia page found')
wd_url = f'https://www.wikidata.org/w/api.php?action=wbsearchentities&search={quote_plus(brand)}&language=en&format=json'
r2 = requests.get(wd_url, headers={'User-Agent': 'GEO-Audit/1.0'}, timeout=15)
wd = r2.json()
entities = wd.get('search', [])
if entities:
    print(f'WIKIDATA ENTRY: {entities[0].get(\"id\", \"\")} — {entities[0].get(\"description\", \"\")}')
"
```

**Method 2 — Direct URL check (backup):**
WebFetch `https://en.wikipedia.org/wiki/[Brand_Name]` — check if page loads.

**Method 3 — Search (least reliable, supplemental only):**
Search `[brand name] site:wikipedia.org`

**CRITICAL:** Web search alone is NOT reliable for determining Wikipedia presence. ALWAYS run the Python API check first.

### Score Bands

| Score | Criteria |
|-------|---------|
| 90-100 | Detailed Wikipedia article (B-class or higher), Wikidata entry with complete properties, brand cited as reference in multiple articles, founder has Wikipedia page |
| 70-89 | Wikipedia article exists (start-class or higher), Wikidata entry exists, brand mentioned in 2+ other Wikipedia articles |
| 50-69 | Wikipedia article exists (stub or start), basic Wikidata entry, limited mentions in other articles |
| 30-49 | No Wikipedia article but brand is mentioned in other articles or cited as reference; Wikidata entry may exist |
| 10-29 | Brand mentioned in 1-2 Wikipedia articles as a passing reference only |
| 0-9 | No Wikipedia or Wikidata presence of any kind |

---

## LinkedIn Scoring (0-100)

### Why LinkedIn Matters

- LinkedIn content increasingly indexed by AI systems for professional/B2B context and company entity signals.
- AI models reference LinkedIn for company information, team credentials, and professional authority.

### What to Check

- **Company page:** LinkedIn company page? Follower count? Post frequency?
- **Employee thought leadership:** Leadership posting content mentioning the brand?
- **Company mentions:** Brand mentioned in LinkedIn posts by non-employees?
- **LinkedIn articles:** Long-form articles about the brand?
- **Employee profiles:** Employees list company with detailed descriptions?
- **Engagement metrics:** Typical engagement on company posts?

### Score Bands

| Score | Criteria |
|-------|---------|
| 90-100 | Active company page with 10K+ followers, leadership regularly posts thought leadership, brand frequently mentioned by industry professionals, strong employee profiles |
| 70-89 | Active company page with 5K+ followers, some employee thought leadership, occasional third-party mentions |
| 50-69 | Company page exists with 1K+ followers, irregular posting, limited third-party mentions |
| 30-49 | Company page exists but is sparse or inactive, few followers, no third-party mentions |
| 10-29 | Basic company page with minimal information |
| 0-9 | No LinkedIn company page |

---

## Other Platforms Scoring (0-100)

### Supplementary Platforms

#### Quora
- **Relevance:** Answers frequently included in AI training data, cited by Perplexity.
- **Check:** Brand mentioned in answers to industry-relevant questions? Official presence?
- **Signal strength:** Moderate for B2C, lower for B2B.

#### Stack Overflow / Stack Exchange
- **Relevance:** Critical for developer-facing brands (SaaS, dev tools, APIs).
- **Check:** Product discussed in SO questions/answers? Brand has a tag? Official account answering questions?
- **Signal strength:** High for technical products, irrelevant for most B2C.

#### GitHub
- **Relevance:** Critical for open-source and developer-focused brands.
- **Check:** GitHub organization? Stars on repositories? Mentions in other repos?
- **Signal strength:** High for dev tools and open-source, low for non-technical brands.

#### Industry Forums and Communities
- **Relevance:** Niche authority signals from domain-specific training data.
- **Check:** Brand discussed in Hacker News, ProductHunt, industry Slack communities?
- **Signal strength:** Moderate, valuable for niche authority.

#### News and Press
- **Relevance:** Entity authority and recency signals.
- **Check:** Coverage by major news outlets? How recently? Context?
- **Signal strength:** Moderate. Recency matters — last 6 months is far more valuable than 3 years ago.

#### Podcasts
- **Relevance:** Growing AI training data source. Transcripts increasingly indexed.
- **Check:** Brand or leadership appeared on podcasts? Transcripts indexed?
- **Signal strength:** Moderate and growing.

---

## Sentiment Assessment

For Reddit and other discussion platforms, assess sentiment from most recent and prominent mentions:

| Sentiment | Indicators |
|-----------|-----------|
| **Positive** | Recommendations ("I love [brand]," "Highly recommend"), upvoted mentions, positive comparisons |
| **Neutral** | Factual mentions ("We use [brand] for..."), questions about the brand, balanced comparisons |
| **Negative** | Complaints ("Avoid [brand]", "terrible support"), downvoted recommendations, negative comparisons |
| **Mixed** | Combination of positive and negative. Note the ratio and primary themes. |

For building guides: see `actions-growth.md`.
