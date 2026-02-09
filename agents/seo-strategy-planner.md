---
name: seo-strategy-planner
description: |
  Creates detailed implementation plan for a specific SEO strategy.

  Input:
    - strategy name (e.g., "comparison-pages")
    - paths to strategy JSON files from different competitors

  Output: strategies/<strategy-name>.md with implementation plan

  Requires: Run from .claude/skills/seo-research/ directory.
model: sonnet
---

# SEO Strategy Planner

Create a detailed implementation plan for a specific SEO strategy based on competitor analysis.

## Input

You will receive:
1. Strategy name (e.g., `comparison-pages`)
2. Paths to JSON files from competitors using this strategy

Example:
```
Strategy: comparison-pages
Files:
  - competitors/wisprflow.ai/comparison-pages.json
  - competitors/superwhisper.com/comparison-pages.json
```

## Task

### Step 1: Read Strategy Files

Read each JSON file. They contain:
```json
{
  "strategy": "comparison-pages",
  "description": "How this competitor executes the strategy",
  "urls": ["https://domain.com/comparison/x", "https://domain.com/comparison/y"]
}
```

### Step 2: Get Keyword Data (optional)

If you need keyword details for specific pages:
```bash
./scripts/cli.sh pages --domain <domain>
```

### Step 3: Research Competitor Pages

Use WebFetch to read the actual competitor pages mentioned in the strategy files.

Analyze:
- Page structure and layout
- Content sections
- Keywords targeted
- CTAs used
- What makes the page effective

### Step 4: Write Strategy Plan

Read `output_dir` from `config.json`.

Create: `<output_dir>/strategies/<strategy-name>.md`

## Strategy Plan Output Format

```markdown
---
strategy: comparison-pages
competitors: [wisprflow.ai, superwhisper.com]
pages_count: XXX (max 200)
---

# Strategy: {Strategy Name}

## What It Is
[1-2 sentences explaining this strategy type]

## Why It Works
[Why this strategy is effective for SEO and conversions]

## Competitor Analysis

### competitor-a.com
**Approach:** [How they execute this strategy]
**Pages:**
// comprehensive list of pages for this stratgegy
- https://wisprflow.ai/comparison/x - [what it targets]
- https://wisprflow.ai/comparison/y - [what it targets]

### competitor-b.com
**Approach:** [How they execute this strategy]
**Pages:**
- https://superwhisper.com/... - [what it targets]

**IMPORTANT:** Always use full URLs with https:// in all competitor examples and tables. Never use relative paths.

## Implementation Plan

### URL Structure
`/comparison/[competitor]-alternative`

### Page Template
- **H1:** [format]
- **Sections:**
  1. [section 1]
  2. [section 2]
  ...
- **CTA:** [what action to drive]

### Pages to Create

<!-- 
Make sure to include as many pages as possible. You have to analyze competitors on existing pages, patterns, and the content they already have. Maybe even search a bit.

Second, it will be a second batch, so the first batch is content that competitors already have. It shall be something like content ideas. So you have pages to create. I think it better shall be a list of articles with priority:

1. Known articles with known traffic
2. Articles that are not present but may fit well into the strategy

Since you're already researching the strategy and deep into the domain, you have a very good idea of extra ideas that can be implemented here. So make sure the report is like a holy grail for the SEO content manager to explore, improve, and work on. 
-->

#### Batch 1: Direct competotrs clones

- [ ] /comparison/x-alternative - comapre competitor X to your product
...
- [ ] /comparison/x-alternative - comapre competitor z to your product
  
#### Batch 2: Extra ideas not found in SERP
...

### Content Clusters
[Analise the data and create high level content clusters that arise naturally inside of this strategy]
```

## Response

[Answer to user or agent who requests the task with simple message]
```
Finished. Created: [path/to/strategies/<strategy-name>.md]
```
