# Jekyll Performance & SEO Files - Complete Index
**Generated**: 2025-12-09

---

## CONFIGURATION & METADATA

| File Path | Purpose | Impact |
|-----------|---------|--------|
| `/Users/sangnguyen/Documents/ngocsangyem.dev/_config.yml` | Main Jekyll config, SEO settings, plugin configuration | HIGH - Controls all site behavior |
| `/Users/sangnguyen/Documents/ngocsangyem.dev/offline.md` | Offline page for service worker | MEDIUM - UX when offline |

---

## HEAD & SEO INCLUDES (Theme: #jekyll-theme-hydejack/)

### Head Meta Tags
| File Path | Purpose | Impact |
|-----------|---------|--------|
| `_includes/head/index.html` | Head orchestrator, loads all meta/styles/scripts | HIGH - All page metadata |
| `_includes/head/meta.html` | robots, keywords, theme-color, color-scheme meta tags | HIGH - SEO signals |
| `_includes/head/meta-static.html` | Static meta tag setup | MEDIUM |
| `_includes/head/seo-tag.html` | Calls jekyll-seo-tag plugin for OG/Twitter cards | HIGH - Social sharing |
| `_includes/head/seo-fallback.html` | Fallback SEO if jekyll-seo-tag unavailable | LOW - Fallback only |

### Head Links & Preloading
| File Path | Purpose | Impact |
|-----------|---------|--------|
| `_includes/head/links.html` | hreflang alternate links, language SEO | MEDIUM - International SEO |
| `_includes/head/links-static.html` | Static link declarations | LOW |
| `_includes/head/feed-tag.html` | RSS feed link generation | MEDIUM - Distribution |

### Head Scripts
| File Path | Purpose | Impact |
|-----------|---------|--------|
| `_includes/head/scripts.html` | JS loaders, window config, MathJax async loading | HIGH - Core Web Vitals |

### Head Styles & CSS
| File Path | Purpose | Impact |
|-----------|---------|--------|
| `_includes/head/styles.html` | Inline vs defer CSS strategy logic | HIGH - Performance |
| `_includes/head/styles-inline.html` | Critical path CSS, preload with `display=swap` | HIGH - FCP, FID |
| `_includes/head/styles-layout.html` | Layout-specific inline styles | MEDIUM |
| `_includes/head/styles-no-inline.html` | Full CSS linking (no inlining) alternative | MEDIUM - Build speed |
| `_includes/head/page-style.html` | Per-page accent color inlining | MEDIUM |

---

## CUSTOM SITE OVERRIDES

### Head & Body Hooks
| File Path | Purpose | Impact |
|-----------|---------|--------|
| `/Users/sangnguyen/Documents/ngocsangyem.dev/_includes/my-head.html` | Custom head content hook (currently empty) | LOW - Ready for use |
| `/Users/sangnguyen/Documents/ngocsangyem.dev/_includes/my-body.html` | CloudFlare email protection + analytics hooks | HIGH - SPAccess compatibility |

### Custom Styles (Sass)
| File Path | Purpose | Impact |
|-----------|---------|--------|
| `/Users/sangnguyen/Documents/ngocsangyem.dev/_sass/my-style.scss` | Custom component styles (14 lines) | LOW |
| `/Users/sangnguyen/Documents/ngocsangyem.dev/_sass/my-inline.scss` | Custom inline CSS hooks (empty) | LOW |

---

## THEME LAYOUTS (Impact on Page Structure & SEO)

| File Path | Purpose | Impact |
|-----------|---------|--------|
| `#jekyll-theme-hydejack/_layouts/compress.html` | HTML compression wrapper (saves ~30%) | HIGH - Page size |
| `#jekyll-theme-hydejack/_layouts/base.html` | Core HTML structure | HIGH - Markup foundation |
| `#jekyll-theme-hydejack/_layouts/default.html` | Default page with sidebar | MEDIUM - Standard pages |
| `#jekyll-theme-hydejack/_layouts/post.html` | Blog post layout with metadata | HIGH - Blog SEO |
| `#jekyll-theme-hydejack/_layouts/page.html` | Static page layout | MEDIUM |
| `#jekyll-theme-hydejack/_layouts/home.html` | Landing page optimized layout | HIGH - First impression |
| `#jekyll-theme-hydejack/_layouts/project.html` | Project showcase with structured data | HIGH - Portfolio SEO |
| `#jekyll-theme-hydejack/_layouts/resume.html` | Resume with structured data support | MEDIUM |
| `#jekyll-theme-hydejack/_layouts/blog.html` | Blog listing layout | MEDIUM - Pagination |
| `#jekyll-theme-hydejack/_layouts/grid.html` | Grid layout for projects | MEDIUM |
| `#jekyll-theme-hydejack/_layouts/list.html` | Generic list layout | MEDIUM |
| `#jekyll-theme-hydejack/_layouts/about.html` | About page layout | LOW |
| `#jekyll-theme-hydejack/_layouts/not-found.html` | 404 error page | LOW |
| `#jekyll-theme-hydejack/_layouts/offline.html` | Offline page layout | LOW |
| `#jekyll-theme-hydejack/_layouts/plain.html` | Plain/minimal layout | LOW |
| `#jekyll-theme-hydejack/_layouts/welcome.html` | Welcome/onboarding layout | MEDIUM |
| `#jekyll-theme-hydejack/_layouts/redirect.html` | Redirect handler | MEDIUM |

---

## THEME COMPONENTS (Content Display)

| File Path | Purpose | Impact |
|-----------|---------|--------|
| `_includes/components/post.html` | Single post render with metadata | HIGH - Content presentation |
| `_includes/components/post-list-item.html` | Post list item for archives/feeds | HIGH - Discoverability |
| `_includes/components/message.html` | Callout/message component | LOW |
| `_includes/components/from-to.html` | Date range component (resume) | LOW |

---

## THEME STYLING (SCSS/CSS)

### Critical Path Styles
| File Path | Purpose | Impact |
|-----------|---------|--------|
| `_sass/hydejack/__inline__/_base.scss` | Critical HTML element styles | HIGH - FCP |
| `_sass/hydejack/__inline__/_avatar.scss` | Avatar critical styles | MEDIUM |
| `_sass/hydejack/__inline__/_content.scss` | Content critical styles | HIGH - Readability |
| `_sass/hydejack/__inline__/_footer.scss` | Footer critical styles | LOW |
| `_sass/hydejack/__inline__/_images.scss` | Image critical styles | MEDIUM |
| `_sass/hydejack/__inline__/_links.scss` | Link critical styles | MEDIUM |
| `_sass/hydejack/__inline__/_sidebar.scss` | Sidebar critical styles | MEDIUM |
| `_sass/hydejack/__inline__/_mark-external.scss` | External link markers | LOW |
| `_sass/hydejack/__inline__/_menu.scss` | Menu critical styles | MEDIUM |
| `_sass/hydejack/__inline__/_social.scss` | Social links critical | LOW |
| `_sass/hydejack/__inline__/_toc.scss` | Table of contents critical | MEDIUM |
| `_sass/hydejack/__inline__/_utilities.scss` | Utility critical styles | LOW |

### Deferred Styles
| File Path | Purpose | Impact |
|-----------|---------|--------|
| `_sass/hydejack/__link__/` | Non-critical stylesheet versions | MEDIUM - Async loading |
| `_sass/pooleparty/` | Theme base styles | HIGH - Overall appearance |
| `_sass/pro/` | Premium features (dark mode, search, etc) | HIGH - Feature styles |
| `_sass/pro/_dark-mode.scss` | Dark mode CSS variables | HIGH - Dark mode performance |
| `_sass/pro/_dark-mode-dynamic.scss` | Dynamic dark mode toggle | MEDIUM |
| `_sass/pro/_dark-mode-dynamic-syntax.scss` | Code syntax dark mode | LOW |
| `_sass/pro/_search.scss` | Search feature styles | MEDIUM |
| `_sass/pro/_resume.scss` | Resume page styling | LOW |

### Variables & Utilities
| File Path | Purpose | Impact |
|-----------|---------|--------|
| `_sass/_variables.scss` | Theme color/size variables | HIGH - Customization |
| `_sass/_mixins.scss` | Reusable SCSS mixins | MEDIUM - Code organization |
| `_sass/html.scss` | Root HTML styles | MEDIUM |

---

## JAVASCRIPT (Theme)

### Performance & Loading
| File Path | Purpose | Impact |
|-----------|---------|--------|
| `_includes/js/service-worker.js` | Service worker caching logic | HIGH - Offline/cache |
| `assets/js/service-worker.js` | Generated SW (from above) | HIGH |
| `assets/js/sw.js` | Alternative SW entry point | HIGH |
| `_includes/js/scripts/load-js.min.js` | Minified async JS loader | HIGH - Non-blocking JS |
| `_includes/js/scripts/loadCSS.min.js` | CSS loading utility | HIGH - Non-blocking CSS |
| `_includes/js/scripts/cssrelpreload.min.js` | CSS preload polyfill | HIGH - Browser compat |

### Body Scripts
| File Path | Purpose | Impact |
|-----------|---------|--------|
| `_includes/body/scripts.html` | Main app initialization | HIGH - Interactivity |
| `_includes/body/analytics.html` | Analytics integration hook | MEDIUM - Tracking |
| `_includes/body/comments.html` | Comments section | LOW |

---

## ASSET DIRECTORIES & IMAGES

| Directory | Purpose | Performance Note |
|-----------|---------|------------------|
| `/Users/sangnguyen/Documents/ngocsangyem.dev/assets/img/` | All image assets | Performance-critical |
| `assets/img/author/me/` | Profile images (WebP, multiple widths) | HIGH - Responsive |
| `assets/img/blog/` | Blog post images (mixed formats) | HIGH - Content visual |
| `assets/img/blog/javascript/jun_2022/` | JS tutorial WebP images | HIGH - Visual content |
| `assets/img/blog/html/` | HTML tutorial responsive JPGs | HIGH |
| `assets/img/blog/vue/` | Vue tutorial images | MEDIUM |
| `assets/img/projects/` | Project showcase images | MEDIUM |
| `assets/img/docs/` | Documentation screenshots | LOW |
| `/Users/sangnguyen/Documents/ngocsangyem.dev/_site/assets/resized/` | Auto-generated responsive variants | HIGH - Responsive images |

### Image Format Strategy
- **WebP**: Modern format for async/tutorial images
- **JPG**: Fallback for responsive images
- **PNG**: Icons/diagrams

---

## SEO & DISCOVERABILITY (Generated)

| File Path | Purpose | Impact |
|-----------|---------|--------|
| `_site/sitemap.xml` | XML sitemap (auto-generated by jekyll-sitemap) | HIGH - Crawlability |
| `_site/robots.txt` | Robots directives (auto-generated) | HIGH - Crawl instructions |
| `_site/feed.xml` | RSS/Atom feed (jekyll-feed plugin) | MEDIUM - Distribution |
| `_site/assets/sitedata.json` | Site search index (deferred load) | MEDIUM - Search |

---

## DATA FILES (Site Metadata)

| File Path | Purpose | Impact |
|-----------|---------|--------|
| `/Users/sangnguyen/Documents/ngocsangyem.dev/_data/authors.yml` | Author info for jekyll-seo-tag | HIGH - Author markup |
| `/Users/sangnguyen/Documents/ngocsangyem.dev/_data/resume.yml` | Structured resume data | MEDIUM - Structured data |
| `/Users/sangnguyen/Documents/ngocsangyem.dev/_data/social.yml` | Social media links | MEDIUM - Social sharing |
| `/Users/sangnguyen/Documents/ngocsangyem.dev/_data/variables.yml` | Site-wide configuration variables | MEDIUM |
| `/Users/sangnguyen/Documents/ngocsangyem.dev/_data/strings.yml` | UI copy and labels | LOW |
| `/Users/sangnguyen/Documents/ngocsangyem.dev/_data/countries.yml` | Country list helper | LOW |

---

## ACCESSIBILITY & DARK MODE (Theme)

| File Path | Purpose | Impact |
|-----------|---------|--------|
| `_includes/pro/dark-mode-fix.html` | FOUC prevention for dark mode | MEDIUM - User experience |
| `_sass/pro/_dark-mode.scss` | Dark mode CSS variables | HIGH - Theme switching |
| `_sass/pro/_dark-mode-dynamic.scss` | Dynamic mode toggle styles | MEDIUM |
| `_sass/pro/_dark-mode-dynamic-syntax.scss` | Code syntax dark mode | LOW |

---

## BUILD CONFIGURATION SUMMARY

**Compression**:
- HTML: via `compress_html` plugin
- CSS: `sass.style: compressed`
- JS: Minified by theme

**Caching**:
- Include cache: `jekyll-include-cache` plugin
- Service Worker: v13 (disabled by default)
- Assets excluded from sitemap

**SEO Plugins**:
- `jekyll-seo-tag` - Meta/OG/Twitter cards
- `jekyll-sitemap` - XML sitemap
- `jekyll-feed` - RSS feed
- `jekyll-last-modified-at` - Modification dates

**Other Performance Plugins**:
- `jekyll-include-cache` - Build speed
- `jekyll-optional-front-matter` - Flexible content
- `jekyll-titles-from-headings` - Auto titles

---

## FILE COUNT SUMMARY

| Category | Count | Notes |
|----------|-------|-------|
| Config files | 2 | _config.yml + offline.md |
| Head includes | 9 | Meta, scripts, styles, links |
| Layout templates | 18 | Various page types |
| Component includes | 4+ | Post display, lists, messages |
| SCSS files | 80+ | Theme + custom styles |
| JavaScript files | 6 | SW + loaders + body scripts |
| Image assets | 150+ | With responsive variants |
| Data files | 6 | Authors, resume, social, etc |
| Generated SEO files | 3 | sitemap.xml, robots.txt, feed.xml |
| **TOTAL** | **~280+** | Includes theme & generated files |

---

## KEY PERFORMANCE LEVERS

### High-Impact Items (Optimize First)
1. **CSS Inlining** - `_includes/head/styles.html` + `styles-inline.html`
2. **Image Optimization** - `assets/img/` (WebP + responsive variants)
3. **JavaScript Defer** - `_includes/head/scripts.html`
4. **Service Worker** - Toggle `offline.enabled` in `_config.yml`
5. **HTML Compression** - Already enabled in `_config.yml`

### Medium-Impact Items
1. **Dark Mode** - CSS custom properties in `pro/_dark-mode.scss`
2. **Sitemap** - Auto-generated, monitor coverage
3. **Feed** - RSS distribution via `jekyll-feed`
4. **Include Cache** - Already enabled plugin

### Low-Impact / Monitoring
1. **Robots.txt** - Review for custom rules
2. **Breadcrumbs** - Consider adding JSON-LD
3. **Verification** - Add Google/Bing tokens to `_config.yml`
4. **Analytics** - Hook available in `_includes/my-body.html`

