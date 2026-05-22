# Site Cleanup & Maintainability Plan

## Current State

### Theme & Stack
- **Theme**: `no-style-please` (minimalist, monospace, intentionally unstyled)
- **Jekyll**: 4.4.1 with `jekyll-feed`
- **Custom CSS**: `assets/main.scss` (project cards, figure sizing, footer)

### Layout Hierarchy
```
default.html          ← base HTML shell (head.html + footer.html)
  ├── home.html       ← homepage only; adds <hr> + nav from _data/menu.yml
  └── page.html       ← all inner pages; renders content only (no nav)
```

### Entry Points
| File | Layout | Purpose |
|------|--------|---------|
| `index.markdown` | `home` | Homepage with photo + bio |
| `blog.md` | `page` | Lists all `_blog/` entries as cards |
| `projects.md` | `page` | Lists all `_projects/` entries as cards |
| `_blog/*.md` | `page` | Individual blog/notes posts |
| `_projects/*.md` | `page` | Individual project write-ups |

### Data
- `_data/menu.yml` — manually maintained nav tree (top-level + nested per-item links)

---

## Issues Found

1. **Duplicate/wrong CSS link in `head.html`**  
   Two `<link>` tags: `/assets/css/main.css` (theme output) and `/assets/main.css` (custom SCSS).  
   The custom SCSS front matter triggers Jekyll to compile `assets/main.scss` → `assets/main.css`, so `/assets/main.css` is correct. But both are loaded — verify the theme link is needed and not redundant.

2. **Nav only on homepage**  
   `home.html` includes the nav; `page.html` has none. Inner pages (blog posts, project pages) have no way to get back to the top-level without the browser back button. This is a UX gap.

3. **`menu.yml` is manually maintained and can drift**  
   Adding a new `_blog/` post doesn't automatically appear in nav — it must be added to `_data/menu.yml` separately. The index pages (`blog.md`, `projects.md`) auto-iterate collections, but the sidebar nav does not.

4. **`menu_item.html` is a theme-provided include**  
   `home.html` calls `{% include menu_item.html %}` — this lives inside the gem, not in `_includes/`. Makes it opaque and hard to customize without ejecting the include.

5. **No consistent frontmatter convention**  
   Some files use `layout: page`, some don't declare `date`, `description`, or any metadata beyond `title` and `permalink`. Card listings only show title — no tagline, date, or description available.

---

## Proposed Changes

### 1. Fix the CSS double-load
- Audit which CSS rules come from the theme vs. `main.scss`
- Remove the redundant `<link>` in `head.html` if confirmed duplicate

### 2. Add nav to all pages
- Move the `<hr><nav>` block from `home.html` into `default.html` (or extract to a `_includes/nav.html`)
- This gives every page a consistent nav without duplicating markup
- Keeps `home.html` and `page.html` as thin wrappers

### 3. Simplify top-level nav (drop or flatten `menu.yml`)
- Replace the nested `menu.yml` + `menu_item.html` with a flat, self-contained `_includes/nav.html`:
  ```html
  <nav>
    <a href="/">home</a> /
    <a href="/projects/">projects</a> /
    <a href="/blog/">blog</a>
  </nav>
  ```
- Removes dependency on the theme include and the manually-maintained YAML
- Individual project/blog entries are discoverable via their index pages — no need for per-item nav links

### 4. Standardize frontmatter
Add a consistent set of optional fields to all collection items:
```yaml
---
layout: page
title: "Post Title"
date: YYYY-MM-DD        # for blog posts
description: "One-line summary shown on index cards"
---
```
Then update `blog.md` and `projects.md` cards to show `description` if present.

### 5. Add a `description` to index cards (optional enhancement)
Update the card template in `blog.md` / `projects.md`:
```liquid
<a class="project-card" href="{{ p.url }}">
  <h3>{{ p.title }}</h3>
  {% if p.description %}<p>{{ p.description }}</p>{% endif %}
</a>
```

---

## File Touch Map

| File | Change |
|------|--------|
| `_includes/head.html` | Remove redundant CSS link |
| `_includes/nav.html` | **New** — flat nav include |
| `_layouts/default.html` | Add `{% include nav.html %}` |
| `_layouts/home.html` | Remove inline nav block (now in default) |
| `_data/menu.yml` | Can be deleted or kept for reference |
| `_blog/*.md` | Add `description:` frontmatter |
| `_projects/*.md` | Add `description:` frontmatter |
| `blog.md` / `projects.md` | Show description in cards |
| `assets/main.scss` | Minor cleanup if needed |

---

## Out of Scope (for now)
- Changing the `no-style-please` theme or adding a new theme
- Adding tags, categories, or search
- Pagination for blog/project listings
- Dark/light mode toggle
