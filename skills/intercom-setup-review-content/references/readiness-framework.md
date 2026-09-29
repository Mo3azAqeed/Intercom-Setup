# Fin Content Readiness Framework

Fourteen factors decide whether an article is ready for Fin AI Agent and Copilot to retrieve and use. They come from Intercom's guidance on optimizing content for Fin. This file is the detection side: how to tell whether an article passes. The fix patterns live in the optimize skill.

**Why these matter:** Fin does not read an article top to bottom. It retrieves chunks — usually a section under a heading — and answers from those. Every factor below is a way a chunk can fail when it is pulled out of its article.

## How to Score Each Factor

Score every factor for every article as one of:

| Score | Meaning |
|-------|---------|
| `pass` | No instance of the problem found |
| `partial` | The problem appears once or twice, or only in a minor section |
| `fail` | The problem is systemic, or appears in the section that answers the article's main question |
| `n/a` | The factor cannot apply (e.g. factor 14 on an article with no images) |

Always record **evidence**: the exact phrase, heading, or block that triggered a `partial` or `fail`. A score without evidence is not useful to the optimize skill.

---

## 1. Jobs to be done

**Test:** Does the first paragraph say what the reader will be able to *do* after reading?

- Pass: "Use this article to check your credit balance, set a monthly spending limit, and understand what happens when credits run out."
- Fail: "This article is about credits." / The article opens straight into steps or a table with no opening paragraph.

**Why it matters:** Fin uses the opening to decide what the article is for. A topic label instead of a task weakens how often the article surfaces.

## 2. Disambiguation

**Test:** Is every reference self-descriptive? Search for sentences that start with or lean on "it", "this", "they", "that", "the above", "as mentioned" where the subject is not in the same sentence.

- Pass: "The monthly limit caps how much pay-as-you-go can spend."
- Fail: "It caps how much you can spend."

## 3. Self-contained sections

**Test:** Read each section on its own, as if it were the only thing Fin retrieved. Does it still make sense and name its subject?

- Fail signals: a section that opens with "Next," "Also," "Alternatively," "In that case"; a section that only works after reading the section above.

## 4. Semantic chunk boundaries

**Test:** Does each section under a heading cover exactly one topic? Are long stretches broken up by headings?

- Fail signals: a section covering two or more distinct tasks; more than roughly 250 words with no subheading; a heading whose section drifts into an unrelated topic.
- Also check: the section's opening sentence repeats the heading's topic in words, because Fin may not capture the HTML heading itself.

## 5. Query-answer symmetry

**Test:** Do headings (and the title) mirror how a customer would phrase the question? Does the answer restate the question instead of replying "Yes." or "No."?

- Pass heading: "Why am I getting a 429 error?"
- Fail heading: "Throttling behavior"
- Fail answer: "Yes." with no restated subject.

## 6. Structured enumeration

**Test:**
- Multi-step processes are numbered lists.
- Sets of options or items are bulleted lists.
- Any sentence ending in "the following:" is followed by an actual list.
- No paragraph packs three or more parallel items into one sentence that should be a list.

## 7. Instruction completeness

**Test:** Does every set of steps say what happens after the last step — the confirmation the customer sees, and what to do if they don't see it?

- Fail: steps end on "Click Save."

## 8. Numerical clarity

**Test:** Search for vague quantities: "a few", "some", "several", "shortly", "soon", "a while", "quickly", "up to a point", "limited", "may take time". Every number, limit, threshold, price, and duration should be exact.

- Also fail: the article expects the reader (or Fin) to calculate something — adding durations, multiplying rates — without a worked example.

## 9. Defined terms

**Test:** Is every acronym and product-specific term defined the first time it appears? List every acronym and internal term found and whether it was defined.

- Common misses in developer products: API, SDK, MCP, rate limit, concurrency, credit, webhook, 402/429 status codes.

## 10. Audience specification

**Test:** Does the article say who it applies to — which plans, roles, permissions, or regions? Are contact details labeled by purpose?

- Fail: plan-specific behavior described with no plan named; "Contact us" with a list of addresses and no label for which situation each is for.

## 11. Limitations and workarounds

**Test:** Are known limits and edge cases stated specifically — what doesn't work, where, and what to do instead?

- Fail: "Some plans may not support this." / "This may not work in all cases."

## 12. Entity distribution

**Test:** Does the feature or product name appear in every section, not just the opening? A section that says "click the button in the top right" without naming the feature fails.

## 13. Context in tables

**Test:** Is every table (and every standalone block: callout, code block, image) introduced by a sentence that says what it covers?

## 14. Visual content and alt text

**Test:** Does every image have descriptive alt text? Is every process shown in an image also written out as text steps? (Fin sends at most three images per answer and cannot read instructions that only exist inside a screenshot.)

---

## Quick Reference

| # | Factor | One-line test |
|---|--------|---------------|
| 1 | Jobs to be done | Opening states what the reader will accomplish |
| 2 | Disambiguation | No dangling "it/this/they" |
| 3 | Self-contained sections | Each section makes sense alone |
| 4 | Semantic chunk boundaries | One topic per heading; heading topic restated in first sentence |
| 5 | Query-answer symmetry | Headings phrased as customer questions; answers restate the question |
| 6 | Structured enumeration | Steps numbered, items bulleted |
| 7 | Instruction completeness | Steps end with the confirmation and a fallback |
| 8 | Numerical clarity | Exact numbers; no math left to the reader |
| 9 | Defined terms | Acronyms and product terms defined on first use |
| 10 | Audience specification | Plan/role/region stated; contacts labeled |
| 11 | Limitations and workarounds | Limits stated specifically with a workaround |
| 12 | Entity distribution | Feature name appears in every section |
| 13 | Context in tables | Every table and block has an intro sentence |
| 14 | Visual content and alt text | Alt text on images; image steps also in text |
