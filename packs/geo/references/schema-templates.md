# Schema & Structured Data Templates

> JSON-LD templates for GEO, sameAs strategy, deprecated schemas. Used by geo-audit (Agent 5: Schema).

## Why Structured Data Matters for GEO

Structured data is the primary machine-readable signal that tells AI systems what an entity IS, what it does, and how it connects to other entities. While schema markup has traditionally been about earning Google rich results, its role in GEO is fundamentally different: **structured data is how AI models understand and trust your entity**. A complete entity graph in structured data dramatically increases citation probability across all AI search platforms.

---

## Detection and Validation

### Detection Methods

1. **JSON-LD**: Look for `<script type="application/ld+json">` blocks in HTML. Parse each as JSON. A page may have multiple blocks.
2. **Microdata**: Look for `itemscope`, `itemtype`, `itemprop` attributes. Harder for AI crawlers to parse — recommend migration to JSON-LD.
3. **RDFa**: Look for `typeof`, `property`, `vocab` attributes. Same recommendation — migrate to JSON-LD.

**Priority Order**: JSON-LD is the **strongly recommended format** for GEO. Google, Bing, and all AI platforms process JSON-LD most reliably.

### Validation Checklist (per schema block)

1. **Valid JSON**: Syntactically valid? No trailing commas, unquoted keys, malformed strings.
2. **Valid @type**: Matches a recognized Schema.org type?
3. **Required Properties**: Includes all required properties for its type?
4. **Recommended Properties**: Includes recommended GEO-enhancing properties?
5. **sameAs Links**: Includes `sameAs` properties linking to other platform presences?
6. **URL Validity**: All URLs resolve (not 404)?
7. **Nesting**: Properly nested (author inside Article, address inside Organization)?
8. **Rendering Method**: In server-rendered HTML or injected via JavaScript? Per Google December 2025 guidance, **JavaScript-injected structured data may face delayed processing**.

---

## Schema Types and Templates

### Organization (CRITICAL — every business site)

Essential for entity recognition across all AI platforms.

**Required properties:**
- `@type`: "Organization" (or subtype: Corporation, LocalBusiness, etc.)
- `name`: Official business name
- `url`: Official website URL
- `logo`: URL to logo image (ImageObject preferred)

**Recommended properties for GEO:**
- `sameAs`: Array of ALL platform URLs
- `description`: 1-2 sentence description
- `foundingDate`: ISO 8601 date
- `founder`: Person schema
- `address`: PostalAddress schema
- `contactPoint`: ContactPoint with telephone, email, contactType
- `areaServed`: Geographic area
- `numberOfEmployees`: QuantitativeValue
- `industry`: Text or DefinedTerm
- `award`: Array of awards received
- `knowsAbout`: Array of topics the organization is expert in (strong GEO signal)

**Template:**
```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "@id": "https://example.com/#organization",
  "name": "Company Name",
  "url": "https://example.com",
  "logo": {
    "@type": "ImageObject",
    "url": "https://example.com/logo.png",
    "width": 600,
    "height": 60
  },
  "description": "Concise description of what the company does.",
  "foundingDate": "2020-01-15",
  "founder": {
    "@type": "Person",
    "name": "Founder Name",
    "sameAs": "https://www.linkedin.com/in/founder"
  },
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "123 Main St",
    "addressLocality": "City",
    "addressRegion": "State",
    "postalCode": "12345",
    "addressCountry": "US"
  },
  "contactPoint": {
    "@type": "ContactPoint",
    "telephone": "+1-555-555-5555",
    "contactType": "customer service",
    "email": "support@example.com"
  },
  "sameAs": [
    "https://en.wikipedia.org/wiki/Company_Name",
    "https://www.wikidata.org/wiki/Q12345",
    "https://www.linkedin.com/company/company-name",
    "https://www.youtube.com/@companyname",
    "https://twitter.com/companyname",
    "https://github.com/companyname",
    "https://www.crunchbase.com/organization/company-name"
  ],
  "knowsAbout": [
    "Topic 1",
    "Topic 2",
    "Topic 3"
  ]
}
```

### Article + Author (CRITICAL for publishers)

The Author schema is one of the strongest E-E-A-T signals for AI platforms.

**Article required:**
- `@type`: "Article" (or NewsArticle, BlogPosting, TechArticle)
- `headline`: Article title
- `datePublished`: ISO 8601
- `dateModified`: ISO 8601 (critical for freshness signals)
- `author`: Person or Organization schema
- `publisher`: Organization schema with logo
- `image`: Representative image

**Author (Person) required for GEO:**
- `name`: Full name
- `url`: Author page URL on the site
- `sameAs`: LinkedIn, Twitter, personal site, Google Scholar, ORCID
- `jobTitle`: Professional title
- `worksFor`: Organization schema
- `knowsAbout`: Array of expertise areas
- `alumniOf`: Educational institutions
- `award`: Professional awards

**Template:**
```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "@id": "https://example.com/blog/post-slug#article",
  "headline": "Article Title Here",
  "datePublished": "2026-01-15T08:00:00Z",
  "dateModified": "2026-02-20T10:30:00Z",
  "image": "https://example.com/images/post-hero.jpg",
  "author": {
    "@type": "Person",
    "@id": "https://example.com/about/author-name#person",
    "name": "Author Name",
    "url": "https://example.com/about/author-name",
    "jobTitle": "Senior Engineer",
    "worksFor": {"@id": "https://example.com/#organization"},
    "knowsAbout": ["Topic 1", "Topic 2"],
    "alumniOf": {"@type": "EducationalOrganization", "name": "University Name"},
    "sameAs": [
      "https://www.linkedin.com/in/author-name",
      "https://twitter.com/authorname",
      "https://scholar.google.com/citations?user=XXXX"
    ]
  },
  "publisher": {"@id": "https://example.com/#organization"},
  "speakable": {
    "@type": "SpeakableSpecification",
    "cssSelector": [".article-summary", ".key-takeaway"]
  }
}
```

### Product (for e-commerce)

**Required:**
- `name`, `description`, `image`
- `offers`: Offer with price, priceCurrency, availability
- `brand`: Brand schema
- `sku` or `gtin`/`mpn`

**Recommended for GEO:**
- `aggregateRating`: AggregateRating
- `review`: Array of individual reviews
- `category`: Product category
- `material`, `weight`, `width`, `height` (where applicable)

**Template:**
```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Product Name",
  "description": "Clear product description with key features.",
  "image": "https://example.com/images/product.jpg",
  "brand": {"@type": "Brand", "name": "Brand Name"},
  "sku": "SKU-12345",
  "offers": {
    "@type": "Offer",
    "price": "99.99",
    "priceCurrency": "USD",
    "availability": "https://schema.org/InStock",
    "url": "https://example.com/products/product-name"
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.5",
    "reviewCount": "127"
  }
}
```

### LocalBusiness (physical locations)

Extends Organization. Critical for local AI search results and Google Gemini.

**Additional required:**
- `address`: Full PostalAddress
- `telephone`: Phone number
- `openingHoursSpecification`: Operating hours

**Recommended for GEO:**
- `geo`: GeoCoordinates (latitude, longitude)
- `priceRange`: Price indicator
- `aggregateRating`: AggregateRating
- `review`: Array of Review schemas
- `hasMap`: URL to Google Maps

**Template:**
```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "@id": "https://example.com/#localbusiness",
  "name": "Business Name",
  "url": "https://example.com",
  "telephone": "+1-555-555-5555",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "123 Main St",
    "addressLocality": "City",
    "addressRegion": "State",
    "postalCode": "12345",
    "addressCountry": "US"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": "40.7128",
    "longitude": "-74.0060"
  },
  "openingHoursSpecification": [
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"],
      "opens": "09:00",
      "closes": "17:00"
    }
  ],
  "priceRange": "$$",
  "sameAs": ["https://www.linkedin.com/company/...", "https://www.youtube.com/@..."]
}
```

### SoftwareApplication (for SaaS)

**Required:**
- `name`, `description`
- `applicationCategory`: e.g., "BusinessApplication"
- `operatingSystem`: Supported platforms
- `offers`: Pricing

**Recommended for GEO:**
- `aggregateRating`: User ratings
- `featureList`: Array of features (strong citation signal)
- `screenshot`: Screenshots
- `softwareVersion`: Current version
- `releaseNotes`: Link to changelog

**Template:**
```json
{
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "App Name",
  "description": "What the software does.",
  "applicationCategory": "BusinessApplication",
  "operatingSystem": "Web, iOS, Android",
  "offers": {
    "@type": "Offer",
    "price": "29",
    "priceCurrency": "USD",
    "priceValidUntil": "2026-12-31"
  },
  "featureList": ["Feature 1", "Feature 2", "Feature 3"],
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.7",
    "reviewCount": "542"
  },
  "softwareVersion": "3.2.1"
}
```

### WebSite + SearchAction (sitelinks search box)

```json
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "name": "Site Name",
  "url": "https://example.com",
  "potentialAction": {
    "@type": "SearchAction",
    "target": {
      "@type": "EntryPoint",
      "urlTemplate": "https://example.com/search?q={search_term_string}"
    },
    "query-input": "required name=search_term_string"
  }
}
```

### Person (standalone — personal brands, authors, thought leaders)

Use on About/Bio pages. Builds entity graph for individual expertise.

**Required:** `name`, `url`
**Recommended for GEO:** `sameAs`, `jobTitle`, `worksFor`, `knowsAbout`, `alumniOf`, `award`, `description`, `image`

### speakable Property (voice/AI assistants)

Marks specific sections as suitable for voice and AI assistant consumption. Add to Article or WebPage schemas.

```json
{
  "@type": "Article",
  "speakable": {
    "@type": "SpeakableSpecification",
    "cssSelector": [".article-summary", ".key-takeaway"]
  }
}
```

Signals to AI assistants which passages are the best candidates for citation or reading aloud.

### FAQPage

**Status (2024+)**: Google restricts FAQ rich results to government and health sites. However, FAQPage schema still serves GEO purposes — AI platforms parse FAQ structured data for question-answer extraction.

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What is X?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "X is [clear definition with specific facts]."
      }
    }
  ]
}
```

---

## sameAs Strategy (CRITICAL for Entity Recognition)

The `sameAs` property is the single most important structured data property for GEO. It tells AI systems: "This entity on my website is the SAME entity as these profiles elsewhere."

### Recommended sameAs Links (priority order)

1. **Wikipedia article** — highest authority entity link
2. **Wikidata item** — machine-readable entity identifier (e.g., `https://www.wikidata.org/wiki/Q12345`)
3. **LinkedIn** — company page or personal profile
4. **YouTube** — channel URL
5. **Twitter/X** — profile URL
6. **Facebook** — page URL
7. **Crunchbase** — company profile (for startups/tech)
8. **GitHub** — organization or personal profile (for tech)
9. **Google Scholar** — author profile (for researchers/academics)
10. **ORCID** — researcher identifier (for academics)
11. **Instagram** — profile URL
12. **Apple App Store / Google Play** — app listings (for software)
13. **BBB** — Better Business Bureau listing (for US businesses)
14. **Industry directories** — relevant vertical directories

### sameAs Audit Process

1. Collect all known web presences for the entity
2. Check that each URL resolves (not 404 or redirected)
3. Verify the Organization/Person schema includes ALL of them
4. Check that information on each platform is consistent (name, description, founding date, etc.)
5. Flag any platforms where the entity should have a presence but does not

---

## Deprecated/Changed Schemas

| Schema | Status | Note |
|--------|--------|------|
| HowTo | Rich results deprecated Aug 2023 | Still useful for AI parsing, but do not promise rich results |
| FAQPage | Restricted to govt/health Aug 2023 | Still useful for AI parsing (see above) |
| SpecialAnnouncement | Deprecated 2023 | Was for COVID; remove if still present |
| CourseInfo | Replaced by Course updates 2024 | Use updated Course schema properties |
| VideoObject `contentUrl` | Changed behavior 2024 | Must point to actual video file, not page URL |
| Review snippet | Stricter enforcement 2024 | Self-serving reviews on product pages may not display |

Flag any deprecated schemas found and recommend replacements.

---

## Business-Type Schema Map

| Type | Required Schemas |
|------|-----------------|
| All | Organization + WebSite + SearchAction |
| SaaS | + SoftwareApplication with featureList |
| Local | + LocalBusiness with geo, hours, reviews |
| E-commerce | + Product with offers, shipping, returns |
| Publisher | + Article + Author (Person) with speakable |

---

## JSON-LD Generation Rules

- Use the `@graph` pattern to include multiple schemas in one JSON-LD block
- All URLs must be absolute (not relative)
- Include `@id` properties for cross-referencing between schemas
- Use ISO 8601 for all dates
- Include `speakable` on Article schemas with CSS selectors pointing to key content sections
- Place JSON-LD in `<head>` section — NOT injected via JavaScript

---

## Scoring Rubric (0-100)

| Criterion | Points | How to Score |
|-----------|--------|-------------|
| Organization/Person schema present and complete | 15 | 15 if full, 10 if basic, 0 if none |
| sameAs links (5+ platforms) | 15 | 3 per valid sameAs link, max 15 |
| Article schema with author details | 10 | 10 if full author schema, 5 if name only, 0 if none |
| Business-type-specific schema present | 10 | 10 if complete, 5 if partial, 0 if missing |
| WebSite + SearchAction | 5 | 5 if present, 0 if not |
| BreadcrumbList on inner pages | 5 | 5 if present, 0 if not |
| JSON-LD format (not Microdata/RDFa) | 5 | 5 if JSON-LD, 3 if mixed, 0 if only Microdata/RDFa |
| Server-rendered (not JS-injected) | 10 | 10 if in HTML source, 5 if JS but in head, 0 if dynamic JS |
| speakable property on articles | 5 | 5 if present, 0 if not |
| Valid JSON + valid Schema.org types | 10 | 10 if no errors, 5 if minor issues, 0 if major errors |
| knowsAbout property on Organization/Person | 5 | 5 if present with 3+ topics, 0 if missing |
| No deprecated schemas present | 5 | 5 if clean, 0 if deprecated schemas found |
