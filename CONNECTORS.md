# Connectors

This plugin works through the Intercom MCP. Without it, the skills can only work on article text you paste in.

## ~~intercom — Intercom Workspace (required)

| Tool | Purpose | Used by |
|------|---------|---------|
| `list_articles` | Inventory every help center article with metadata (state, updated_at, parent collection) | review-content |
| `get_article` | Read an article's full HTML body | review-content, optimize-content |
| `search_articles` | Find articles covering the same topic (conflict and duplicate checks) | review-content, optimize-content |
| `search_conversations` / `search` | Pull recent customer conversations to see how customers phrase questions and which topics have no article | review-content (optional coverage check) |
| `get_conversation` | Read a sampled conversation in full | review-content (optional coverage check) |
| `update_article` | Write an optimized body, title, or description back to a **draft** article | optimize-content |
| `create_article` | Create a new draft when a published article's rewrite needs staging, or when a section is split into its own article | optimize-content |

### What the Intercom MCP cannot do

These live only in the Intercom app. Skills that need them prepare exact instructions instead of acting:

- Enabling Fin, setting its tone, guidance rules, or handover
- Snippets, internal articles, and synced external sources (not exposed as tools)
- Audience rules and article targeting
- Batch testing Fin and reading CX Score
- Deleting articles

## ~~web — Public Pages (optional)

| Tool | Purpose | Used by |
|------|---------|---------|
| Web fetch / Firecrawl | Read public pages (pricing, docs) that also serve as Fin sources, to check them against help center articles for conflicts | review-content |
