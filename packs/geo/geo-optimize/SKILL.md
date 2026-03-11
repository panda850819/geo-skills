---
name: geo-optimize
description: >
  GEO writing optimization for content creators. Use when writing or editing content
  to maximize AI citability. Triggers on "GEO optimize", "optimize for AI search",
  "make content citable", "AI-optimize this article", "check GEO before publishing".
  Provides GEO checklist, passage rewrites, schema suggestions, and platform-specific
  tips. Chains with content-creator skill.
model: sonnet
allowed-tools:
  - Read
  - Grep
  - Glob
  - Bash
  - WebFetch
  - Write
---

# GEO Content Optimizer

> Make content AI-citable during writing, not after. Prevention over remediation.

## When to Use

- Writing a blog post, article, or landing page
- Editing existing content for AI visibility
- Reviewing drafts before publication
- Chaining from `content-creator` skill

## Usage

```
/geo-optimize <file>              # Optimize a local markdown/HTML file
/geo-optimize <url>               # Optimize published content
/geo-optimize --checklist         # Show GEO writing checklist only
```

---

## References

Read these before optimizing:

| Reference | When to Read |
|-----------|-------------|
| `../references/geo-methodology.md` | Core thesis, composite weights, crawler lists, severity levels |
| `../references/citability-rubrics.md` | Before scoring blocks on the 5 dimensions |
| `../references/eeat-content.md` | When assessing E-E-A-T signals and content quality |
| `../references/schema-templates.md` | When generating schema recommendations |
| `../references/platform-rubrics.md` | When adding platform-specific tips |
| `../references/brand-authority.md` | When assessing brand presence across platforms |

For specific improvement actions with tools and effort estimates, see `../references/actions-content.md`, `actions-technical.md`, or `actions-growth.md`.

Resolve all paths relative to this SKILL.md's parent directory.

---

## GEO Writing Checklist

Apply to every piece of content:

### Structure (do first)

- [ ] **One clear H1** -- matches the primary query this page targets
- [ ] **H2s as questions** where possible -- "What is X?", "How does X work?"
- [ ] **H2>H3 hierarchy** -- never skip levels
- [ ] **2-4 sentences per paragraph** -- each paragraph = one extractable idea
- [ ] **Tables for comparisons** of 3+ items
- [ ] **Ordered lists** for processes, **unordered** for features

### Answer Blocks (critical for citability)

- [ ] **Answer-first pattern** -- each section opens with 1-2 sentence direct answer
- [ ] **Definition patterns** -- "X is [definition]" for key concepts
- [ ] **134-167 words per key block** -- the AI citation sweet spot
- [ ] **No buried answers** -- the answer is NEVER in paragraph 3 of a section
- [ ] **Self-contained passages** -- each block understandable without context

### Data Density

- [ ] **3+ statistics per 500 words** -- specific percentages, dollar amounts, counts
- [ ] **Named sources** -- "According to [Source]" not "Studies show"
- [ ] **Exact numbers** -- "73%" not "most", "$4,500" not "thousands"
- [ ] **Dated references** -- "2025 HubSpot Report" not "a recent study"
- [ ] **Original data when possible** -- "Our analysis of 500 sites found..."

### E-E-A-T Signals

- [ ] **Author byline** with credentials and link to author page
- [ ] **First-person experience** -- "I tested...", "We implemented..."
- [ ] **Publication date** and last-updated date visible
- [ ] **Methodology shown** -- how you reached conclusions
- [ ] **Sources cited** -- link or name specific sources for claims

### Technical

- [ ] **Content in raw HTML** -- not behind JavaScript rendering
- [ ] **Schema.org markup** -- Article + Author with sameAs links
- [ ] **speakable CSS selectors** on key passages
- [ ] **canonical URL** set correctly
- [ ] **Meta description** that summarizes the answer (150-160 chars)

---

## Optimization Procedure

### Step 1: Analyze Current Content

Read the file or fetch the URL. Score each content block on the 5 citability dimensions (see `../references/citability-rubrics.md`). Flag blocks scoring below 60.

### Step 2: Rewrite Weak Blocks

For each block below 60, apply these transformation patterns:

**Pattern: Answer-First Rewrite**
```
BEFORE (buried answer):
"There are many factors to consider when choosing a CDN.
Performance, cost, and coverage all play a role. In general,
most businesses find that..."

AFTER (answer-first):
"The three critical factors for choosing a CDN are performance
(measured by latency reduction), cost (typically $0.01-0.10/GB),
and geographic coverage. According to the 2025 CDN Report by
KeyCDN, businesses using CDNs with 200+ edge locations see
50-70% faster page loads compared to single-origin serving."
```

**Pattern: Self-Containment Fix**
```
BEFORE (context-dependent):
"It also offers several other features that make it stand out.
These include real-time analytics and automated optimization."

AFTER (self-contained):
"Cloudflare's CDN differentiates through real-time analytics
dashboards showing per-request latency metrics and automated
image optimization that reduces payload by 30-50% without
configuration. These features are included in all paid plans
starting at $20/month."
```

**Pattern: Statistics Injection**
```
BEFORE (vague):
"Many companies have seen significant improvements after
implementing this approach."

AFTER (specific):
"Companies implementing edge caching report a median 47%
reduction in Time to First Byte (TTFB), according to
Catchpoint's 2025 Web Performance Report. Among the 200
enterprises surveyed, 89% achieved sub-200ms TTFB within
30 days of deployment."
```

### Step 3: Platform-Specific Tips

Based on content type, add targeted recommendations. See `../references/platform-rubrics.md` for detailed criteria.

| Content Type | Primary Platform | Key Optimization |
|-------------|-----------------|-----------------|
| How-to / Tutorial | Google AIO | Question H2s + ordered lists + tables |
| Product comparison | Perplexity | Data-dense tables + Reddit-friendly framing |
| Industry analysis | ChatGPT | Comprehensive (2000+ words) + named sources |
| Local service | Gemini | LocalBusiness schema + Google Business Profile |
| Technical docs | Copilot | IndexNow + exact-match keywords + GitHub links |

### Step 4: Schema Recommendations

Based on content, suggest JSON-LD. See `../references/schema-templates.md` for ready-to-paste templates.

1. **Always**: Article + Author with `sameAs` and `knowsAbout`
2. **If how-to**: Keep HowTo schema (still useful for AI even without rich results)
3. **If FAQ section**: FAQPage schema (still parsed by AI platforms)
4. **Add `speakable`**: Point CSS selectors at the strongest answer blocks

### Step 5: Generate Optimized Version

Output the optimized content with inline comments marking changes:

```markdown
<!-- GEO: Rewritten for answer-first pattern. Score: 45->78 -->
Content delivery networks (CDNs) are distributed server systems...

<!-- GEO: Added statistics. Score: 30->65 -->
According to Cloudflare's 2025 State of the Internet report...
```

---

## Output Format

When optimizing a file, generate two outputs:

### 1. Inline: Summary Report

```markdown
## GEO Optimization Summary

**Before:** Average citability XX/100
**After:** Average citability XX/100 (+XX)
**Blocks improved:** X of Y

### Changes Made
1. [Section name]: [What changed] -- Score: XX->XX
2. ...

### Remaining Opportunities
- [What couldn't be auto-fixed and why]

### Schema to Add
[Ready-to-paste JSON-LD]
```

### 2. File: Optimized Content

Write the optimized version back to the file (or to `[filename]-geo-optimized.md` if user prefers non-destructive).

---

## Integration with content-creator

When chained from `content-creator`:

1. content-creator produces the draft
2. geo-optimize runs the checklist against the draft
3. Rewrites weak blocks inline
4. Adds schema recommendations
5. Returns the GEO-optimized version

Suggest this chain when content is being created:

> "Draft is ready. Run `/geo-optimize` to check AI citability before publishing?"
