# Help Center Checks

These checks sit alongside the 14 factors. They are about how an article is named, described, organized, and kept current — things that affect whether Fin (and customers browsing) find the right article at all.

## Article-Level Checks

| Check | How to detect | Severity |
|-------|---------------|----------|
| **Title in customer language** | Title is a product or internal label ("Credit accounting model") rather than what a customer would type ("How many credits does a scrape cost?") | medium |
| **Title is task-framed** | Title names a feature ("Calendar integration setup") instead of the goal ("How to schedule a meeting") | low |
| **Description present** | `description` field is empty | medium |
| **Description length** | `description` longer than 140 characters | low |
| **Description is useful** | Description repeats the title or says "This article explains…" without saying what the reader gets | low |
| **Callouts for key facts** | Critical warnings (billing, data loss, irreversible actions) are buried in body text instead of a labeled callout or bold "Important:" line | medium |
| **Staleness** | `updated_at` older than 12 months (flag), older than 24 months (high) | medium / high |
| **Draft vs published** | State is `draft` — Fin only uses published public articles (unless internal/audience settings say otherwise) | info |
| **Orphaned** | `parent_id` is null — the article is not in any collection | low |
| **Title H1 duplication** | The body opens with an H1 that repeats the title. Intercom renders the title separately (not as H1), so this is allowed for accessibility but should not be counted as a content heading | info |

## Cross-Article Checks

Run these across the whole inventory, not per article.

### Source conflicts (highest priority)

The same fact stated two different ways in two places. Fin may answer with either version.

**How to detect:**
1. Extract every hard fact from each article: numbers, prices, limits, durations, plan names, yes/no policies ("credits roll over", "refunds are available").
2. Group facts by subject (e.g. "credit rollover on Enterprise").
3. Flag any subject with two or more different values.
4. If the user named public pages that are also Fin sources (pricing page, docs), fetch them and include their facts in the comparison.

Record both statements verbatim, both sources, and which one looks more recent or more authoritative. Do **not** decide which is correct — that is a question for the user.

### Duplicates

Two articles that answer the same question. Detect by near-identical titles, or `search_articles` on each title's key phrase returning another article that covers the same task. Duplicates split Fin's retrieval and drift apart over time.

### Collection structure

Check whether collections follow a familiar information architecture. A common pattern:

- **Overview** — pricing, plans, company basics
- **Getting started** — onboarding and first steps
- **Core features** — one group per feature: explainer, setup, best practices, troubleshooting, FAQ
- **Security and privacy** — policies and compliance
- **Integrations** — third-party tools

Report collections that mix unrelated topics or have a single article. This is a low-severity, observational check.

### Coverage gaps (optional — needs conversations)

If the workspace has conversation history:
1. Pull a sample of recent closed conversations with `search_conversations` (per_page up to 150).
2. For each sampled conversation, note the customer's opening question in their own words.
3. Cluster the questions into topics.
4. For each topic, `search_articles` for a matching article.
5. Report topics with volume and no matching article, and topics where customer wording differs sharply from the article title.

Skip this step if the workspace has no conversations, and say so in the report.
