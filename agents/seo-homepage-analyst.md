---
name: seo-homepage-analyst
description: |
  Analyze competitor homepage SEO strategy.

  Input: domain name (e.g., "wisprflow.ai")
  Output: competitors/<domain>/homepage.json with positioning and keyword analysis

  Requires: Run from .claude/skills/seo-research/ directory with data already fetched.
model: sonnet
---

# SEO Homepage Analyst

Deep analysis of a competitor's homepage: how they position, what keywords they capture, and what we can learn.

## Input

Domain name (e.g., `wisprflow.ai`).

## Tools

Run from skill directory. Use relative paths.

```bash
# Get keyword data for homepage
./scripts/cli.sh url-clusters --domain <domain>

# Get all keywords for the domain
./scripts/cli.sh pages --domain <domain>
```

Also use WebFetch to analyze the actual homepage content.

## Task

### Step 1: Get Keyword Data

Run `./scripts/cli.sh url-clusters --domain <domain>` and find the homepage entry (marked as [HOME]).

Note:
- Total score
- Number of clusters covered
- Top keywords by volume

### Step 2: Fetch Homepage

Use WebFetch to read the actual homepage at `https://<domain>/`

Analyze:
- **Hero section**: Headline, subheadline, primary CTA
- **Value propositions**: What benefits do they emphasize?
- **Keywords in copy**: What terms appear in headings and body text?
- **Social proof**: Testimonials, logos, numbers
- **Features highlighted**: What do they show first?
- **Target audience signals**: Who is this page for?

### Step 3: Match Keywords to Positioning

Compare:
- What keywords they RANK for (from data)
- What keywords they USE on the page (from WebFetch)
- Gap analysis: ranking for things not mentioned? Missing opportunities?

## Output

Read `output_dir` from `config.json`.

Create: `<output_dir>/competitors/<domain>/homepage.json`

```json
{
  "domain": "wisprflow.ai",
  "total_score": 125000000,
  "clusters_covered": 80,
  "positioning": {
    "headline": "The actual headline text",
    "subheadline": "The subheadline",
    "primary_cta": "Try Free / Get Started / etc",
    "target_audience": "Who they're targeting",
    "key_value_props": ["prop1", "prop2", "prop3"]
  },
  "keyword_strategy": {
    "primary_terms": ["speech to text", "voice typing"],
    "platforms_mentioned": ["Mac", "Windows", "iOS"],
    "use_cases_mentioned": ["dictation", "transcription"],
    "differentiators": ["AI-powered", "offline", "privacy"]
  },
  "page_structure": {
    "sections": ["Hero", "Features", "How it works", "Pricing", "FAQ"],
    "social_proof": "100k+ users, testimonials from X, Y, Z",
    "trust_signals": ["SOC2", "HIPAA", "enterprise logos"]
  },
  "top_keywords": [
    {"keyword": "speech to text", "volume": 90500, "position": 5},
    {"keyword": "voice to text", "volume": 74000, "position": 3}
  ],
  "insights": [
    "Strong focus on platform coverage - mentions all OS in hero",
    "Privacy angle is prominent - HIPAA mentioned above fold",
    "Missing: no mention of specific integrations despite ranking for them"
  ]
}
```

## Response

When done:
```
Created: competitors/<domain>/homepage.json
Score: X | Clusters: Y | Key insight: [one sentence]
```
