# Hydejack Theme Specifics

## Theme Configuration

### Local Theme Installation
- Theme is installed locally in `#jekyll-theme-hydejack/` directory
- Uses `theme: jekyll-theme-hydejack` in `_config.yml`
- Alternative remote theme option available but commented out

### Key Hydejack Settings (in _config.yml)
```yaml
hydejack:
  post_addons: [about, newsletter, related, random, comments]
  project_addons: [about, newsletter, other, comments]
  no_mark_external: false
  no_push_state: false
  no_drawer: false
  no_navbar: false
  no_search: false
  no_inline_css: false
  no_page_style: false
  no_break_layout: true
  no_toc: false
  no_third_column: false
  no_large_headings: false
  no_structured_data: false
  no_theme_color: false
  no_breadcrumbs: false
  use_lsi: true
  cookies_banner: false
  advertise: false
  hide_dates: false
  hide_last_modified: false
```

### Dark Mode Configuration
```yaml
dark_mode:
  always: false          # Don't force dark mode
  dynamic: true          # Use OS preference
  icon: true            # Show dark mode toggle
```

### Offline Support (Experimental)
```yaml
offline:
  enabled: false
  cache_version: 13
  precache_assets:
    - /assets/img/swipe.svg
```

## Theme Customization

### Custom Styling
- **Primary custom styles**: `_sass/my-style.scss`
- **Inline styles**: `_sass/my-inline.scss`
- **Accent color**: `rgb(79,177,186)` (teal blue)
- **Theme color**: `rgb(25,55,71)` (dark blue)
- **Sidebar background**: `/assets/img/sidebar-bg.jpg`

### Layout Customizations
- `no_break_layout: true` - Code blocks and tables same width as content
- Dynamic Table of Contents enabled
- Third column enabled for large screens
- Breadcrumbs enabled
- Large headings enabled

### Font Configuration
- Google Fonts disabled by default for privacy
- Uses system fonts instead
- Custom font options available but commented out

## Content Collections

### Configured Collections
```yaml
collections:
  featured_categories:
    permalink: /blog/:name/
    output: true
  featured_tags:
    permalink: /tag-:name/
    output: true
  projects:
    permalink: /projects/:path/
    output: true
```

### Post Configuration
- **Permalink structure**: `/blog/:categories/:year-:month-:day-:title/`
- **Pagination**: 10 posts per page
- **Paginate path**: `/blog/:num/`

## SEO and Social Media

### SEO Configuration
- `jekyll-seo-tag` plugin enabled
- Twitter username: `ngocsangyem`
- Structured data enabled for posts and projects
- Custom meta descriptions for all content types

### Social Media Integration
- Twitter cards enabled
- Facebook Open Graph ready (commented out)
- Social links configured in `_data/social.yml`

## Performance Features

### Optimization Settings
- **Sass compression**: `compressed`
- **HTML compression**: Enabled with clippings
- **Include cache**: Enabled via `jekyll-include-cache`
- **LSI**: Enabled for better related posts
- **Inline CSS**: Enabled for performance

### Build Exclusions
```yaml
exclude:
  - ./#jekyll-theme-hydejack/node_modules
  - ./#jekyll-theme-hydejack/assets
  - ./#jekyll-theme-hydejack/.git
  - .jekyll-cache
  - .sass-cache
  - vendor
  - Gemfile
  - Gemfile.lock
```