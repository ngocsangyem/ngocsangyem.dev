# Jekyll Performance & SEO Scout Report
**Date**: 2025-12-09  
**Project**: ngocsangyem.dev (Jekyll + Hydejack)  
**Focus**: Files impacting performance and SEO

---

## CONFIGURATION FILES

### Main Configuration
- **`/Users/sangnguyen/Documents/ngocsangyem.dev/_config.yml`**
  - Central Jekyll configuration for site metadata, theme settings, and plugin configurations
  - Contains SEO keywords, author info, social media handles (Twitter)
  - HTML compression enabled via `compress_html` settings
  - Sass compilation set to `compressed` style for production
  - Jekyll plugins configured: jekyll-seo-tag, jekyll-feed, jekyll-sitemap, jekyll-include-cache
  - Dark mode configuration with dynamic CSS theme switching
  - Service worker cache versioning (v13) for offline support

---

## HEAD SECTION & META TAGS

### Primary Head Includes (Theme)
- **`#jekyll-theme-hydejack/_includes/head/index.html`**
  - Main head orchestrator that loads all meta, styles, and scripts

- **`#jekyll-theme-hydejack/_includes/head/meta.html`**
  - Conditional robots meta tags (noindex support)
  - jekyll-seo-tag plugin integration
  - Keywords meta tag generation
  - Color scheme meta tags for dark mode support
  - Theme color meta tag for browser UI

- **`#jekyll-theme-hydejack/_includes/head/seo-tag.html`**
  - Calls jekyll-seo-tag plugin for automatic meta generation
  - Handles OpenGraph tags and Twitter cards (configured via _config.yml)

- **`#jekyll-theme-hydejack/_includes/head/meta-static.html`**
  - Static meta tags setup

- **`#jekyll-theme-hydejack/_includes/head/seo-fallback.html`**
  - Fallback SEO implementation if jekyll-seo-tag unavailable

### Custom Head Overrides
- **`/Users/sangnguyen/Documents/ngocsangyem.dev/_includes/my-head.html`**
  - Empty custom head hook for site-specific additions
  - **Status**: Currently unused, ready for customization

- **`#jekyll-theme-hydejack/_includes/my-head.html`**
  - CloudFlare email protection integration for SPA nav
  - Matomo analytics tracking hook (commented example)

---

## STYLES & CSS OPTIMIZATION

### Inline CSS Strategy
- **`#jekyll-theme-hydejack/_includes/head/styles.html`**
  - Conditionally inlines critical CSS vs defers full CSS
  - No inline CSS mode available via `no_inline_css` config

- **`#jekyll-theme-hydejack/_includes/head/styles-inline.html`**
  - Contains inlined critical path CSS
  - Preloads primary styles and icon fonts with `rel="preload"`
  - Implements font-display=swap for better performance

- **`#jekyll-theme-hydejack/_includes/head/styles-layout.html`**
  - Layout-specific inline styles

- **`#jekyll-theme-hydejack/_includes/head/styles-no-inline.html`**
  - Alternative for full CSS linking (no inlining)

### Custom Sass
- **`/Users/sangnguyen/Documents/ngocsangyem.dev/_sass/my-style.scss`**
  - Custom styling for download tables and buttons
  - Minimal content (14 lines)

- **`/Users/sangnguyen/Documents/ngocsangyem.dev/_sass/my-inline.scss`**
  - Custom inline CSS hooks (currently empty with template comments)

- **`#jekyll-theme-hydejack/_sass/` (extensive)**
  - Theme SASS modules organized by layout type:
    - `hydejack/__inline__/` - Critical path CSS
    - `hydejack/__link__/` - Deferred CSS
    - `pooleparty/` - Base theme styles
    - `pro/` - Premium feature styles including dark mode

---

## JAVASCRIPT & PERFORMANCE

### Head Scripts
- **`#jekyll-theme-hydejack/_includes/head/scripts.html`**
  - Loads JS loaders (`load-js.min.js`, `loadCSS.min.js`, `cssrelpreload.min.js`)
  - Initializes window config object with performance flags
  - Conditional MathJax loading (async if configured)
  - Defers sitedata.json loading for search functionality

### Body Scripts
- **`#jekyll-theme-hydejack/_includes/body/scripts.html`**
  - Main app initialization and dynamic features

### Custom Script Hooks
- **`/Users/sangnguyen/Documents/ngocsangyem.dev/_includes/my-body.html`**
  - Contains CloudFlare email protection for SPA page transitions
  - Hooks into Hydejack's `hy-push-state-after` events

---

## SERVICE WORKER & OFFLINE SUPPORT

### Service Worker Files
- **`#jekyll-theme-hydejack/_includes/js/service-worker.js`**
  - Core SW implementation (100+ lines of advanced caching)
  - Handles offline functionality and asset caching

- **`#jekyll-theme-hydejack/assets/js/service-worker.js`**
  - Generated JS output of above

- **`#jekyll-theme-hydejack/assets/js/sw.js`**
  - Alternative SW entry point

### SW Configuration
- **`/Users/sangnguyen/Documents/ngocsangyem.dev/offline.md`**
  - Offline page that SW serves when disconnected
  - Marked with `sitemap: false` to exclude from indexes

- **`_config.yml` offline section**:
  ```yaml
  offline:
    enabled: false  # Currently disabled
    cache_version: 13
    precache_assets:
      - /assets/img/swipe.svg
  ```

---

## ASSET HANDLING

### Image Assets
Directory: `/Users/sangnguyen/Documents/ngocsangyem.dev/assets/img/`

**Responsive Images with WebP Format**:
- `author/me/sang.nguyenngoc_w_*.webp` - Multiple widths (128-1400px)
- `blog/javascript/jun_2022/*.webp` - WebP format async step images
- `blog/html/*.jpg` - Responsive HTML tutorial images with multiple widths
- All blog images have responsive variants

**Pre-resized Assets**:
- `/Users/sangnguyen/Documents/ngocsangyem.dev/_site/assets/resized/` - Auto-generated responsive image variants
- Multiple breakpoints per image (320px, 481px, 769px, 1025px, 1201px, 1400px)

**Performance Optimizations**:
- Modern WebP format used (better compression than JPG/PNG)
- Multiple responsive variants for responsive images
- PNG/JPG backups for legacy support

---

## SEO-SPECIFIC FILES

### Sitemap & Feeds
- **`_site/sitemap.xml`** (generated by jekyll-sitemap plugin)
  - Auto-generated XML sitemap for search engines

- **`_site/robots.txt`** (generated)
  - Auto-generated robots file (basic configuration)

- **`_site/feed.xml`** (generated by jekyll-feed plugin)
  - RSS/Atom feed for content distribution

### Configuration for SEO
- **`_config.yml` SEO section**:
  ```yaml
  # Plugins for SEO
  plugins:
    - jekyll-seo-tag       # Meta tag generation
    - jekyll-sitemap       # XML sitemap
    - jekyll-feed          # RSS feed
    - jekyll-last-modified-at  # Last modified dates
  
  # Social metadata
  twitter:
    username: ngocsangyem
  
  # Keywords
  keywords: ["Frontend", "HTML", "Javascript", "Life style", "CSS", "Vuejs", "Travel"]
  
  # Logo for social sharing
  logo: /assets/img/author/me/sang.nguyenngoc_w_506.webp
  ```

### Structured Data
- **`_config.yml` structured data settings**:
  ```yaml
  hydejack:
    no_structured_data: false  # Enables JSON-LD output
    # Post types automatically set to BlogPosting
    # Projects/Pages can override to WebPage
  ```

- **`#jekyll-theme-hydejack/_layouts/project.html`**
  - Supports structured data with `seo.type: WebPage`

- **`#jekyll-theme-hydejack/_layouts/resume.html`**
  - Resume data can include structured markup

---

## PERFORMANCE FEATURES

### HTML Compression
- **`_config.yml` compress_html section**:
  ```yaml
  compress_html:
    comments: ["<!--", "-->"]
    clippings: all  # Remove extra whitespace
    endings: all    # Remove closing tags where safe
    ignore:
      envs: [development]  # Skip in dev for easier debugging
  ```

### CSS Minification
- **`_config.yml` sass section**:
  ```yaml
  sass:
    style: compressed  # Minified CSS output
  ```

### CSS Inlining & Critical Path
- **Theme performance config** (`no_inline_css`, `no_page_style`)
  - Inline critical CSS by default
  - Per-page accent colors inlined
  - Option to disable for faster builds

### Caching & Cache Busting
- **`_config.yml` defaults**:
  ```yaml
  - scope: assets/
    values: sitemap: false  # Don't index asset files
  ```

- **Service Worker cache versioning** (v13)
- **Search index cache busting** via timestamp

### Jekyll Include Cache Plugin
- **`jekyll-include-cache` plugin**
  - Caches included partials to speed up builds
  - Significant performance improvement for large sites

### Image Resizing
- Pre-resized image variants stored in `/assets/resized/`
- Hydejack theme handles responsive image generation

---

## LAYOUT & HTML STRUCTURE

### Main Layouts
- **`#jekyll-theme-hydejack/_layouts/compress.html`**
  - Base layout with HTML compression (saves ~30% overhead)

- **`#jekyll-theme-hydejack/_layouts/base.html`**
  - Core HTML structure

- **`#jekyll-theme-hydejack/_layouts/default.html`**
  - Default page layout with sidebar

- **`#jekyll-theme-hydejack/_layouts/post.html`**
  - Blog post layout with metadata support

- **`#jekyll-theme-hydejack/_layouts/page.html`**
  - Static page layout

- **`#jekyll-theme-hydejack/_layouts/home.html`**
  - Landing page optimized layout

### Component Includes
- **`#jekyll-theme-hydejack/_includes/components/post.html`**
  - Post display component with SEO metadata

- **`#jekyll-theme-hydejack/_includes/components/post-list-item.html`**
  - Summary list items for post feeds

---

## LINK & RESOURCE OPTIMIZATION

### Link Tags
- **`#jekyll-theme-hydejack/_includes/head/links.html`**
  - `hreflang` alternate link for language targeting
  - Supports internationalization SEO

- **`#jekyll-theme-hydejack/_includes/head/links-static.html`**
  - Static link declarations

### Preload Strategy
- **`head/styles-inline.html` uses**:
  ```html
  <link rel="preload" as="style" href="..." id="_stylePreload">
  ```
  - Preloads CSS with dynamic link switching via JS

- **Font loading with `display=swap`**
  - Better Core Web Vitals performance
  - Prevents font loading delays

---

## THEME CUSTOMIZATION STRUCTURE

### Override Capability
- **`_includes/my-head.html`** - Custom head content
- **`_includes/my-body.html`** - Custom body scripts
- **`_sass/my-style.scss`** - Custom styles
- **`_sass/my-inline.scss`** - Custom inline styles

### Theme Hooks
- **`_layouts/`** - Can override any theme layout
- **`_sass/my-variables.scss`** - Override theme variables

---

## BUILD & DEPLOYMENT

### Build Profile
- **Development builds**: Standard incremental builds
- **Production builds**: 
  ```bash
  JEKYLL_ENV=production bundle exec jekyll build
  ```
  - Enables search indexing
  - Activates HTML/CSS compression

### LSI (Latent Semantic Indexing)
- **`_config.yml` use_lsi: true**
- Generate related posts recommendations via:
  ```bash
  JEKYLL_ENV=production bundle exec jekyll build --lsi
  ```

---

## PLUGIN STACK FOR PERFORMANCE/SEO

| Plugin | Purpose | Performance Impact |
|--------|---------|-------------------|
| `jekyll-seo-tag` | Auto meta generation | Positive (structured data) |
| `jekyll-sitemap` | XML sitemap generation | Positive (SEO) |
| `jekyll-feed` | RSS feed generation | Positive (distribution) |
| `jekyll-include-cache` | Partial caching | Positive (build speed) |
| `jekyll-last-modified-at` | Track modifications | Positive (freshness signals) |
| `jekyll-optional-front-matter` | Simplify pages | Neutral |
| `jekyll-titles-from-headings` | Auto title extraction | Neutral |

---

## DATA FILES (SEO METADATA)

### `/Users/sangnguyen/Documents/ngocsangyem.dev/_data/`
- **`authors.yml`** - Author info used by jekyll-seo-tag
- **`resume.yml`** - Structured resume data
- **`social.yml`** - Social media links
- **`variables.yml`** - Site-wide variables
- **`strings.yml`** - UI copy and labels
- **`countries.yml`** - Country list support

---

## ACCESSIBILITY & DARK MODE

### Dark Mode Performance
- **`_config.yml` dark_mode settings**:
  ```yaml
  dark_mode:
    always: false
    dynamic: true  # OS preference detection
    icon: true     # Manual toggle available
  ```

- **`#jekyll-theme-hydejack/_sass/pro/_dark-mode.scss`**
  - CSS custom properties for theme switching
  - No layout shift on mode change

- **`#jekyll-theme-hydejack/_includes/pro/dark-mode-fix.html`**
  - Prevents flash of unstyled content

### Color Scheme Meta Tags
- **`head/meta.html` includes**:
  ```html
  <meta name="color-scheme" content="dark light">
  ```
  - Helps browser render dark mode quicker

---

## RECOMMENDATIONS FOR FURTHER OPTIMIZATION

### High Priority
1. **Enable Service Worker** - `offline.enabled: true` in _config.yml for cache-first strategy
2. **Generate SEO verification tokens** - Add Google/Bing webmaster verification to _config.yml
3. **Implement JSON-LD breadcrumbs** - Manually add in custom layouts for better SERP display

### Medium Priority
1. **Add Core Web Vitals monitoring** - Include performance tracking script
2. **Optimize image lazy loading** - Add `loading="lazy"` to image includes
3. **Cache headers configuration** - Set up .htaccess or server config for cache-control headers
4. **AMP setup** (optional) - Consider if mobile traffic is priority

### Low Priority
1. **Implement sitemap index** - If content grows significantly
2. **Add rel=canonical** - Already handled by jekyll-seo-tag but verify per page
3. **Enable BROTLI compression** - Server-side (above Jekyll level)

---

## UNRESOLVED QUESTIONS

1. **Are custom robots.txt rules needed?** - Currently auto-generated, may need customization
2. **Is Google Analytics enabled?** - Not found in current config (matomo hook exists)
3. **Are Open Graph images configured per-post?** - Check individual post front matter
4. **Is HTTP/2 server push configured?** - Handled by hosting platform (not Jekyll)
5. **Should Service Worker be enabled?** - Currently disabled, assess user cache needs

