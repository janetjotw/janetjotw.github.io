# Agent instructions for janetjotw.github.io

This file provides instructions for AI agents (Claude Code, GitHub Copilot) working in this repository.

This repo is Janet Jose's technical writing portfolio, built with Hugo and the PaperMod theme and published at https://janetjotw.github.io. The content was exported from the WordPress blog at `entwineinwords.wordpress.com`.

## Before editing

Read the relevant files in `.github/instructions/`:

- **`content.instructions.md`**: language and grammar, punctuation, formatting, links, images, terminology, front matter, and WordPress-import cleanup. Read before any Markdown content change.
- **`repo.instructions.md`**: repo structure, Hugo conventions, build and validation commands, and commit and PR conventions. Applies to all files.

## Scope

Prefer the smallest safe change that satisfies the request.

For content-only tasks:

- Edit only the files named in the task, plus their co-located images in `static/images/<post-slug>/` when needed.
- Don't rewrite a post's voice, structure, or technical claims unless asked. Style fixes are fine. Changing what the post says is not.
- Don't apply style cleanup to posts outside the task, even if they break the rules in `content.instructions.md`. Mention them in your summary instead.
- Don't change `draft` status, publish dates, or `hugo.toml` unless asked.
- Don't modify the `themes/PaperMod` submodule. Override theme templates by adding files under `layouts/` instead.

## Validation

- For Markdown-only changes, run `hugo --minify` once after final edits to confirm the site builds. Don't run it speculatively during exploration.
- Run `hugo server -D` only when the user wants to preview a page or the change affects layout, menus, or shortcodes.
- If the theme submodule is missing, run `git submodule update --init --recursive` first.
- If Hugo isn't installed or validation is blocked, make the requested edit and state what validation was skipped and why.

