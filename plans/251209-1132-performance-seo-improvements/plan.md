# Performance & SEO Improvement Plan

**Project**: ngocsangyem.dev (Jekyll + Hydejack)
**Date**: 2025-12-09
**Status**: Ready for Implementation
**Overall Score**: SEO 7.5/10, Performance 6.5/10 → Target: 9/10

---

## Executive Summary

Jekyll site has solid foundation but 3 critical SEO issues and 4 critical performance issues blocking optimal Core Web Vitals. Key gaps: missing production URL (breaks all meta tags), service worker disabled, no inline critical CSS.

**Projected improvements after all fixes:**
- LCP: 2.8s → 1.0s (-1.8s)
- FCP: 1.6s → 0.5s (-1.1s)
- SEO Score: 7.5/10 → 9/10

---

## Phase Overview

| Phase | Focus | Priority | Impact | Status |
|-------|-------|----------|--------|--------|
| [Phase 1](phase-01-critical-seo-fixes.md) | Critical SEO | CRITICAL | High | **COMPLETED** |
| [Phase 2](phase-02-critical-performance.md) | Core Web Vitals | CRITICAL | High | **COMPLETED** |
| [Phase 3](phase-03-content-seo.md) | Content SEO | HIGH | Medium | **COMPLETED** |
| [Phase 4](phase-04-advanced-performance.md) | Advanced Perf | MEDIUM | Medium | **COMPLETED** |
| [Phase 5](phase-05-structured-data.md) | Structured Data | LOW | Low | **COMPLETED** |

---

## Quick Wins (15 mins)

```yaml
# _config.yml - 3 changes
url: https://ngocsangyem.dev  # Line 6: Uncomment and set

offline:
  enabled: true  # Line 283: Enable service worker
  cache_version: 14  # Increment

google_site_verification: your-code-here  # Line 350: Add after getting from GSC
```

---

## Critical Issues Summary

### SEO (3 Critical)
1. Missing production URL → All meta tags use localhost
2. Category mismatches → URL confusion, broken breadcrumbs
3. Missing Google verification → Cannot submit sitemap

### Performance (4 Critical)
1. Service worker disabled → No caching (+800ms LCP)
2. No inline critical CSS → Blocking render (+600ms FCP)
3. Render-blocking CSS → First paint delayed (+400ms)
4. Missing preconnect hints → External resources slow (+200ms)

---

## Implementation Order

```
Week 1: Phase 1 + Phase 2 (Critical fixes)
Week 2: Phase 3 (Content audit)
Week 3: Phase 4 (Advanced perf)
Week 4: Phase 5 (Structured data) + Testing
```

---

## Files to Modify

| File | Phases | Changes |
|------|--------|---------|
| `_config.yml` | 1,2 | URL, service worker, verification |
| `_sass/my-inline.scss` | 2 | Critical CSS |
| `_includes/my-head.html` | 2,5 | Preload, structured data |
| `_posts/jekyll/*.md` | 3 | Category, image, sitemap |
| `_posts/html/*.md` | 3 | Category, headings |

---

## Validation Checklist

- [ ] No localhost URLs in production build
- [ ] Google Search Console verified
- [ ] Lighthouse score >90 (all metrics)
- [ ] Rich Results Test passes
- [ ] Social preview cards working

---

## Reports

- [SEO Review](../reports/code-reviewer-251209-seo-implementation-review.md)
- [Performance Audit](../reports/code-reviewer-251209-jekyll-performance-audit.md)
- [Jekyll SEO Research](../reports/researcher-251209-jekyll-seo-2024-2025.md)
- [Web Perf Research](../reports/researcher-251209-web-perf-optimization.md)
- [Scout Summary](../reports/scout-251209-jekyll-perf-seo.md)
