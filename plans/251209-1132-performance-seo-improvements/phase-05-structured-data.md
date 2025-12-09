# Phase 5: Structured Data Enhancements

**Priority**: LOW
**Status**: COMPLETED
**Impact**: Rich search results
**Completed**: 2025-12-09

---

## Context

- [SEO Review Report](../reports/code-reviewer-251209-seo-implementation-review.md)
- [Jekyll SEO Research](../reports/researcher-251209-jekyll-seo-2024-2025.md)

---

## Overview

| Item | Value |
|------|-------|
| Date | 2025-12-09 |
| Priority | LOW |
| Status | Pending |
| Files | 2 |
| Issues | 2 Low |

---

## Key Insights

1. Breadcrumb schema missing - no breadcrumb rich results in Google
2. FAQ schema not implemented - opportunity for how-to posts
3. jekyll-seo-tag handles BlogPosting/WebPage well already

---

## Requirements

- BreadcrumbList structured data
- Optional FAQ schema for relevant posts
- Validate with Rich Results Test

---

## Implementation Steps

### 5.1 Add Breadcrumb Schema

**File**: `_includes/breadcrumbs-schema.html`

```liquid
{% if page.url != "/" %}
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": "{{ site.url }}"
    }
    {% assign url_parts = page.url | split: '/' | compact %}
    {% assign position = 2 %}
    {% assign accumulated_path = "" %}
    {% for part in url_parts %}
      {% unless forloop.last %}
        {% assign accumulated_path = accumulated_path | append: '/' | append: part %}
        ,{
          "@type": "ListItem",
          "position": {{ position }},
          "name": "{{ part | capitalize | replace: '-', ' ' }}",
          "item": "{{ site.url }}{{ accumulated_path }}"
        }
        {% assign position = position | plus: 1 %}
      {% endunless %}
    {% endfor %}
    {% if page.title %}
    ,{
      "@type": "ListItem",
      "position": {{ position }},
      "name": "{{ page.title | escape }}"
    }
    {% endif %}
  ]
}
</script>
{% endif %}
```

**Include in head**:

**File**: `_includes/my-head.html`

```liquid
{% include breadcrumbs-schema.html %}
```

### 5.2 Add FAQ Schema for How-To Posts

**File**: `_includes/faq-schema.html`

```liquid
{% if page.faq %}
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {% for item in page.faq %}
    {
      "@type": "Question",
      "name": "{{ item.question | escape }}",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "{{ item.answer | escape }}"
      }
    }{% unless forloop.last %},{% endunless %}
    {% endfor %}
  ]
}
</script>
{% endif %}
```

**Usage in posts**:

```yaml
---
layout: post
title: JavaScript Closures FAQ
faq:
  - question: What is a closure in JavaScript?
    answer: A closure is a function that remembers the variables from its outer scope even after the outer function has finished executing.
  - question: Why are closures useful?
    answer: Closures enable data privacy, function factories, and maintaining state in callbacks.
---
```

### 5.3 Include in Head

**File**: `_includes/my-head.html`

```liquid
<!-- Structured Data -->
{% include breadcrumbs-schema.html %}
{% include faq-schema.html %}
```

---

## Validation

After implementation, validate:

1. **Rich Results Test**: https://search.google.com/test/rich-results
2. **Schema Validator**: https://validator.schema.org/
3. **Google Search Console**: Monitor structured data coverage

---

## Todo List

- [x] Create breadcrumbs-schema.html
- [x] Create faq-schema.html
- [x] Include in my-head.html
- [x] Add FAQ data to relevant posts (javascript-closure.md)
- [ ] Validate with Rich Results Test (USER ACTION REQUIRED)
- [ ] Monitor Search Console for rich results (USER ACTION REQUIRED)

---

## Success Criteria

- [ ] BreadcrumbList schema valid
- [ ] FAQPage schema valid (on FAQ posts)
- [ ] Rich breadcrumbs appear in Google (after indexing)
- [ ] No structured data errors in Search Console

---

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Invalid JSON-LD | Low | Medium | Validate with tools before deploy |
| Liquid escaping issues | Low | Low | Use escape filter |

---

## Next Steps

After completing Phase 5:
1. Final Lighthouse audit
2. Submit to Google Search Console
3. Monitor rich results over 2-4 weeks
4. Document completed improvements
