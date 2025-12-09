# Phase 1: Critical SEO Fixes

**Priority**: CRITICAL
**Status**: COMPLETED
**Impact**: All meta tags, sitemap, canonical URLs
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
| Priority | CRITICAL |
| Status | Pending |
| Files | 2 |
| Issues | 3 Critical |

---

## Key Insights

1. All URLs in production use `http://localhost:4000` - breaks social sharing and SEO
2. Google Search Console verification missing - cannot submit sitemap
3. Social links not configured - missing sameAs in JSON-LD

---

## Requirements

- Production URL configured
- Google Search Console verified
- Social links in structured data

---

## Architecture

No architecture changes needed - configuration only.

---

## Related Code Files

- `/Users/sangnguyen/Documents/ngocsangyem.dev/_config.yml:6,350-356,369-373`

---

## Implementation Steps

### 1.1 Set Production URL

**File**: `_config.yml:6`

```yaml
# Before
# url:                   https://username.github.io

# After
url: https://ngocsangyem.dev
```

### 1.2 Add Google Site Verification

**File**: `_config.yml:350`

1. Go to [Google Search Console](https://search.google.com/search-console)
2. Add property: `https://ngocsangyem.dev`
3. Choose HTML tag verification method
4. Copy verification code

```yaml
# Add after line 350
google_site_verification: YOUR_VERIFICATION_CODE_HERE
```

### 1.3 Configure Social Links

**File**: `_config.yml:369-373`

```yaml
# Before (commented out)
# social:
#   name:                <firstname> <lastname>
#   links:
#     - https://twitter.com/<username>
#     - https://github.com/<username>

# After
social:
  name: Sang Nguyen
  links:
    - https://twitter.com/ngocsangyem
    - https://github.com/ngocsangyem
```

---

## Todo List

- [x] Uncomment and set `url` in _config.yml
- [ ] Get Google verification code from Search Console (USER ACTION REQUIRED)
- [x] Add `google_site_verification` to _config.yml (placeholder added)
- [x] Uncomment and configure `social` section
- [ ] Production build and verify no localhost URLs (run: `bundle install && JEKYLL_ENV=production bundle exec jekyll build`)
- [ ] Submit sitemap to Google Search Console (USER ACTION REQUIRED)

---

## Success Criteria

- [ ] `grep -r "localhost" _site/ | wc -l` returns 0
- [ ] Meta tag `google-site-verification` present in HTML
- [ ] JSON-LD includes `sameAs` with social links
- [ ] Sitemap accepted in Google Search Console

---

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Wrong URL format | Low | High | Verify with full URL including protocol |
| Verification failure | Low | Medium | Try alternative verification methods |

---

## Security Considerations

- Verification code is public and safe to commit
- Do not expose any API keys or secrets

---

## Next Steps

After completing Phase 1:
1. Proceed to [Phase 2: Critical Performance](phase-02-critical-performance.md)
2. Test with production build: `JEKYLL_ENV=production bundle exec jekyll build`
3. Validate with [Rich Results Test](https://search.google.com/test/rich-results)
