# Rewrite Rules

How to fix each of the 14 readiness factors. The review skill records *what* failed and *where*; this file says *how* to fix it. Every fix restructures or clarifies existing facts. None of them adds a fact that isn't already in the source.

## The Fact Lock

Before rewriting, list every hard fact in the original article: numbers, prices, limits, durations, plan names, policies, URLs, UI labels, error codes. After rewriting, check the list again. Every fact must appear in the new version with the same value. Nothing new may appear.

If a fix needs a fact the article doesn't contain (an exact number, a plan name, a confirmation message), **don't invent it**. Insert a visible placeholder and log it:

```html
<p><strong>[NEEDS INPUT: exact rate limit per plan]</strong></p>
```

Articles with placeholders are never written back to Intercom. They are saved locally and listed under "Needs input" in the log.

---

## 1. Jobs to be done

Open with one sentence starting "Use this article to…" followed by two or three concrete tasks the article supports.

- Before: "Rate limits cap how many requests you can make."
- After: "Use this article to understand Firecrawl rate limits, find out why you're getting a 429 error, and fix it with retries or a plan upgrade."

## 2. Disambiguation

Replace every dangling pronoun with its noun. Read each sentence alone; if the subject isn't in it, add it.

- Before: "It resets each month."
- After: "Your plan's credit allowance resets each month."

## 3. Self-contained sections

Each section opens by naming its subject. Remove openers that depend on the previous section ("Next,", "Also,", "In that case,"). If a section only makes sense after another one, either merge them or restate the needed context in one sentence.

## 4. Semantic chunk boundaries

One topic per heading. Split any section covering two tasks into two sections. Add a subheading roughly every 150–250 words. Restate the heading's topic in the section's first sentence, because Fin may not capture the HTML heading.

## 5. Query-answer symmetry

Rephrase headings as the question a customer would type. Rewrite yes/no answers so the answer restates the question.

- Heading before: "Throttling" → after: "Why am I getting a 429 error?"
- Answer before: "No." → after: "No, failed scrapes that return no document do not use credits."

Use wording from real conversations when the review includes coverage data.

## 6. Structured enumeration

- Sequential steps → `<ol>`
- Options or items → `<ul>`
- Every "the following:" is followed by a list
- A sentence with three or more parallel items → bulleted list

## 7. Instruction completeness

After the last step, add what the customer sees when it worked, and what to do if they don't see it. If the source doesn't say what success looks like, use a `[NEEDS INPUT]` placeholder.

## 8. Numerical clarity

Replace vague quantities with the exact value from the source. If the source has no exact value, use a `[NEEDS INPUT]` placeholder — never estimate. When a customer would need to calculate something, add a worked example using only numbers already in the article.

- Before: "Retry after a short wait."
- After: "Retry after 1 second. If you get another 429, wait 2 seconds, then 4 seconds."

## 9. Defined terms

Define every acronym and product-specific term the first time it appears, in a short clause, then use the short form.

- "…returns a 429 (Too Many Requests) error…"
- "Concurrency (how many jobs can run at the same time) depends on your plan."

## 10. Audience specification

State who the article applies to near the top: plans, roles, regions, permissions. Label every contact detail by purpose. If behavior differs by plan and the source lists the plans, use a table (see factor 13).

## 11. Limitations and workarounds

Turn vague caveats into a specific statement: what doesn't work, where, and what to do instead. If the source only says "some plans" with no detail, use a `[NEEDS INPUT]` placeholder.

## 12. Entity distribution

Name the feature or product in every section, at least once, in full. Replace "the button", "the limit", "this setting" with the named thing.

## 13. Context in tables

Put one sentence before every table, callout, and code block saying what it shows and where it applies: "The table below shows the rate limit for each Firecrawl plan:"

## 14. Visual content and alt text

Add descriptive alt text to every image. If an image shows a process, write the steps as a numbered list next to it. You cannot upload images through the MCP — keep existing `<img>` tags and their `src` exactly as they are.

---

## Help Center Fixes

| Finding | Fix |
|---------|-----|
| Title is an internal label | Rewrite as the customer's question or task: "How many credits does a scrape cost?" |
| Missing description | Write one sentence on what the reader gets, ≤ 140 characters |
| Description > 140 characters | Shorten to ≤ 140 characters, keep the task |
| Critical fact buried in body | Move it into a bold "Important:" line directly under the relevant heading |
| Duplicate articles | Don't merge automatically. Propose which one to keep in the log; the user decides |
| Stale article | Don't change facts because they look old. Flag "verify current values" in the log |

## Resolved Conflicts

When `content-review.yaml` has a conflict with `resolution` filled in, rewrite every affected article to use the resolved statement. When `resolution` is null, skip the article and list it under "Blocked by conflict".
