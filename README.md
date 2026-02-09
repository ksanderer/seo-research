# SEO Research — Claude Code Plugin

Automated competitor SEO research pipeline for Claude Code. Fetches keywords, clusters by intent, analyzes competitor content strategies, and produces actionable implementation plans.

## Installation

Two steps — add the marketplace, then install the plugin:

```bash
# 1. Add marketplace
/plugin marketplace add ksanderer/seo-research

# 2. Install plugin
/plugin install seo-tools@ksanderer-seo-research
```

Restart Claude Code after installation.

## Usage

```
/seo-tools:research
```

The skill walks you through an interactive 7-stage pipeline:

1. **Competitor discovery** — provide domains manually or let Claude find them via web search
2. **Onboarding** — choose output directory, set parameters (location, language, keyword limits)
3. **Data collection** — fetch ranked keywords from DataForSEO API
4. **Preprocessing** — merge, filter, calculate opportunity scores
5. **Embeddings + Clustering** — group keywords by search intent (K-means)
6. **Strategy analysis** — categorize competitor pages into strategy types (comparison, platform, vertical, etc.)
7. **Final report** — SEO Master Plan with ranked strategies and implementation recommendations

## Agents

The plugin includes 4 specialized agents:

| Agent | Purpose |
|-------|---------|
| `competitor-discovery-agent` | Find all competitors in a niche from seed domains |
| `seo-strategy-reserach-agent` | Analyze one competitor domain, output strategy JSONs |
| `seo-strategy-planner` | Create implementation plan for one strategy type |
| `seo-homepage-analyst` | Deep analysis of competitor homepage positioning |

## API Keys Required

You'll be prompted to configure these on first run. Keys are stored in `.env.local` inside your project directory (git-ignored).

| Service | Keys | Purpose |
|---------|------|---------|
| [DataForSEO](https://dataforseo.com) | `DATAFORSEO_LOGIN`, `DATAFORSEO_PASSWORD` | Keyword rankings data |
| [OpenRouter](https://openrouter.ai) | `OPENROUTER_API_KEY` | Text embeddings for clustering |

## Output

```
your-project/seo-research/
├── config.json                 # Project settings
├── .env.local                  # API keys (git-ignored)
├── .cache/                     # Raw data, embeddings, clusters (git-ignored)
├── competitors/
│   └── domain.com/
│       ├── homepage.json       # Homepage analysis
│       ├── comparison-pages.json
│       └── ...                 # Strategy JSONs
└── strategies/
    ├── 0_SEO_Master_Plan.md    # Executive summary + ranked strategies
    ├── homepage.md             # Homepage optimization plan
    ├── comparison-pages.md     # Strategy implementation plans
    └── ...
```

## Requirements

- [Claude Code](https://claude.ai/code) CLI
- [uv](https://docs.astral.sh/uv/) — installed automatically if missing
- Python 3.10+ (managed by uv)

## Updating

```bash
/plugin marketplace update ksanderer-seo-research
/plugin update seo-tools@ksanderer-seo-research
```

## License

MIT
