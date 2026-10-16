---
applyTo: "**"
---

**When to use:** All files. Read this before any change to understand the repo structure, Hugo conventions, validation, and commit conventions.

## 1. Repo structure

This is a **Hugo** static site using the **PaperMod** theme, deployed to GitHub Pages at https://janetjotw.github.io by GitHub Actions on every push to `main`.

| Path | Contents |
| --- | --- |
| `content/posts/` | Blog posts and writing samples (one Markdown file per post) |
| `content/*.md` | Top-level pages linked from the main menu (`about-me.md`, `services.md`, `api-reference.md`, `resources.md`, `blog.md`) |
| `static/images/<post-slug>/` | Images for each post, served at `/images/<post-slug>/` |
| `archetypes/default.md` | Template Hugo uses for `hugo new` |
| `hugo.toml` | Site config: title, menus, theme params, social icons, outputs |
| `themes/PaperMod/` | Theme, as a Git submodule. Don't edit. |
| `layouts/` | (Create if needed) Overrides for PaperMod templates and custom shortcodes |
| `.github/workflows/` | GitHub Pages build and deploy workflow |
| `.github/instructions/` | Agent instruction files |

- Name content files in **lowercase kebab-case** matching the page title (for example, `creating-a-webhook-receiver.md`). The filename becomes the URL slug, so don't rename published posts unless asked.
- Don't commit `public/` or `.hugo_build.lock`. They're in `.gitignore`.

## 2. Adding, moving, or removing pages

- **Adding a post**: run `hugo new posts/<slug>.md`, then update the front matter to match `content.instructions.md` (YAML, sentence-case title, `description`). Put images in `static/images/<slug>/`.
- **Adding a top-level page**: create `content/<slug>.md` and add a `[[menu.main]]` entry in `hugo.toml` only if the user asks for it in the menu.
- **Renaming or moving a published post**: add the old path to an `aliases` list in the post's front matter (for example, `aliases: ["/posts/old-slug/"]`) so existing links keep working. Update `relref` links that point to it.
- **Removing a post**: prefer setting `draft: true` over deleting the file, unless the user asks to delete it. Search for `relref` links to it and update them.

## 3. Build and validation

Commands:

- `git submodule update --init --recursive`: fetch the PaperMod theme (needed after a fresh clone).
- `hugo server -D`: run a local preview at http://localhost:1313, including drafts.
- `hugo --minify`: build the site the same way CI does. Output goes to `public/`.

Rules:

- CI uses **Hugo extended 0.160.1** (see `.github/workflows/`). Match it locally when possible. Don't change the CI version unless asked.
- Run `hugo --minify` once after final changes. It catches broken `relref` links, bad front matter, and template errors.
- Don't run builds speculatively during exploration.
- Don't change the deploy workflow, `baseURL`, or theme without an explicit request.

## 4. Commits and pull requests

- Commit messages use the format `{type}: {description}` or `{type}(scope): {description}`.
  - Types: `docs` (content), `feat` (new page, section, or site feature), `fix` (broken link, image, or build), `style` (formatting-only cleanup), `chore` (config, dependencies, tooling), `ci` (workflow changes).
  - Scope is optional and usually the post slug or area (for example, `docs(webhooks): add troubleshooting section`).
  - Keep the header under 72 characters, in the present tense and imperative mood.
- One logical change per commit. Keep style cleanup in separate commits from content changes so diffs stay reviewable.
- For changes beyond a small fix, work on a branch and open a pull request against `main` rather than pushing directly, because pushing to `main` deploys the live site.
- In the PR description, list the posts changed, what changed, and any validation that was skipped.
