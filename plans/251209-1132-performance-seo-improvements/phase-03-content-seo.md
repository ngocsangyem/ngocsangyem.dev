# Phase 3: Content SEO Improvements

**Priority**: HIGH
**Status**: COMPLETED
**Impact**: Search rankings, social sharing
**Completed**: 2025-12-09

---

## Context

- [SEO Review Report](../reports/code-reviewer-251209-seo-implementation-review.md)

---

## Overview

| Item | Value |
|------|-------|
| Date | 2025-12-09 |
| Priority | HIGH |
| Status | Pending |
| Files | 5+ posts |
| Issues | 4 High, 2 Medium |

---

## Key Insights

1. Category mismatches - posts in wrong URL paths
2. Missing Open Graph images - poor social previews
3. Heading hierarchy broken - H3 before H2
4. Inconsistent sitemap metadata

---

## Requirements

- All posts have matching category and folder
- All posts have OG image (1200x630px)
- Proper heading hierarchy (H1→H2→H3)
- Consistent front matter metadata

---

## Posts to Fix

### 3.1 Jekyll Setup Post - Missing Category

**File**: `_posts/jekyll/2022-03-14-set-up-jekyll-environment-on-mac-os.md`

```yaml
# Before
---
layout: post
title: Set up Jekyll environment on macOS
description: Set Ruby, Bundler and Jekyll on macOS Silicon
---

# After
---
layout: post
title: Set up Jekyll environment on macOS
description: >
  Complete guide to setting up Ruby, Bundler and Jekyll on macOS Silicon M1/M2 for local development.
image: /assets/img/blog/jekyll/jekyll-macos-setup.webp
sitemap: true
category: jekyll
tags:
  - jekyll
  - ruby
  - macos
---
```

**Actions**:
1. Add `category: jekyll`
2. Add `image:` with blog post cover
3. Expand description to ~150 chars
4. Add relevant tags
5. Add `sitemap: true`

### 3.2 HTML Post - Wrong Category & Heading

**File**: `_posts/html/2022-03-08-can-a-web-page-contain-multiple-element.md`

```yaml
# Before
---
# ...
category: devlog  # WRONG - should match folder
---

### Answer  # H3 without H2!

# After
---
layout: post
title: Can a web page contain multiple header elements?
description: >
  W3 specification allows multiple header and footer elements in HTML5. Learn when and how to use them correctly.
image: /assets/img/blog/html/multiple-headers.webp
sitemap: true
category: html  # FIXED - matches folder
tags:
  - html
  - w3c
  - semantics
---

## Answer  # FIXED - H2 instead of H3
```

**Actions**:
1. Change `category: devlog` → `category: html`
2. Change `### Answer` → `## Answer`
3. Change `### Additional links` → `## Additional links`
4. Add/update image
5. Expand description

### 3.3 Vue Post - Missing Sitemap

**File**: `_posts/vue/2022-06-19-setup-script-is-the-cool-feature-of-vue-but.md`

```yaml
# Add to front matter
sitemap: true
```

### 3.4 Create Missing Images

Create OG images (1200x630px, WebP) for posts missing them:

```bash
# Use Canva, Figma, or ImageMagick to create:
/assets/img/blog/jekyll/jekyll-macos-setup.webp
/assets/img/blog/html/multiple-headers.webp
```

**Design guidelines**:
- 1200x630px dimension
- WebP format
- Include post title or topic
- Consistent brand colors (accent_color: rgb(79,177,186))

---

## Audit Script

```bash
#!/bin/bash
# Run from project root

echo "=== Posts missing categories ==="
find _posts -name "*.md" -exec sh -c '
  folder=$(dirname "$1" | sed "s|_posts/||")
  if [ "$folder" != "_posts" ]; then
    cat=$(grep -E "^category:" "$1" | head -1 | cut -d: -f2 | tr -d " ")
    if [ -z "$cat" ]; then
      echo "MISSING: $1 (folder: $folder)"
    elif [ "$cat" != "$folder" ]; then
      echo "MISMATCH: $1 (folder: $folder, category: $cat)"
    fi
  fi
' _ {} \;

echo ""
echo "=== Posts missing images ==="
find _posts -name "*.md" -exec grep -L "^image:" {} \;

echo ""
echo "=== Posts missing sitemap ==="
find _posts -name "*.md" -exec grep -L "^sitemap:" {} \;
```

---

## Todo List

- [x] Fix Jekyll post: add category, image, description
- [x] Fix HTML post: change category, fix headings (devlog → html, H3 → H2)
- [x] Fix Vue post: add sitemap, category, fix headings (H3/H5 → H2/H3)
- [x] Create OG images for posts missing them (jekyll-macos-setup.webp, 13KB)
- [x] Run audit script to verify all posts
- [x] Test URLs match expected pattern

---

## Success Criteria

- [ ] All posts have category matching folder
- [ ] All posts have 1200x630px OG image
- [ ] All posts follow H1→H2→H3 hierarchy
- [ ] All posts have sitemap: true
- [ ] Twitter Card validator shows image preview

---

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| URL changes break links | Medium | High | Set up redirects for changed URLs |
| Image creation time | Medium | Low | Use template/batch process |

---

## Next Steps

After completing Phase 3:
1. Verify all posts have consistent metadata
2. Test social sharing with [Open Graph debugger](https://www.opengraph.xyz/)
3. Proceed to [Phase 4: Advanced Performance](phase-04-advanced-performance.md)
