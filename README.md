# ngocsangyem.dev

> Sang Nguyen’s personal portfolio and blog website — a fast, elegant static site powered by Jekyll and the Hydejack theme.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Technology Stack](#technology-stack)
- [Quick Start Guide](#quick-start-guide)
- [Project Structure](#project-structure)
- [Content Creation Guide](#content-creation-guide)
- [Documentation Reference](#documentation-reference)
- [Development Commands](#development-commands)
- [Contributing / Contact](#contributing--contact)

---

## Project Overview
ngocsangyem.dev is the personal portfolio and blog of Sang Nguyen, a frontend developer. The site highlights Sang’s technical skills and experience through project showcases, a résumé page, and an active blog.

The blog features a blend of technical tutorials and lifestyle posts, with a strong focus on HTML, CSS, JavaScript, and Vue.js. Content is organized by topic for easy discovery and is structured to be educational, practical, and readable.

The website is implemented as a static site for optimal performance, security, and SEO. Built with Jekyll 4.3 and the premium Hydejack theme, it ships fast-loading pages, great accessibility, and a delightful reading experience.

---

## Technology Stack
- Jekyll 4.3 (static site generator)
- Hydejack theme (premium Jekyll theme, local copy in `#jekyll-theme-hydejack/`)
- Ruby and Bundler for dependency management
- Key plugins:
  - jekyll-seo-tag
  - jekyll-feed
  - jekyll-sitemap
  - jekyll-include-cache
  - jekyll-last-modified-at
  - jekyll-compose (content helpers)
  - kramdown-math-katex (with KaTeX for math rendering)
- Sass for styling
- KaTeX for math formulas

---

## Quick Start Guide

> Prerequisites: Ruby (>= 2.7 recommended), Bundler, and a working C toolchain for native gems if needed.

```bash
# Install Ruby dependencies
bundle install

# Start development server with live reload
bundle exec jekyll serve

# Access the site
# -> http://localhost:4000
```

Notes
- Jekyll 4.3 requires Ruby 2.7 or newer. Ruby 3.x is recommended for performance.
- If you have multiple Ruby versions installed, consider using a version manager (rbenv, rvm, asdf).

---

## Project Structure
```
.
├── _config.yml            # Main Jekyll configuration and theme settings
├── Gemfile                # Ruby gem dependencies
├── index.md               # Home page
├── about.md               # About page
├── resume.md              # Résumé page (uses _data/resume.yml)
├── posts.md               # Blog index
├── projects.md            # Projects index
├── 404.md                 # Error page
├── offline.md             # Offline/Service Worker support page (optional)
├── forms-by-example.md    # Forms example page
│
├── _posts/                # Blog posts organized by category
│   ├── jekyll/            #   Jekyll-related posts
│   ├── vue/               #   Vue.js posts
│   ├── html/              #   HTML posts
│   └── javascript/        #   JavaScript posts
│
├── _projects/             # Portfolio project pages
│   ├── qwtel.md
│   └── hydejack-site.md
│
├── _data/                 # Site configuration and structured content
│   ├── authors.yml        # Author information
│   ├── resume.yml         # Résumé data
│   ├── social.yml         # Social media links/config
│   ├── variables.yml      # Site variables
│   ├── strings.yml        # Copy and UI strings
│   └── countries.yml      # Country list (used by theme)
│
├── _sass/                 # Custom styling (Sass)
│   ├── my-style.scss
│   └── my-inline.scss
│
├── assets/                # Static assets
│   ├── img/               #   Images
│   └── resized/           #   Pre-resized images
│
├── docs/                  # Comprehensive documentation
│   ├── install.md         #   Setup instructions
│   ├── deploy.md          #   Deployment processes
│   ├── writing.md         #   Content creation guidelines
│   └── build.md           #   Build configuration details
│
└── #jekyll-theme-hydejack/ # Local Hydejack theme and scripts
```

---

## Content Creation Guide

### 1) Create a new blog post (jekyll-compose)
Use the jekyll-compose plugin for consistent front matter:
```bash
# New post (published)
bundle exec jekyll post "Your Post Title"

# New draft (kept in _drafts/)
bundle exec jekyll draft "Exploring Vue 3 Composition API"

# Publish a draft later
bundle exec jekyll publish _drafts/exploring-vue-3-composition-api.md
```

### 2) File naming and placement
- Posts live in `_posts/` with the format: `YYYY-MM-DD-title-with-hyphens.md`
- Organize posts by category using subfolders (e.g., `_posts/vue/2025-02-14-vue-3-basics.md`)
- Projects live in `_projects/` (e.g., `_projects/project-name.md`)

### 3) Required front matter (example)
```yaml
---
layout: post
# title is taken from the first H1 in content by default (jekyll-titles-from-headings)
description: >
  A short ~160 character description for search engines and social previews.
image:
  path: /assets/img/sidebar-bg.jpg
categories: [vue]
tags: [vue, javascript, frontend]
---
```

### 4) Categories, tags, and organization
- Use one primary category (matching the subfolder when possible)
- Add a few relevant tags for discoverability
- Keep descriptions concise (150–160 chars) for SEO

### 5) Images and media
- Store images under `assets/img/` (use descriptive names)
- Prefer modern formats like WebP for performance
- Always include meaningful `alt` text
- Keep file sizes small; optimize before committing

### 6) Local testing checklist
- Build locally and check for warnings:
  ```bash
  bundle exec jekyll serve --incremental
  # or include drafts
  bundle exec jekyll serve --drafts
  ```
- Verify links, images, and code formatting
- Test on mobile sizes and dark mode (Hydejack supports dynamic dark mode)

---

## Documentation Reference
For deeper guidance and edge cases, see:
- docs/install.md — Installation and environment setup
- docs/deploy.md — Deployment processes and recommendations
- docs/writing.md — Content structure, front matter, and style
- docs/build.md — Build configuration, profiling, and options

---

## Development Commands

### Development server
```bash
# Standard dev server (live reload)
bundle exec jekyll serve

# Include drafts in the site
bundle exec jekyll serve --drafts

# Faster rebuilds (incremental)
bundle exec jekyll serve --incremental
```

### Production builds
```bash
# Production build (minified assets, SEO-ready)
JEKYLL_ENV=production bundle exec jekyll build

# Production build with LSI for related posts
JEKYLL_ENV=production bundle exec jekyll build --lsi

# Build with profiling information
bundle exec jekyll build --profile
```

### Content helpers (jekyll-compose)
```bash
# Create content
bundle exec jekyll post "Post Title"
bundle exec jekyll draft "Draft Title"
bundle exec jekyll project "Project Title"

# Publish a draft
bundle exec jekyll publish _drafts/draft-name.md
```

### Validation (optional)
```bash
# Rebuild and inspect output (console warnings)
JEKYLL_ENV=production bundle exec jekyll build --verbose

# If using htmlproofer (optional)
# gem install html-proofer
# htmlproofer ./_site --check-html --check-opengraph --allow-hash-href
```

---

## Contributing / Contact

This is a personal website, but issues and pull requests (PRs) are welcome for fixes, improvements, and documentation updates. Please keep contributions focused, respectful, and aligned with the site’s purpose.

### Before you start
- Check existing issues/PRs to avoid duplicates
- Keep the scope small and focused on one change
- Follow the style and content guidelines in:
  - docs/writing.md (front matter, naming, images, SEO)
  - docs/build.md (build and profiling)
  - docs/install.md (environment setup)

### Reporting an issue
Please include:
- What happened vs. what you expected
- Steps to reproduce (URLs/slugs, links to affected pages)
- Environment (OS, Ruby, Jekyll versions)
- Relevant logs/output (from `bundle exec jekyll build` / `serve`)
- Screenshots or code snippets if helpful

### Submitting a pull request
1. Fork or create a feature branch from the default branch
2. Create a branch with a descriptive name (e.g., `feat/blog-dark-mode-toggle` or `fix/broken-link-about`)
3. Set up locally and validate:
   ```bash
   bundle install
   bundle exec jekyll serve --incremental
   JEKYLL_ENV=production bundle exec jekyll build
   ```
4. Ensure your changes meet these guidelines:
   - Content: correct front matter, file naming `YYYY-MM-DD-title-with-hyphens.md`, categories/tags, alt text, SEO description
   - Styles: test responsiveness and dark mode (Hydejack supports dynamic dark mode)
   - Keep PRs small; update docs if user-facing behavior changes
5. Commit and push:
   ```bash
   git checkout -b feat/scope-short-description
   git add -A
   git commit -m "feat(scope): short description"
   git push origin feat/scope-short-description
   ```
6. Open a PR describing the change, motivation, and any screenshots. Link related issues.

### Code of Conduct
Be kind and constructive. The maintainer may request revisions or decline changes that don’t fit the project goals.

### License
By submitting a contribution, you agree that your changes will be licensed under this repository’s license. See [LICENSE.md](LICENSE.md).

### Contact
- Author: **Sang Nguyen**
- Email: **nnsang24@gmail.com**
- X: **[@ngocsangyem](https://x.com/ngocsangyem)**
- About: [/about](/about/) — Learn more about the author

---

> Built with ❤️ using [Jekyll](https://jekyllrb.com/) and the [Hydejack](https://hydejack.com/) theme.
