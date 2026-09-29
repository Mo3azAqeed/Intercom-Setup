# Intercom Setup

**Fin isn't the problem. The content you feed it is.**

Fin AI Agent answers from your help center. When an article is vague, mixes three topics under one heading, hides a limit in a screenshot, or disagrees with another article, Fin gives a vague, unfocused, or wrong answer — and your resolution rate stalls.

Intercom Setup works directly inside your Intercom workspace through the Intercom MCP. It reviews every article against Fin's content readiness framework, then rewrites the ones that fail so Fin can retrieve and use them.

**Works in:** Claude Code · Claude (with the Intercom connector) · any AI agent tool with MCP support

---

## See It In Action

Connect Intercom, then start talking:

```
You: review my help center content
AI:  [Pulls every article through the Intercom MCP, scores each against 14 factors]
     24 articles reviewed. 6 ready, 11 need work, 7 not ready. 2 source conflicts.
     Saved to .intercom/content-review.yaml

You: optimize content
AI:  [Rewrites the highest-priority articles to pass every factor]
     5 articles rewritten. 3 drafts updated in Intercom, 2 published articles
     staged locally for your approval. Log saved to .intercom/optimization-log.md
```

---

## The Lifecycle

```
review-content → optimize-content → (more skills coming)
```

| Skill | What it does | Output |
|-------|-------------|--------|
| **intercom-setup-review-content** | Reads your help center through the Intercom MCP and scores every article against Fin's 14-factor content readiness framework plus help center conventions. Flags conflicts between articles. Describes, doesn't rewrite. | `.intercom/content-review.yaml`, `.intercom/reviews/YYYY-MM-DD.md` |
| **intercom-setup-optimize-content** | Takes the review, rewrites failing articles to pass every factor without changing the facts, and writes them back to Intercom as drafts. | `.intercom/optimized/`, `.intercom/optimization-log.md` |

Every skill reads what the previous one wrote to `.intercom/`, so each step can run without re-asking you for context.

---

## What These Skills Do

They make your knowledge base **retrievable** by Fin: each section self-contained, each number exact, each heading phrased the way customers ask, each limitation written down.

### What They Don't Do

- Turn Fin on or change Fin settings (the Intercom MCP can't reach those)
- Invent facts, prices, limits, or policies — optimization only restructures what's already true
- Publish anything without your approval
- Delete articles

---

## What's Inside

- **The 14-factor content readiness framework** — each factor with a detection test and a fix pattern
- **Help center conventions for Fin** — titles in customer language, 140-character descriptions, collection structure
- **Intercom editor rules** — what the article editor and API accept, and where formatting breaks (tables inside callouts, blank space from HTML whitespace, the title not being an H1)
- **Source conflict detection** — the same fact stated two different ways across articles
- **A default style guide** you can override with your own

---

## Setup

1. Install this plugin. It ships a `.mcp.json` that registers the Intercom MCP server (`https://mcp.intercom.com/mcp`); sign in to Intercom when prompted. In Claude, you can use the Intercom connector instead.
2. Say **"review my help center content"**.
3. Resolve any conflicts the review finds, then say **"optimize my content"**.

Everything the skills produce lives in `.intercom/` in your working directory:

```
.intercom/
├── scope.md                  # Fin's first job and audience (optional, read if present)
├── style-guide.md            # Your style guide (optional, overrides the default)
├── content-review.yaml       # Scored inventory of every article
├── reviews/
│   └── 2026-09-30.md         # Dated review reports
├── optimized/
│   ├── 17234720-rate-limits.html           # Rewritten body
│   └── 17234720-rate-limits.original.html  # Original, for undo
└── optimization-log.md       # What changed, what needs input, what's blocked
```

See [CONNECTORS.md](CONNECTORS.md) for which tools each skill uses.

---

## License

MIT
