---
applyTo: "content/**/*.md"
---

**When to use:** Any content editing, post writing, or Markdown change under `content/`. These rules are adapted from the Camunda docs content instructions and tailored to a personal technical writing portfolio.

## 1. Language and grammar

- Default to **American English** (US spelling: "analyze", "color", "organize").
- Use **second person** ("you", "your") and **active voice** for tutorials, how-tos, integration guides, and reference content.
- First person ("I", "my") is acceptable in personal posts, introductions, and short asides about the author's own setup (for example, "I use VS Code"). Don't use it for instructions the reader must follow.
- Use **common contractions** (you'll, don't, it's) for a natural, conversational tone.
- Write whole numbers **one through nine** in full; use numerals for **10 and above**. Use numerals with units and percentages (for example, "5 MB", "10%").
- Avoid Latin abbreviations (e.g., i.e., etc.). Write "for example", "that is", or "and more", or end the list cleanly.
- Use **gender-neutral language**: "they" for a user.
- Replace vague "it", "this", or "that" with the specific noun when the referent is ambiguous.
- Use **empowering language**: "With webhooks, you can…" rather than "Webhooks allow you to…".
- Don't use "please" in instructional steps.
- Avoid directional references such as "below" and "above" ("the steps below"). Write "the following steps" or link to the section.
- Use one space after a period.

## 2. Punctuation

- Use the **Oxford comma** (for example, "Python, Flask, and ngrok").
- Use **en dashes** (–) for date and number ranges; **hyphens** (-) for compound adjectives.
- Avoid em dashes (—). Use shorter sentences, colons, or parentheses instead.
- Don't use quotation marks for UI elements, buttons, or section names. Use **bold**.
- Use double quotation marks only for direct speech or quoted text.
- Omit hyphens in prefixed words (reactivate, undo, prerequisites) unless the result looks incorrect.

## 3. Formatting and structure

- Use **sentence case** for the `title` front matter and all headings: capitalize only the first word and proper nouns (for example, "Creating a webhook receiver", "Docker for Java developers").
- Don't use the `title` as an H1 in the body. PaperMod renders it. Start body headings at `##`.
- Don't put bold or other formatting inside headings (`## **Overview**` → `## Overview`). Don't end headings with a colon.
- Make headings **descriptive and action-oriented** ("Install ngrok", "Send a GET request") rather than generic ("Overview", "Introduction", "Conclusion") where possible. Use parallel verb forms for sibling headings.
- Don't skip heading levels (`##` → `####`).
- **Bold** UI element names and button labels (for example, `Select **Save**`). Don't use bold for emphasis.
- Use `>` to separate UI navigation steps (for example, `**File > New > Project**`).
- Use *italics* only for emphasis on a specific word.
- Put **filenames**, **commands**, **package names**, and **code identifiers** in inline code (for example, `main.py`, `pip`, `boto3`).
- Use **fenced code blocks with a language identifier** (`bash`, `python`, `json`, `xml`, `yaml`, `http`) for all multi-line code and for commands the reader copies.
- Keep paragraphs to **four to five sentences** at most.
- Use **bulleted lists** with dashes (`-`), not asterisks, for three or more unordered items. Capitalize the first word of each item.
- Use **numbered lists** for sequential steps. `1.` for every item is fine.
- Mark optional steps as `(Optional) Do the thing.`
- Hugo and PaperMod have no admonition syntax. For a note or warning, use a blockquote that starts with a bold label (for example, `> **Note:** …`). Use them sparingly, never stack them, and never put required steps inside one.

## 4. Front matter

Every page uses YAML front matter delimited by `---`:

```yaml
---
title: "Sentence case title"
date: 2026-10-15T09:00:00-05:00
draft: true
description: "One sentence under 160 characters that says what the reader gets from this page."
tags: ["api", "python"]
---
```

- `title`, `date`, and `draft` are required. Keep `title` in double quotes.
- Add `description` to every new post. PaperMod uses it for the post list, search, and social previews. Don't backfill existing posts unless asked.
- `tags` are optional. Use lowercase, and reuse existing tags before inventing new ones.
- New posts start as `draft: true`. Only the author publishes.
- Don't change an existing post's `date`.

## 5. Links

- Link to other posts on this site with Hugo's `relref` shortcode so broken links fail the build: `[webhook security]({{< relref "posts/webhooks.md#security" >}})`.
- Link to the most relevant **section anchor**, not just the top of a page.
- Use **descriptive link text**. Never use "here", "click here", "this article", or a bare URL as link text.
- Prefer existing sentence text as the link. Use "Learn more about …" only when no suitable text exists.
- Link external references to the most specific page or anchor (for a GitHub repo, the relevant file, not the repo root).
- Write "GitHub" with a capital H.

## 6. Images

- Store images in `static/images/<post-slug>/`, where `<post-slug>` matches the post's filename without `.md`. Reference them with a root-relative path: `![Alt text](/images/<post-slug>/file.png)`.
- Every image needs **descriptive alt text** that states what the image shows, not "image" or "screenshot".
- Never use an image as the only source of a value, command, or field name the reader needs. Include it in the text too.
- Name image files in lowercase kebab-case.
- Crop personal information (account IDs, emails, API keys, IP addresses) from screenshots.
- Avoid GIFs.

## 7. Terminology

| Use | Not |
| --- | --- |
| GitHub | Github, github |
| JavaScript | Javascript |
| macOS | MacOS, Mac OS |
| VS Code | VSCode, vscode |
| JSON, XML, YAML, REST, API, SDK | json, Json, Rest |
| webhook (lowercase in running text) | Webhook, web hook |
| Amazon RDS, AWS Lambda (full service name on first use) | RDS alone on first use |
| prerequisites | pre-requisites |
| set up (verb), setup (noun) | setup (as a verb) |
| sign in | login (as a verb) |

- Spell out acronyms on first use unless they're standard for a technical audience (API, JSON, HTTP).
- Don't capitalize file extensions (.md, .json, .yaml).
- Don't capitalize general terms such as "server", "endpoint", or "payload" unless they start a sentence.

## 8. Troubleshooting sections

Apply this pattern to any troubleshooting section or list of common errors:

- **One entry per visible symptom**, not per root cause.
- **Three parts per entry**: what the reader sees (exact error text or behavior), why it happens, and how to fix it (concrete steps, not "check your configuration").
- **Quote exact error text** in inline code or a code block so readers can search for it.
- **Pair every cause with a fix.**

## 9. AI-ready content

These rules make posts easier for search engines, AI assistants, and readers who skim:

- **Opening sentences**: the first sentence after the front matter and after each heading directly says what the page or section covers, in one self-contained sentence under 150 characters.
- **Descriptive headings**: specific and action-oriented ("Configure the Flask route"), not generic.
- **Self-contained sections**: avoid "as mentioned above" or "now that you've done X". Repeat the needed context.
- **Tables over prose** for lists of fields, parameters, HTTP status codes, or options.
- **Complete code blocks**: closed fences, a language tag, and examples that run as written.

## 10. WordPress-import cleanup

Posts were exported from WordPress and still contain conversion artifacts. When you edit a post, fix these in that post only:

- **Old blog links**: replace `entwineinwords.wordpress.com/...` links to posts that exist in `content/posts/` with a `relref` link. Keep the anchor if the heading still exists.
- **Backticks inside fences**: remove stray inline backticks wrapping the code inside fenced blocks (for example, a fence containing `` `pip install flask` ``), and add the language identifier.
- **Lost indentation**: restore indentation in Python, JSON, XML, and YAML examples so they're valid. If you can't infer the correct structure, flag it instead of guessing.
- **Bold in headings** and **title case** headings: convert to plain sentence case.
- **Empty alt text** (`![](...)`): add descriptive alt text based on the surrounding content.
- **Escaped characters** such as `\_`, `&amp;`, or `&nbsp;`: replace with the literal character where Markdown doesn't need the escape.
