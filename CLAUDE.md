# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Serve locally with live reload
bundle exec jekyll serve

# Build the site (outputs to _site/)
bundle exec jekyll build

# Install dependencies
bundle install
```

The site runs at `http://localhost:4000` by default. Changes to `_config.yml` require a server restart — other files hot-reload.

## Architecture

This is a Jekyll 4 static site deployed to GitHub Pages at `https://malikalabbas.github.io/`.

**Collections** (defined in `_config.yml`):
- `_projects/` → `/projects/:name/` — project write-ups
- `_blog/` → `/blog/:name/` — blog posts and notes
- `_blog` entries are also exposed under the name `musings` in some nav contexts (`/musings/` permalink shows in `_site/`)

**Index pages** (`blog.md`, `projects.md`) iterate over their respective collections using `{% for p in site.blog %}` / `{% for p in site.projects %}` and render cards via the `.projects-grid` / `.project-card` CSS classes.

**Layouts**:
- `minima` theme provides `default`, `page`, `post` — all pages currently use `layout: page`
- `_layouts/homepage.html` extends `default` with a two-column aside/main grid (currently unused by index.markdown, which uses `page`)

**Styling** (`assets/main.scss`): imports minima then adds overrides — card grid layout, hover animation, and footer styles.

**MathJax**: LaTeX rendering is loaded globally via `_includes/footer.html`. Use standard LaTeX delimiters (`$$...$$` for display, `\\(...\\)` for inline) in any page.

**Footer** (`_includes/footer.html`): injects GitHub/LinkedIn links from `_config.yml` fields `github_username` and `linkedin_username`, plus the MathJax CDN script.
