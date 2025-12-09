# Phase 4: Advanced Performance Optimizations

**Priority**: MEDIUM
**Status**: COMPLETED
**Impact**: LCP -300ms, INP -50ms
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
| Priority | MEDIUM |
| Status | Pending |
| Files | 4 |
| Issues | 3 Medium |

---

## Key Insights

1. AVIF format not used - 20-30% smaller than WebP
2. No `<picture>` fallbacks - format negotiation missing
3. Sidebar image not optimized - large LCP candidate
4. KaTeX loads on all pages - should be conditional

---

## Requirements

- AVIF images with WebP/JPEG fallback
- Hero image optimized with preload
- Conditional KaTeX loading
- Responsive image srcset on all images

---

## Implementation Steps

### 4.1 Convert Images to AVIF

```bash
# Install avif tools
brew install libavif  # macOS
# or: apt install libavif-bin  # Ubuntu

# Convert existing WebP to AVIF
cd /Users/sangnguyen/Documents/ngocsangyem.dev/assets/img
find . -name "*.webp" -exec sh -c '
  avifenc -q 60 "$1" "${1%.webp}.avif"
' _ {} \;

# Convert JPEG to AVIF
find . -name "*.jpg" -exec sh -c '
  avifenc -q 60 "$1" "${1%.jpg}.avif"
' _ {} \;
```

**Expected savings**: 20-30% smaller than WebP

### 4.2 Add Picture Element Support

Create custom image include for format fallback:

**File**: `_includes/picture.html`

```liquid
{% assign img_path = include.src | split: '.' %}
{% assign img_base = img_path[0] %}
{% assign img_ext = img_path[1] %}

<picture>
  {% if include.avif != false %}
  <source srcset="{{ img_base }}.avif" type="image/avif">
  {% endif %}
  {% if include.webp != false %}
  <source srcset="{{ img_base }}.webp" type="image/webp">
  {% endif %}
  <img
    src="{{ include.src }}"
    alt="{{ include.alt | default: '' }}"
    width="{{ include.width }}"
    height="{{ include.height }}"
    {% if include.lazy != false %}loading="lazy" decoding="async"{% endif %}
    {% if include.class %}class="{{ include.class }}"{% endif %}
  >
</picture>
```

**Usage in posts**:
```liquid
{% include picture.html
   src="/assets/img/blog/javascript/closure.jpg"
   alt="JavaScript closure diagram"
   width="800"
   height="450"
%}
```

### 4.3 Optimize Sidebar Image

1. Create optimized versions:

```bash
cd /Users/sangnguyen/Documents/ngocsangyem.dev/assets/img

# Create multiple sizes for responsive
convert sidebar-bg.jpg -resize 1920x1080 -quality 80 sidebar-bg-1920.jpg
convert sidebar-bg.jpg -resize 1280x720 -quality 80 sidebar-bg-1280.jpg
convert sidebar-bg.jpg -resize 640x360 -quality 80 sidebar-bg-640.jpg

# Convert to WebP
cwebp -q 80 sidebar-bg-1920.jpg -o sidebar-bg-1920.webp
cwebp -q 80 sidebar-bg-1280.jpg -o sidebar-bg-1280.webp
cwebp -q 80 sidebar-bg-640.jpg -o sidebar-bg-640.webp

# Convert to AVIF
avifenc -q 60 sidebar-bg-1920.jpg sidebar-bg-1920.avif
```

2. Update `_includes/my-head.html` with responsive preload:

```html
<link rel="preload" as="image"
      href="/assets/img/sidebar-bg-1920.avif"
      imagesrcset="/assets/img/sidebar-bg-640.avif 640w,
                   /assets/img/sidebar-bg-1280.avif 1280w,
                   /assets/img/sidebar-bg-1920.avif 1920w"
      imagesizes="100vw"
      type="image/avif">
```

### 4.4 Conditional KaTeX Loading

Only load KaTeX on pages with math content.

**File**: `_includes/my-head.html`

```liquid
{% if page.math == true or page.katex == true %}
<link rel="preload" as="style"
      href="/assets/bower_components/katex/dist/katex.min.css"
      onload="this.onload=null;this.rel='stylesheet'">
<noscript>
  <link rel="stylesheet" href="/assets/bower_components/katex/dist/katex.min.css">
</noscript>
{% endif %}
```

**In posts with math**:
```yaml
---
layout: post
title: Math equations post
math: true  # Enable KaTeX
---
```

---

## Todo List

- [x] Install AVIF tools (libavif) - already available
- [x] Convert WebP images to AVIF (7 images converted)
- [x] Create picture.html include
- [x] Generate sidebar image responsive sizes (640, 1280, 1920)
- [x] Add preload with imagesrcset for AVIF
- [x] Implement conditional KaTeX loading (math: true)
- [ ] Test with Lighthouse (USER ACTION REQUIRED)

---

## Success Criteria

- [ ] AVIF images serve on Chrome/Firefox
- [ ] WebP fallback works on Safari <16
- [ ] Sidebar image <100KB
- [ ] KaTeX not loaded on non-math pages
- [ ] LCP <2.0s

---

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Safari AVIF support | Low | Low | WebP fallback ensures compatibility |
| AVIF build time | Low | Low | One-time conversion |
| Math pages break | Low | Medium | Test pages with math: true |

---

## Next Steps

After completing Phase 4:
1. Run full Lighthouse audit
2. Compare Core Web Vitals metrics
3. Proceed to [Phase 5: Structured Data](phase-05-structured-data.md)
