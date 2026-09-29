# Output Formats

## `.intercom/optimized/<article-id>-<slug>.html`

One file per rewritten article: the final body HTML exactly as it will be (or was) sent to `update_article`, with no whitespace between block tags. Put the proposed title and description in a comment on the first line so the file is self-contained:

```html
<!-- title: How do I fix a 429 rate limit error? | description: Why Firecrawl returns a 429 error and how to retry or raise your limit. -->
<p>Use this article to…</p><h2>…</h2>
```

Also save the original body as `.intercom/optimized/<article-id>-<slug>.original.html` before any write, so the change can be undone.

## `.intercom/optimization-log.md`

Append a new dated section on every run. Never overwrite earlier runs.

```markdown
## Run — YYYY-MM-DD

**Source review:** .intercom/reviews/YYYY-MM-DD.md · **Articles in this run:** 5

### Written to Intercom (drafts)

| Article | ID | Before | After | Fields changed |
|---------|----|--------|-------|----------------|
| How do I fix a 429 rate limit error? | 17234720 | Not ready (5 fails) | Ready | title, description, body |

### Staged for approval (published articles)

| Article | ID | Local file | Draft copy ID |
|---------|----|-----------|---------------|
| How many credits does each request cost? | 17234712 | optimized/17234712-credits.html | 17239001 |

### Needs input

| Article | Placeholder | What's missing |
|---------|-------------|----------------|
| Rate limits and 429 errors | [NEEDS INPUT: requests per minute per plan] | Exact per-plan limits |

### Blocked by conflict

| Article | Conflict subject |
|---------|------------------|

### Manual follow-ups in the Intercom editor

- Add a callout block for the "Important:" line in article 17234717
- Consider an audience rule so article 17234720 only shows to paid plans

### Fact check

For each article: "N facts in original, N facts in rewrite, 0 added, 0 changed" — or list any difference.
```

## `.intercom/content-review.yaml` updates

After writing an article, update its entry in place:

```yaml
    optimized:
      at: 2026-09-30
      file: .intercom/optimized/17234720-rate-limits.html
      written_to: intercom_draft   # intercom_draft | draft_copy | local_only
      rescored_readiness: ready
```

Don't change the original factor scores — they record the state at review time. The next review run rescores from Intercom.
