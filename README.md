# SEO Research — Claude Code Plugin

Automated competitor SEO research pipeline for Claude Code. Fetches keywords, clusters by intent, analyzes competitor content strategies, and produces actionable implementation plans.

## Installation

```bash
claude plugin install github:YOUR_USERNAME/seo-research
```

## What It Does

1. **Competitor Discovery** — finds all competitors in your niche via web search
2. **Keyword Fetching** — pulls ranked keywords from DataForSEO API
3. **Clustering** — groups keywords by search intent using embeddings + K-means
4. **Strategy Analysis** — categorizes competitor pages into SEO strategy types (comparison pages, integration pages, vertical landing, etc.)
5. **Implementation Plans** — generates detailed content plans based on competitor analysis

## Usage

Invoke the skill:

```
/seo-research
```

The skill guides you through an interactive pipeline:
- Competitor discovery or manual input
- Config setup (domains, filters, location)
- Data collection → preprocessing → embedding → clustering
- Iterative cluster review and cleanup
- Per-competitor strategy analysis (via agents)
- Final SEO master plan generation

## Agents

The plugin includes 4 specialized agents that run as part of the pipeline:

| Agent | Purpose |
|-------|---------|
| `competitor-discovery-agent` | Find all competitors in a niche from seed domains |
| `seo-strategy-reserach-agent` | Analyze one competitor domain, output strategy JSONs |
| `seo-strategy-planner` | Create implementation plan for one strategy type |
| `seo-homepage-analyst` | Deep analysis of competitor homepage positioning |

## API Keys Required

The plugin uses external APIs. You'll be prompted to configure these on first run.

| Service | Keys | Purpose |
|---------|------|---------|
| [DataForSEO](https://dataforseo.com) | `DATAFORSEO_LOGIN`, `DATAFORSEO_PASSWORD` | Keyword rankings data |
| [OpenRouter](https://openrouter.ai) | `OPENROUTER_API_KEY` | Text embeddings for clustering |

Keys are stored in `.env.local` in your project directory (git-ignored).

## Output Structure

```
your-project/seo-research/
├── config.json              # Project settings
├── competitors/
│   └── domain.com/
│       ├── homepage.json    # Homepage analysis
│       ├── comparison-pages.json
│       └── ...              # Strategy JSONs
└── strategies/
    ├── 0_SEO_Master_Plan.md # Executive summary
    ├── homepage.md          # Homepage optimization plan
    ├── comparison-pages.md  # Strategy implementation plans
    └── ...
```

## Requirements

- [uv](https://docs.astral.sh/uv/) — installed automatically if missing
- Python 3.10+ (managed by uv)
- Claude Code CLI

## License

MIT
