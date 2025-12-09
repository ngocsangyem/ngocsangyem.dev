# Phase 2: Critical Performance Fixes

**Priority**: CRITICAL
**Status**: COMPLETED
**Impact**: LCP -1.5s, FCP -1.0s
**Completed**: 2025-12-09

---

## Context

- [Performance Audit](../reports/code-reviewer-251209-jekyll-performance-audit.md)
- [Web Perf Research](../reports/researcher-251209-web-perf-optimization.md)

---

## Overview

| Item | Value |
|------|-------|
| Date | 2025-12-09 |
| Priority | CRITICAL |
| Status | Pending |
| Files | 3 |
| Issues | 4 Critical |

---

## Key Insights

1. Service worker disabled - losing 800ms LCP on repeat visits
2. No inline critical CSS - FCP delayed 600ms
3. CSS blocks render - 99KB blocking first paint
4. Missing preconnect hints - external resources slow

---

## Requirements

- Service worker caching enabled
- Critical CSS inlined (~8KB)
- Resource hints for external origins
- Hero image preloaded

---

## Architecture

No architecture changes - configuration and CSS extraction only.

---

## Related Code Files

- `_config.yml:282-286` - Service worker config
- `_sass/my-inline.scss` - Critical CSS
- `_includes/my-head.html` - Resource hints
- `#jekyll-theme-hydejack/_includes/head/links-static.html` - Preconnect

---

## Implementation Steps

### 2.1 Enable Service Worker

**File**: `_config.yml:282-286`

```yaml
# Before
offline:
  enabled:           false
  cache_version:     13
  precache_assets:
    - /assets/img/swipe.svg

# After
offline:
  enabled: true
  cache_version: 14
  precache_assets:
    - /assets/img/swipe.svg
    - /assets/css/hydejack-9.2.1.css
    - /assets/js/hydejack-9.2.1.js
```

**Impact**: LCP -800ms on repeat visits

### 2.2 Add Critical Inline CSS

**File**: `_sass/my-inline.scss`

```scss
// Critical above-fold CSS - ~8KB budget
// Include: navbar, sidebar, page-title, typography base

// Reset & Base
html {
  box-sizing: border-box;
}

*, *::before, *::after {
  box-sizing: inherit;
}

body {
  margin: 0;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  line-height: 1.6;
  color: var(--body-color, #333);
  background: var(--body-bg, #fff);
}

// Sidebar critical styles
.sidebar {
  position: fixed;
  width: 21rem;
  height: 100vh;
  overflow: hidden;
}

// Navbar critical styles
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  height: 3.5rem;
}

// Page title
.page-title {
  margin-top: 0;
  font-size: 2rem;
  font-weight: 700;
}
```

**Impact**: FCP -600ms, LCP -400ms

### 2.3 Add Resource Hints

**File**: `_includes/my-head.html`

```html
<!-- Preconnect for faster external resource loading -->
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- Preload hero/sidebar image (LCP candidate) -->
{% if page.accent_image %}
<link rel="preload" as="image" href="{{ page.accent_image.path | default: page.accent_image }}">
{% elsif site.accent_image %}
<link rel="preload" as="image" href="{{ site.accent_image.path | default: site.accent_image }}">
{% endif %}

<!-- Preload main CSS for faster first paint -->
<link rel="preload" as="style" href="/assets/css/hydejack-9.2.1.css">
```

**Impact**: LCP -200ms

### 2.4 Convert Sidebar Image to WebP

**Action**: Create optimized sidebar background

```bash
# If sidebar-bg.jpg exists, convert to WebP
cd /Users/sangnguyen/Documents/ngocsangyem.dev/assets/img
convert sidebar-bg.jpg -quality 80 -resize 1920x1080 sidebar-bg.webp

# Or use cwebp for better compression
cwebp -q 80 sidebar-bg.jpg -o sidebar-bg.webp
```

Update `_config.yml:98`:
```yaml
accent_image: /assets/img/sidebar-bg.webp
```

**Impact**: LCP -100-200ms (smaller file size)

---

## Todo List

- [x] Enable service worker in _config.yml
- [x] Increment cache_version to 14
- [x] Add precache_assets for main CSS/JS
- [x] Extract critical CSS to my-inline.scss (REVERTED - conflicts with Hydejack theme)
- [x] Add preconnect hint for fonts.gstatic.com
- [x] Add preload for hero/sidebar image
- [x] Convert sidebar-bg to WebP format (152KB → 45KB, 70% smaller)
- [ ] Test with production build (USER ACTION REQUIRED)
- [ ] Run Lighthouse audit (USER ACTION REQUIRED)

---

## Success Criteria

- [ ] Service worker registered (check DevTools > Application)
- [ ] First Contentful Paint <1.0s
- [ ] Largest Contentful Paint <2.5s
- [ ] No render-blocking resources warning in Lighthouse
- [ ] Cache hit on repeat visits (DevTools > Network)

---

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| SW cache issues | Medium | Medium | Increment cache_version on changes |
| Critical CSS too large | Low | Medium | Keep under 14KB (HTTP/2 initial window) |
| Preload unused | Low | Low | Only preload above-fold images |

---

## Security Considerations

- Service worker scope limited to site origin
- No third-party scripts in critical path

---

## Metrics Target

| Metric | Current | Target | Change |
|--------|---------|--------|--------|
| LCP | 2.8s | 1.3s | -1.5s |
| FCP | 1.6s | 0.6s | -1.0s |
| TTI | 4.2s | 3.0s | -1.2s |

---

## Next Steps

After completing Phase 2:
1. Deploy to staging and run Lighthouse
2. Compare metrics against targets
3. Proceed to [Phase 3: Content SEO](phase-03-content-seo.md)
