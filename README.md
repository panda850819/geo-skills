# geo-skills

GEO (Generative Engine Optimization) skill pack for Claude Code via skm.

## Skills

| Skill | Use When | Key Output |
|-------|----------|-----------|
| `geo-audit` | Full website audit for AI search visibility | `GEO-AUDIT-REPORT.md` with composite score |
| `geo-citability` | Analyzing how citable a page's content is | `GEO-CITABILITY-SCORE.md` with rewrite suggestions |
| `geo-optimize` | Writing or editing content for AI citability | Optimized content + summary report |

## Architecture

Skills follow progressive disclosure. SKILL.md contains workflow and output format only. Detailed rubrics, templates, and scoring data are in shared reference files:

```
packs/geo/
├── geo-audit/SKILL.md
├── geo-citability/SKILL.md
├── geo-optimize/SKILL.md
└── references/
    ├── geo-methodology.md      # Index: core thesis, composite weights, crawler lists
    ├── citability-rubrics.md   # 5-dimension scoring rubrics with examples
    ├── platform-rubrics.md     # Google AIO, ChatGPT, Perplexity, Gemini, Copilot
    ├── brand-authority.md      # YouTube/Reddit/Wikipedia/LinkedIn scoring
    ├── schema-templates.md     # JSON-LD templates + sameAs strategy
    ├── technical-scoring.md    # 8-category technical SEO (100pts)
    ├── eeat-content.md         # E-E-A-T 4x25pts + content quality metrics
    ├── actions-content.md      # Citability + E-E-A-T improvement actions
    ├── actions-technical.md    # Crawler, schema, SSR, CWV fix guides
    └── actions-growth.md       # Brand authority, platform onboarding, monitoring
```

All skills reference `../references/` relative to their SKILL.md location.

## Install

```bash
# Add registry (one-time)
skm registry add geo https://github.com/panda850819/geo-skills

# Install all 3 skills
skm install geo:geo-audit
skm install geo:geo-citability
skm install geo:geo-optimize

# Or install only what you need — references/ are shared and always available
skm install geo:geo-citability   # just citability analysis
```

Installing any single skill clones the full repo to skm cache, so `../references/` resolves correctly regardless of which skills you install.

## Sources

Methodology synthesized from:
- GEO research: Princeton, Georgia Tech, IIT Delhi (2024)
- Ahrefs Dec 2025 study (75K brands, AI visibility correlations)
- Bortolato 2025 (AI Overview passage analysis)
- geo-seo-claude (MIT license) — architecture patterns and domain knowledge

## License

MIT
