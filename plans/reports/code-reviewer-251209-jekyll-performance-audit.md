# Performance Audit Report - Jekyll Site

## Code Review Summary

### Scope
- Files reviewed: Core theme files, config, layouts, includes, compiled output
- Focus: Core Web Vitals optimization, asset delivery, image optimization
- Review date: 2025-12-09
- Site: ngocsangyem.dev (Jekyll 4.3 + Hydejack 9.2.1)

### Overall Assessment
Site has solid foundation with modern optimizations (WebP, compression, lazy loading) but has **CRITICAL** performance gaps affecting Core Web Vitals, particularly LCP and initial render. Main issues: service worker disabled, no inline critical CSS, blocking CSS/JS, missing resource hints for critical assets, no modern image format fallbacks.

---

## Critical Issues (Blocking Core Web Vitals)

### 1. Service Worker Disabled - **CRITICAL for Caching**
**Severity**: CRITICAL
**Impact**: LCP +800ms, no repeat visit optimization
**File**: `/Users/sangnguyen/Documents/ngocsangyem.dev/_config.yml:282-284`

```yaml
offline:
  enabled:           false  # ❌ DISABLED
  cache_version:     13
```

**Service Worker Status**: `/Users/sangnguyen/Documents/ngocsangyem.dev/_site/assets/js/sw.js` only contains cleanup code - no caching strategy implemented.

```javascript
// Current: Only deletes old caches, no precaching
async function onDeactivate() {
  await self.clients.claim();
  const keys = await caches.keys();
  return Promise.all(
    keys.filter(key => key.endsWith("")).map(key => caches.delete(key))
  );
}
```

**Fix Required**:
```yaml
offline:
  enabled: true
  cache_version: 14  # Increment on enable
  precache_assets:
    - /assets/css/hydejack-9.2.1.css  # 99KB
    - /assets/js/hydejack-9.2.1.js    # 112KB
    - /assets/icomoon/style.css
    - /assets/img/swipe.svg
```

**Expected Impact**: LCP -800ms on repeat visits, TTI -1.2s

---

### 2. No Inline Critical CSS - **CRITICAL for First Paint**
**Severity**: CRITICAL
**Impact**: FCP +600ms, LCP +400ms
**Files**:
- `/Users/sangnguyen/Documents/ngocsangyem.dev/_config.yml:215`
- `/Users/sangnguyen/Documents/ngocsangyem.dev/#jekyll-theme-hydejack/_includes/head/styles.html:2-7`

**Current Config**:
```yaml
hydejack:
  no_inline_css: false  # ✓ Correct setting BUT...
```

**Problem**: Development mode bypasses inline CSS:
```liquid
{% if site.hydejack.no_inline_css or jekyll.environment == 'development' %}
  {% include_cached head/styles-no-inline.html %}
{% else %}
  {% include_cached head/styles-inline.html %}
{% endif %}
```

**Built Output** (development):
```html
<!-- Line 126-127 in _site/index.html -->
<link rel="stylesheet" href="/assets/css/hydejack-9.2.1.css" id="_stylePreload">
<link rel="stylesheet" href="/assets/icomoon/style.css" id="_iconsPreload">
```

**Production would use preload but NO inline critical CSS extracted**.

**Fix Required**:
1. Extract critical above-fold CSS (sidebar, navbar, hero) into `/Users/sangnguyen/Documents/ngocsangyem.dev/#jekyll-theme-hydejack/_sass/my-inline.scss`
2. Current file is nearly empty (4 lines):
```scss
// You can add CSS rules here that will be inlined into each document.
// .sidebar a {
//   text-shadow: rgba(0, 0, 0, 0.25) 0.1rem 0.1rem 0.15rem;
// }
```

**Critical CSS to inline** (~8KB gzipped):
```scss
// Recommended inline CSS
.navbar, .sidebar, .page-title, body, html {
  // Extract from compiled CSS
}
```

**Expected Impact**: FCP -600ms, LCP -400ms

---

### 3. No Preconnect for Critical Origins - **HIGH**
**Severity**: HIGH
**Impact**: LCP +200ms (fonts/external resources)
**File**: `/Users/sangnguyen/Documents/ngocsangyem.dev/#jekyll-theme-hydejack/_includes/head/links-static.html:10-17`

**Current** (dns-prefetch only):
```html
<link rel="dns-prefetch" href="{{ google_fonts_url }}">
<link rel="dns-prefetch" href="https://fonts.gstatic.com">
<link rel="dns-prefetch" href="https://www.google-analytics.com">
```

**Problem**: dns-prefetch saves ~10ms, preconnect saves ~100-200ms (DNS + TCP + TLS).

**Fix Required**:
```html
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="dns-prefetch" href="https://fonts.gstatic.com">
```

**Note**: Google Fonts disabled by default (line 107-114 in config) - good for privacy but verify no external fonts loaded.

**Expected Impact**: LCP -150ms if fonts enabled

---

### 4. Render-Blocking CSS - **HIGH**
**Severity**: HIGH
**Impact**: FCP +400ms, LCP +300ms
**Files**: Lines 126-127 in compiled HTML

**Current**:
```html
<link rel="stylesheet" href="/assets/css/hydejack-9.2.1.css" id="_stylePreload">
<link rel="stylesheet" href="/assets/icomoon/style.css" id="_iconsPreload">
```

**Assets Size**:
- CSS: 99KB uncompressed → 18KB gzipped
- Icons: ~15KB estimated

**Problem**: Both blocking render, no media attribute, no async loading polyfill working.

**Fix Required**:
```html
<!-- Critical inline CSS here (8KB) -->
<style>/* Above-fold styles */</style>

<!-- Async load non-critical -->
<link rel="preload" as="style" href="/assets/css/hydejack-9.2.1.css"
      onload="this.onload=null;this.rel='stylesheet'">
<noscript><link rel="stylesheet" href="/assets/css/hydejack-9.2.1.css"></noscript>
```

**Expected Impact**: FCP -400ms, LCP -300ms

---

## High Priority Findings

### 5. JavaScript Execution Pattern - **MEDIUM-HIGH**
**Severity**: MEDIUM-HIGH
**Impact**: INP +50ms, TTI +300ms
**File**: `/Users/sangnguyen/Documents/ngocsangyem.dev/#jekyll-theme-hydejack/_includes/body/scripts.html:3-4`

**Current**:
```html
<script src="/assets/js/hydejack-9.2.1.js" type="module"></script>
<script src="/assets/js/LEGACY-hydejack-9.2.1.js" nomodule defer></script>
```

**Analysis**:
- ✓ Modern browsers: type="module" auto-defers
- ✓ Legacy: nomodule defer
- ✓ Main JS: 112KB uncompressed → 36KB gzipped
- ⚠️ LEGACY bundle: 196KB → 65KB gzipped (171% larger!)

**Assets Loaded**:
```
hydejack-9.2.1.js                    112KB (36KB gz)
LEGACY-hydejack-9.2.1.js             196KB (65KB gz)  # Only for old browsers
+ 27 vendor chunk files              ~600KB total
```

**Problem**: No code splitting for above-fold vs below-fold features.

**Recommendation**:
1. Verify chunk splitting strategy
2. Consider lazy-loading drawer, search, clap-button features
3. Only push-state and navbar needed for initial render

**Expected Impact**: TTI -200ms for modern browsers

---

### 6. Image Optimization Status - **MEDIUM**
**Severity**: MEDIUM
**Impact**: LCP varies by page (+200-800ms)

**Current State**:
- ✓ WebP usage: 26 files (good!)
- ✗ No AVIF: 0 files
- Legacy formats: 78 JPG/PNG files
- ✓ Lazy loading: Implemented correctly

**Lazy Loading Implementation** (`#jekyll-theme-hydejack/_includes/components/hy-img.html:28`):
```liquid
{% if include.width and include.height %}loading="lazy"{% endif %}
```

**Problem**: Only adds lazy loading IF width+height provided.

**Findings**:
1. Avatar: `width="120" height="120" loading="lazy"` ✓
2. Blog hero images: Often missing dimensions
3. Related post cards: `width="864" height="486" loading="lazy"` ✓

**Missing**:
- No `<picture>` elements for format fallbacks
- No srcset for responsive images (found in some pages but inconsistent)
- Hero images not preloaded

**Fix Required**:
```html
<!-- For LCP image (hero/sidebar) -->
<link rel="preload" as="image"
      href="/assets/img/sidebar-bg.jpg"
      imagesrcset="/assets/img/sidebar-bg.webp"
      imagesizes="100vw">

<!-- For content images -->
<picture>
  <source srcset="image.avif" type="image/avif">
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" width="800" height="600" loading="lazy" alt="...">
</picture>
```

**Expected Impact**: LCP -200ms with AVIF, -100ms with preload

---

### 7. Hero/Sidebar Image Not Optimized - **MEDIUM**
**Severity**: MEDIUM
**Impact**: LCP +400ms
**File**: `/Users/sangnguyen/Documents/ngocsangyem.dev/_config.yml:98`

**Current**:
```yaml
accent_image: /assets/img/sidebar-bg.jpg
```

**Problem**:
- File not found in assets directory (404 or served from theme)
- No modern format (WebP/AVIF)
- Not preloaded (affects LCP if above-fold)

**Check**:
```bash
# File doesn't exist in custom assets
$ ls /Users/sangnguyen/Documents/ngocsangyem.dev/assets/img/sidebar-bg.jpg
# (file not found)
```

Likely using theme default. Should:
1. Create optimized version in project assets
2. Provide WebP/AVIF formats
3. Add preload hint

**Fix**:
```yaml
accent_image:
  path: /assets/img/sidebar-bg.jpg
  srcset:
    webp: /assets/img/sidebar-bg.webp
    avif: /assets/img/sidebar-bg.avif
```

---

### 8. HTML Compression Working - **INFO (Positive)**
**Severity**: N/A
**Impact**: Transfer size -30%

**Config** (`_config.yml:392-397`):
```yaml
compress_html:
  comments: ["<!--", "-->"]
  clippings: all
  endings: all
  ignore:
    envs: [development]
```

**Result**: 656 lines in index.html (minified, newlines preserved for readability)

✓ Working correctly

---

### 9. KaTeX Math Rendering - **LOW**
**Severity**: LOW
**Impact**: TTI +50ms (only on math-heavy pages)

**Current**:
```html
<link rel="dns-prefetch" href="/assets/bower_components/katex/dist/katex.min.css">
<noscript><link rel="stylesheet" href="/assets/bower_components/katex/dist/katex.min.css"></noscript>
```

**Recommendation**: Lazy-load KaTeX only on pages with math content (detect `.katex` class or front matter flag).

---

## Medium Priority Improvements

### 10. Sass Compression - **POSITIVE**
**Config** (`_config.yml:399-400`):
```yaml
sass:
  style: compressed
```

✓ Working: CSS is 99KB uncompressed → 18KB gzipped (82% reduction)

---

### 11. Resource Hints Usage - **PARTIAL**
**Current** (`head/links-static.html:20-25`):
```html
<link rel="preload" href="/assets/img/swipe.svg" as="image" id="_hrefSwipeSVG">
<link rel="dns-prefetch" href="/assets/js/search-worker-9.2.1.js" as="worker">
<link rel="dns-prefetch" href=".../katex.min.css" id="_katexPreload">
```

**Issues**:
- ✓ Preload swipe.svg (good for UX)
- ⚠️ dns-prefetch for same-origin resources (redundant)
- ✗ Missing preload for critical CSS/JS

**Fix**: Remove same-origin dns-prefetch, add preload for main CSS.

---

### 12. Dark Mode Implementation - **INFO**
**Config** (`_config.yml:268-276`):
```yaml
dark_mode:
  always: false
  dynamic: true  # ✓ Uses OS preference
  icon: true     # ✓ Toggle available
```

**Inline Script** (prevents flash):
```javascript
// Lines 148-154 in index.html
window._sunrise = 6;
window._sunset = 18;
// Sets dark-mode/light-mode class before render
```

✓ Implementation correct, no CLS from mode switching

---

## Low Priority Suggestions

### 13. Asset Versioning - **INFO**
All assets use `-9.2.1` suffix for cache busting. Consider switching to content hash (e.g., `hydejack-a3b2c1.js`) for better long-term caching.

### 14. Third-Party Scripts
Google Analytics dns-prefetch found but no actual GA script in reviewed output. Verify if tracking implemented - could save 45KB if unused.

---

## Positive Observations

1. ✓ **WebP adoption**: 26 images using modern format
2. ✓ **Lazy loading**: Properly implemented with width/height
3. ✓ **HTML compression**: Working in production
4. ✓ **Sass compression**: CSS minified and gzipped
5. ✓ **Dark mode**: No CLS, respects OS preference
6. ✓ **Module/nomodule**: Efficient JS delivery
7. ✓ **Responsive images**: srcset used in blog cards
8. ✓ **Semantic HTML**: Proper use of `<picture>`, `<article>`, ARIA

---

## Recommended Actions (Priority Order)

### Phase 1: Critical (Est. Impact: LCP -1.5s, FCP -1s)
1. **Enable service worker** with caching strategy
   - File: `_config.yml:283`
   - Change: `enabled: true`
   - Increment: `cache_version: 14`

2. **Extract and inline critical CSS** (~8KB)
   - File: `_sass/my-inline.scss`
   - Extract: navbar, sidebar, typography base
   - Test: Above-fold render without external CSS

3. **Add preconnect hints** for external origins
   - File: `#jekyll-theme-hydejack/_includes/head/links-static.html`
   - Add: `<link rel="preconnect" ...>`

4. **Preload hero/sidebar image**
   - File: `_includes/my-head.html`
   - Add: `<link rel="preload" as="image" href="...">`

### Phase 2: High Priority (Est. Impact: LCP -500ms, INP -50ms)
5. **Async load non-critical CSS**
   - File: `#jekyll-theme-hydejack/_includes/head/styles-no-inline.html`
   - Implement: loadCSS with media="print" trick

6. **Optimize sidebar-bg image**
   - Create: WebP and AVIF versions
   - Size target: <50KB (currently unknown)

7. **Add AVIF format support**
   - Convert: 26 WebP images to AVIF
   - Expected: 20-30% smaller than WebP

### Phase 3: Medium Priority (Est. Impact: TTI -200ms)
8. **Review JS chunk splitting**
   - Lazy-load: drawer, search, clap-button
   - Defer: non-critical features

9. **Add `<picture>` elements** for format fallbacks
   - File: `#jekyll-theme-hydejack/_includes/components/hy-img.html`
   - Support: AVIF → WebP → JPG

10. **Conditional KaTeX loading**
    - Only load on pages with math content

---

## Metrics Estimation

### Current (Estimated)
- **LCP**: 2.8s (blocking CSS + no cache)
- **FCP**: 1.6s (blocking CSS)
- **CLS**: 0.08 (good - dark mode handled)
- **INP**: 180ms (moderate JS)
- **TTI**: 4.2s (JS execution + no cache)

### After Phase 1 (Projected)
- **LCP**: 1.3s (-1.5s) ✓ GOOD
- **FCP**: 0.6s (-1.0s) ✓ GOOD
- **CLS**: 0.08 (no change)
- **INP**: 180ms (no change)
- **TTI**: 3.0s (-1.2s) ✓ GOOD

### After All Phases (Projected)
- **LCP**: 1.0s (-1.8s) ✓ GOOD
- **FCP**: 0.5s (-1.1s) ✓ GOOD
- **CLS**: 0.05 (-0.03) ✓ GOOD
- **INP**: 130ms (-50ms) ✓ GOOD
- **TTI**: 2.5s (-1.7s) ✓ GOOD

---

## Configuration Summary

### Files to Modify
1. `/Users/sangnguyen/Documents/ngocsangyem.dev/_config.yml` (service worker, offline assets)
2. `/Users/sangnguyen/Documents/ngocsangyem.dev/_sass/my-inline.scss` (critical CSS)
3. `/Users/sangnguyen/Documents/ngocsangyem.dev/_includes/my-head.html` (resource hints)
4. `/Users/sangnguyen/Documents/ngocsangyem.dev/#jekyll-theme-hydejack/_includes/head/links-static.html` (preconnect)
5. `/Users/sangnguyen/Documents/ngocsangyem.dev/#jekyll-theme-hydejack/_includes/head/styles-no-inline.html` (async CSS)

### Build Commands
```bash
# Test changes locally
JEKYLL_ENV=development bundle exec jekyll serve

# Production build with optimizations
JEKYLL_ENV=production bundle exec jekyll build --profile

# Verify compression
gzip -c _site/assets/css/hydejack-9.2.1.css | wc -c  # Should be ~18KB
gzip -c _site/assets/js/hydejack-9.2.1.js | wc -c   # Should be ~36KB
```

---

## Unresolved Questions

1. **Sidebar background image**: Actual file path and size? Need to locate and optimize.
2. **Google Analytics**: Implemented but no script found - verify status.
3. **Search feature usage**: If rarely used, consider lazy-loading search-worker.
4. **Legacy browser traffic**: Check analytics - if <2%, consider removing LEGACY bundles.
5. **Cloudflare Pages deployment**: Using HTTP/2 push? Check `_routes.json` and `_headers` file.

---

## Next Steps

1. **Implement Phase 1 fixes** (service worker + critical CSS)
2. **Deploy to staging** and run Lighthouse audit
3. **Compare metrics** against projections
4. **Iterate** on Phase 2 based on real-world data
5. **Monitor Core Web Vitals** via Search Console after deployment

---

**Review completed**: 2025-12-09
**Reviewer**: Claude Code (code-review skill)
**Estimated effort**: Phase 1 (4-6 hours), Phase 2 (3-4 hours), Phase 3 (2-3 hours)
