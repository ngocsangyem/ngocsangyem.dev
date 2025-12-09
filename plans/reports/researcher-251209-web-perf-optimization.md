# Web Performance Optimization for Static Sites: 2024-2025 Research

## Executive Summary
Static sites can achieve best-in-class performance by optimizing Core Web Vitals, assets, images, caching, and resource hints. Key goal: 75th percentile of users experience LCP <2.5s, INP <200ms, CLS <0.1.

---

## 1. Core Web Vitals Optimization

**LCP (Largest Contentful Paint) - Target: <2.5s**
- Serve compressed images (WebP/AVIF preferred)
- Implement CDN with edge caching
- Defer non-critical scripts asynchronously
- Use code splitting; minimize critical CSS
- Avoid render-blocking resources

**INP (Interaction to Next Paint) - Target: <200ms**
- Eliminate long-running JS tasks (>50ms)
- Reduce third-party script overhead
- Minimize DOM size; update only visible elements
- Use event delegation for lightweight handlers
- Lazy-load non-essential components

**CLS (Cumulative Layout Shift) - Target: <0.1**
- Always specify image/video width & height
- Use `transform` & `opacity` for animations (avoid width/height changes)
- Reserve space for embeds, ads, fonts before load
- Prevent unsized iframes; use aspect-ratio CSS

---

## 2. Asset Optimization

**Minification & Bundling**
- Minify CSS (cssnano/csso), JS (esbuild/Terser), HTML (HTMLMinifier)
- Use bundlers: esbuild (fastest static sites), Webpack (with code splitting)
- Production only; keep source maps for debugging

**Code Splitting**
- Split vendor dependencies into separate chunks
- Lazy-load heavy libraries (client-side only)
- Separate critical CSS for initial paint

---

## 3. Image Optimization

**Format Strategy (2024-2025)**
- Primary: AVIF (60% smaller than JPEG; Chrome, Firefox, Edge)
- Fallback: WebP (25-34% smaller than JPEG; broad support)
- Fallback: JPEG/PNG (for <2% legacy traffic)
- Use CDN/build tools for automatic conversion

**Responsive Images**
- Use `srcset` with density descriptors (e.g., `1x, 2x`)
- Use `sizes` attribute for layout breakpoints
- Use `<picture>` element for format negotiation

**Lazy Loading**
- Add `loading="lazy"` to below-fold images
- Never lazy-load LCP images (above fold)
- Consider native support (99%+ modern browsers)

---

## 4. Caching Strategies

**Static Assets (CSS, JS, Images)**
- Use versioning/fingerprinting: cache forever with `Cache-Control: public, max-age=31536000, immutable`
- Target >90% cache hit rate at CDN edge

**HTML & Dynamic Content**
- Short TTL: `max-age=300, stale-while-revalidate=86400`
- Let stale versions serve while origin updates in background

**CDN Best Practices**
- Deploy static sites to CDN (Cloudflare, Vercel, Netlify)
- Set Cache-Level to "Cache Everything" for static dirs
- Use custom cache keys to improve hit ratio
- Enable gzip/Brotli compression at edge

**Cache Invalidation**
- Fingerprint assets with hashes (app.abc123.js)
- Use ETags + Last-Modified headers
- Implement purge API if content changes

---

## 5. Resource Hints

**Preload**
- Only critical 2-3 assets (hero image, essential font, main CSS)
- Example: `<link rel="preload" as="image" href="hero.jpg">`
- Reduces LCP for critical resources

**Preconnect**
- Establish DNS + TCP + TLS for external origins ahead of time
- Example: `<link rel="preconnect" href="https://fonts.gstatic.com">`
- Best for: CDN, analytics, font servers
- Caveat: costs ~3KB per connection; use sparingly (1-2 max)

**Prefetch**
- Low-priority resources for next navigation (Safari lacks support)
- Use when user flow is predictable
- Note: Not recommended for static sites targeting broad audiences

**Font Optimization (Critical)**
- Preconnect to font delivery origins
- Always include `crossorigin` attribute on preload to avoid double fetch
- Use `font-display: swap` to avoid FOIT/FOUT
- Example: `<link rel="preload" as="font" href="font.woff2" type="font/woff2" crossorigin>`
- Limits: preload only 1-2 fonts; avoid 10+ resource hints

---

## 6. Implementation Checklist

**Must-Have**
- [ ] Minify CSS/JS for production
- [ ] Serve AVIF + WebP with JPEG fallback
- [ ] Add `loading="lazy"` to below-fold images
- [ ] Specify width/height on all images
- [ ] Use CDN with long TTL for versioned assets
- [ ] Preload critical font with crossorigin
- [ ] Preconnect to font service domain

**Should-Have**
- [ ] Implement srcset for responsive images
- [ ] Enable Brotli compression at CDN
- [ ] Use transforms for animations (not layout properties)
- [ ] Reserve space for iframes with aspect-ratio CSS
- [ ] Lazy-load non-critical JS

**Nice-to-Have**
- [ ] Code split large JS bundles
- [ ] DNS-prefetch for 3rd-party analytics
- [ ] Implement stale-while-revalidate headers
- [ ] Monitor with Web Vitals API + CrUX

---

## Key Metrics (2024-2025)

- **75th percentile threshold** used by Google to determine Core Web Vitals "pass"
- **INP replaced FID** in March 2024; ~600K sites moved from pass to fail initially
- **AVIF adoption:** Chrome, Firefox, Edge; Safari support improving
- **Static site advantage:** No origin processing = instant CDN hits + minimal latency

---

## Tools & Resources

**Measurement:**
- [Chrome DevTools](https://developer.chrome.com/docs/devtools/)
- [PageSpeed Insights](https://pagespeed.web.dev/)
- Google Search Console Core Web Vitals report
- [Web Vitals JS Library](https://github.com/GoogleChrome/web-vitals)

**Optimization:**
- Bundlers: esbuild, Webpack
- Image tools: Optimole, Smush, or CDN native conversion
- Analytics: Vercel Analytics, Netlify Analytics

---

## Sources

1. [Core Web Vitals Optimization 2024-2025](https://nitropack.io/blog/post/core-web-vitals-strategy)
2. [Google Search Central: Core Web Vitals](https://developers.google.com/search/docs/appearance/core-web-vitals)
3. [Image Optimization Guide 2025](https://requestmetrics.com/web-performance/high-performance-images/)
4. [AVIF vs WebP 2025](https://elementor.com/blog/webp-vs-avif/)
5. [CDN Caching Best Practices](https://blog.blazingcdn.com/en-us/caching-static-and-dynamic-content-how-does-it-work-in-2024)
6. [Resource Hints Performance](https://nitropack.io/blog/post/resource-hints-performance-optimization)
7. [Web.dev: Resource Hints](https://web.dev/learn/performance/resource-hints)
8. [Static Asset Bundling](https://www.sitepoint.com/bundle-static-site-webpack/)

---

**Last Updated:** 2025-12-09
**Status:** Ready for Implementation
