# Intercom Article Editor Rules

What the Intercom article editor supports, and the rules for writing article HTML through the MCP so it renders correctly.

## HTML Through the API

- **No whitespace between block tags.** Newlines or indentation between `</p>` and `<h2>` become empty paragraphs. Write the body as one continuous string: `<p>…</p><h2>…</h2><ul><li>…</li></ul>`.
- **Deliberate blank line:** `<p>&nbsp;</p>`.
- **Title is not an H1.** Intercom renders the article title in a `<header>`. Start the body with an opening paragraph, and use `<h2>` for sections and `<h3>` for subsections. An H1 repeating the title is allowed for accessibility but isn't needed.
- **Intercom normalizes headings.** Observed on 2026-09-30: an `<h2>` sent through `update_article` / `create_article` is stored as `<h1>` (the editor's large heading), with an id added. The structure is kept, so this isn't an error. Don't "fix" it, and don't flag stored `<h1>` section headings as a problem in reviews.
- **Intercom adds its own markup.** Stored bodies wrap text in `<p class="no-margin">`, turn `<strong>` into `<b>`, and wrap tables in a styled container. Compare stored bodies by text and structure, not by exact HTML.
- **No JavaScript.** Buttons render as styled links; `onclick` and scripts don't run.

## Supported Elements

| Element | HTML | Use it for |
|---------|------|-----------|
| Headings | `<h2>`, `<h3>` | Section and subsection boundaries (factor 4) |
| Paragraph | `<p>` | Body text |
| Bold / italic | `<strong>`, `<em>` | "Important:" and "Note:" labels |
| Inline code | `<code>` | Parameter names, status codes, CLI flags |
| Code block | `<pre><code>…</code></pre>` | Commands and snippets; introduce with a sentence |
| Lists | `<ol>`, `<ul>`, `<li>` (nest by placing a list inside `<li>`) | Steps and options (factor 6) |
| Table | `<table><tbody><tr><td>` | Plan comparisons, limits by tier (factor 13) |
| Link | `<a href="…">` | Links to other articles and pages |
| Image | `<img src="…" alt="…">` | Keep existing images only; max width 650px |
| Divider | `<hr>` | Separating major parts |

## Editor-Only Features

These exist in the editor but can't be created reliably through the API. If one would help, recommend it in the optimization log for the user to add by hand:

- **Callout blocks** (colored boxes for important information)
- **Collapsible sections** (hide auxiliary detail)
- **Video and interactive demo embeds**
- **File attachments**
- **Buttons**

Through the API, use a bold label instead of a callout:

```html
<p><strong>Important:</strong> Pay-as-you-go credits expire if you cancel your subscription.</p>
```

## Editor Limits

- Tables can't go inside callouts or collapsible sections.
- Deleting a table deletes everything in it.
- Images: PNG, JPEG, SVG, GIF; up to 104 MB; displayed at up to 650px wide.
- Fin includes at most 3 images in any single answer, so every image-based process must also be written as text.

## Template

`assets/article-template.html` shows a full article following these rules, with the whitespace removed.
