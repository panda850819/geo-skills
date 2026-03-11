# GEO Actions: Growth

> Growth-focused improvement actions for GEO scores. Covers brand authority building, platform onboarding, and monitoring.

## Table of Contents

1. [Brand Authority Building](#1-brand-authority-building)
2. [Platform-Specific Onboarding](#2-platform-specific-onboarding)
3. [Monitoring and Iteration](#3-monitoring-and-iteration)

---

## 1. Brand Authority Building

Brand authority is 20% of the composite GEO score. Brand mentions correlate ~3x more with AI visibility than backlinks (Ahrefs Dec 2025, 75K brands).

**Timeline expectation:** Brand authority takes 3-12 months to build. These are not quick wins. Start now and compound over time.

### Action Summary

| Action | Effort | Impact | Timeline | Tools |
|--------|--------|--------|----------|-------|
| Create minimum viable YouTube channel | High | +15-25 pts brand | 3-6 months | YouTube Studio, Descript |
| Build authentic Reddit presence | Medium | +10-20 pts brand | 2-6 months | Reddit, Gummy Search |
| Create Wikidata entry | Medium | +10-15 pts brand | 1-4 weeks | wikidata.org |
| Optimize LinkedIn company page | Low | +5-10 pts brand | 1 week | LinkedIn |
| Pursue Wikipedia article | High | +15-20 pts brand | 6-12 months | Wikipedia consultant |

### YouTube: Minimum Viable Channel

YouTube mention correlation with AI citation: 0.737 — the strongest signal. Even a small channel helps.

**3-5 starter videos (pick based on your business):**

| Video Type | Purpose | Example Title |
|------------|---------|---------------|
| "What is [Your Category]" explainer | Capture definition queries | "What is Revenue Operations? Explained in 5 Minutes" |
| "How to [Core Task]" tutorial | Capture how-to queries | "How to Set Up a CI/CD Pipeline with GitHub Actions" |
| "[Product] vs [Competitor]" comparison | Capture comparison queries | "Notion vs Obsidian: Which Note App in 2026?" |
| "[Your Topic] for Beginners" guide | Capture beginner queries | "Kubernetes for Beginners: Your First Deployment" |
| Customer success story / case study | Build social proof | "How [Client] Reduced Costs 40% with [Product]" |

**Production checklist (keep it simple):**
- Screen recording + voiceover is fine (no need for studio production)
- Tools: Descript ($24/mo), Loom (free tier), OBS Studio (free)
- Include brand name in: title, description, spoken audio (transcripts matter)
- Add timestamps/chapters in the description
- Upload closed captions (auto-generated + manual correction)

**How to get mentioned by others:**
- Send product to relevant YouTubers for review (micro-influencers: 5K-50K subs)
- Guest on industry YouTube channels
- Create content that others reference (original data, frameworks, tools)

### Reddit: Authentic Participation Strategy

Reddit mentions are the second strongest AI citation signal. Perplexity cites Reddit in 46.7% of responses.

**Step 1: Identify your subreddits (use Gummy Search — gummysearch.com)**
- Search your industry keywords
- Find 3-5 subreddits where your audience asks questions
- Check subreddit rules before posting

**Step 2: Participation framework (DO NOT shill)**

| Week | Activity | Time |
|------|----------|------|
| 1-2 | Lurk. Read top posts. Understand culture. | 30 min/day |
| 3-4 | Comment helpfully on relevant questions. No brand mentions yet. | 30 min/day |
| 5-8 | Create value-first posts (guides, tips, data). Mention brand only if directly relevant. | 1 hr/week |
| 9+ | Participate in recommendation threads. Share expertise naturally. | 1 hr/week |

**AMA guide:**
- Post in a relevant subreddit (check rules — some require mod approval)
- Title format: "I'm [Name], [Role] at [Brand]. We [notable thing]. AMA!"
- Prepare answers to top 10 likely questions beforehand
- Answer for 2+ hours. Be genuine. Admit limitations.
- Cross-post announcement to your community channels

**Rules:**
- Never create fake accounts to promote your brand
- Never pay for upvotes or astroturf
- Reddit communities detect and permanently ban shills
- One genuine helpful comment outweighs 100 promotional ones

### Wikipedia: Notability and Wikidata

**Notability criteria (do you qualify for a Wikipedia article?):**
- Significant coverage in multiple reliable, independent sources
- Press coverage in major publications (NYT, TechCrunch, Forbes, WSJ, etc.)
- Academic citations or industry reports mentioning the brand
- Annual revenue typically >$10M or significant industry impact

**If you DO NOT meet notability criteria yet:**
1. Focus on getting press coverage first (PR campaigns, thought leadership)
2. Create a Wikidata entry (lower bar than Wikipedia — see below)
3. Get cited as a reference in existing Wikipedia articles

**Wikidata entry creation (step by step):**

1. Go to https://www.wikidata.org/wiki/Special:NewItem
2. Create account if needed
3. Fill in:
   - **Label**: Your brand name
   - **Description**: "software company" / "marketing agency" / etc.
   - **Aliases**: Alternative names, abbreviations
4. Add properties (click "add statement"):
   - `instance of` (P31): "business" (Q4830453) or more specific type
   - `official website` (P856): your URL
   - `inception` (P571): founding date
   - `headquarters location` (P159): city
   - `industry` (P452): your industry
   - `founded by` (P112): founder name(s)
   - `social media links`: LinkedIn (P4264), YouTube (P2397), Twitter (P2002), GitHub (P2037)
5. Save and note your Q-number (e.g., Q12345678)
6. Add this Q-number URL to your Organization schema `sameAs`

**When to hire a Wikipedia consultant:**
- Revenue >$10M and clear notability signals
- Budget $5,000-$15,000 for article creation + maintenance
- Reputable firms: Beutler Ink, Rhiannon Ruff, WikiExperts
- NEVER edit your own Wikipedia article (conflict of interest policy)

### LinkedIn: Company Page Optimization

**Complete these fields (takes 30-60 minutes):**

1. **Header image**: branded, professional (1128x191 px)
2. **Description**: 2-3 paragraphs with keywords (2,000 char max)
3. **Website URL**: verified
4. **Industry**: correct classification
5. **Company size**: accurate range
6. **Headquarters**: full address
7. **Founded**: year
8. **Specialties**: list all (up to 20)

**Employee thought leadership program:**
- Ask 3-5 leaders to post 1x/week about industry topics
- Content should mention brand naturally, not promotionally
- Engage with industry discussions and tag company page
- Publish LinkedIn Articles (long-form) monthly on core expertise topics

---

## 2. Platform-Specific Onboarding

Platform optimization is 10% of the composite GEO score. Each platform has different priorities. Here is a "getting started in 30 minutes" checklist for each.

### Google AIO: 30-Minute Onboarding

| Step | Action | Time |
|------|--------|------|
| 1 | Verify site in Google Search Console (search.google.com/search-console) | 5 min |
| 2 | Submit XML sitemap in GSC | 2 min |
| 3 | Check "Pages" report for indexing issues | 5 min |
| 4 | Pick your top 3 pages. Add question-based H2 headings that match "People Also Ask" | 10 min |
| 5 | For each question heading, write a direct 1-2 sentence answer as the first paragraph | 8 min |

**Ongoing:** Convert one comparison to a table per week. Add one FAQ section per week.

### ChatGPT: 30-Minute Onboarding

| Step | Action | Time |
|------|--------|------|
| 1 | Register at Bing Webmaster Tools (bing.com/webmasters) | 5 min |
| 2 | Submit XML sitemap to Bing | 2 min |
| 3 | Search your brand on Wikidata (wikidata.org). Create entry if missing. | 10 min |
| 4 | Verify robots.txt allows GPTBot and OAI-SearchBot | 3 min |
| 5 | Check entity consistency: is brand name identical on website, LinkedIn, Wikidata? | 5 min |
| 6 | Search your brand in ChatGPT — note what it knows and what's wrong | 5 min |

**Ongoing:** Build toward Wikipedia notability. Maintain Reddit presence.

### Perplexity: 30-Minute Onboarding

| Step | Action | Time |
|------|--------|------|
| 1 | Verify robots.txt allows PerplexityBot | 2 min |
| 2 | Search your brand on Perplexity — note current citations | 5 min |
| 3 | Identify 3 subreddits where your audience is active (use Gummy Search) | 10 min |
| 4 | Create Reddit account if needed. Start lurking in those subreddits. | 3 min |
| 5 | Check publication dates on your top pages. Add visible dates if missing. | 5 min |
| 6 | Pick one page and add 3 sourced statistics | 5 min |

**Ongoing:** Post helpful content on Reddit weekly. Publish original data monthly.

### Gemini: 30-Minute Onboarding

| Step | Action | Time |
|------|--------|------|
| 1 | Claim Google Business Profile (business.google.com) if applicable | 5 min |
| 2 | Create or verify YouTube channel. Upload at least one video. | 10 min |
| 3 | Add Organization schema with sameAs (include YouTube, Wikipedia, LinkedIn) | 10 min |
| 4 | Search your brand on Google — check if Knowledge Panel appears. If yes, claim it. | 3 min |
| 5 | Verify robots.txt allows Google-Extended | 2 min |

**Ongoing:** Upload YouTube content monthly. Optimize GBP with photos and posts weekly.

### Copilot: 30-Minute Onboarding

| Step | Action | Time |
|------|--------|------|
| 1 | Register at Bing Webmaster Tools (if not done for ChatGPT step) | 5 min |
| 2 | Implement IndexNow (install plugin or create key file) | 10 min |
| 3 | Optimize meta descriptions on top 5 pages (Bing weights these heavily) | 10 min |
| 4 | Verify LinkedIn company page is complete | 3 min |
| 5 | Register at Bing Places (bingplaces.com) if local business | 2 min |

**Ongoing:** Keep IndexNow active. Post on LinkedIn weekly.

---

## 3. Monitoring and Iteration

### Re-Audit Frequency

| Site Activity Level | Re-Audit Frequency | Focus |
|--------------------|-------------------|-------|
| Publishing 4+ posts/week | Monthly | Citability, freshness, new page schema |
| Publishing 1-3 posts/week | Every 6 weeks | Full audit |
| Publishing < 1 post/week | Quarterly | Full audit |
| After major site changes | Immediately | Technical + schema |

### Track AI Traffic in GA4

AI platforms show up as referral sources. Set up a custom report:

1. Go to GA4 > Reports > Acquisition > Traffic Acquisition
2. Add secondary dimension: "Session source/medium"
3. Filter for AI sources:

| Source | What It Indicates |
|--------|------------------|
| `chatgpt.com / referral` | ChatGPT cited you with a link |
| `perplexity.ai / referral` | Perplexity cited you |
| `gemini.google.com / referral` | Gemini sent traffic |
| `copilot.microsoft.com / referral` | Copilot cited you |
| `bing.com / referral` (with AI indicators) | Bing Copilot inline citations |

**Set up a GA4 custom channel group:**
1. Admin > Data display > Channel groups > Create new
2. Add rule: Source matches regex `chatgpt|perplexity|gemini|copilot|claude`
3. Name it "AI Search"
4. Now you can track AI search as a distinct channel

### Manual Citation Checks

Until automated tools mature, manually check AI citations monthly:

1. **ChatGPT:** Ask "What is [your brand]?" and "What are the best [your category] tools?" Note if and how you're cited.
2. **Perplexity:** Search your brand name and your top keywords. Check sources listed.
3. **Google AIO:** Search your target keywords on Google. Check if AI Overview appears and whether you're cited.
4. **Gemini:** Ask Gemini about your brand and category. Note responses.

**Track in a spreadsheet:**

| Date | Platform | Query | Cited? | Position | Notes |
|------|----------|-------|--------|----------|-------|
| 2026-03-11 | ChatGPT | "best CDN providers" | Yes | Source 2 | Cited pricing page |
| 2026-03-11 | Perplexity | "best CDN providers" | No | — | Reddit thread cited instead |

### Prioritization Framework

Fix issues in this order — severity determines sequence, not dimension:

| Priority | Severity | Examples | Expected Lift |
|----------|----------|----------|---------------|
| 1 | Critical | AI crawlers blocked, site 100% client-rendered, HTTPS missing | +20-40 pts composite |
| 2 | High | No schema, no author info, thin content, no sameAs links | +10-20 pts composite |
| 3 | Medium | No llms.txt, stale content, incomplete schema, missing CWV optimization | +5-10 pts composite |
| 4 | Low | Tier 3 crawler access, minor CWV improvements, secondary platform presence | +1-5 pts composite |

### Monthly Action Cycle

| Week | Focus |
|------|-------|
| Week 1 | Re-audit top 5 pages. Fix any new Critical/High issues. |
| Week 2 | Content updates — add statistics, refresh dates, improve citability. |
| Week 3 | Brand building — Reddit participation, YouTube upload, LinkedIn post. |
| Week 4 | Technical check — schema validation, CWV monitoring, crawler access verification. |

**Do this now:**
1. Set a monthly calendar reminder for GEO re-audit
2. Set up the GA4 custom channel group for AI traffic
3. Do one manual citation check across all 5 platforms
4. Create the tracking spreadsheet
