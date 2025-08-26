# Content Management

## Blog Post Structure

### Current Post Categories
- **Jekyll** (`_posts/jekyll/`) - Jekyll-related tutorials and tips
- **Vue.js** (`_posts/vue/`) - Vue.js development content
- **HTML** (`_posts/html/`) - HTML techniques and best practices
- **JavaScript** (`_posts/javascript/`) - JavaScript programming content

### Existing Posts
- `2012-02-07-example-content.md` - Example content
- `2017-11-23-example-content-ii.md` - Example content II
- `2018-06-01-example-content-iii.md` - Example content III
- `2020-07-03-introducing-hydejack-9.md` - Hydejack 9 introduction
- `2024-09-08-x-marks-the-spot-in-hydejack-9-2.md` - Latest Hydejack update

### Post Front Matter Template (jekyll-compose)
```yaml
---
layout: post
description: > 
  A short ~160 character description of your post for search engines,
  social media previews, etc.
image:
  path: /assets/img/sidebar-bg.jpg
---
```

## Project Portfolio

### Current Projects
- `_projects/qwtel.md` - Qwtel project
- `_projects/hydejack-site.md` - Hydejack site project

### Project Front Matter Template
```yaml
---
layout: project
description: > 
  A short ~160 character description of your post for search engines,
  social media previews, etc.
image:
  path: /assets/img/sidebar-bg.jpg
links:
  - title: Project Link
    url: https://example.com
---
```

## Resume/CV Management

### Resume Data Structure
- **File**: `_data/resume.yml`
- **Page**: `resume.md`
- **Layout**: Uses structured data for machine-readable format
- **SEO**: Optimized for search engines and social media

## Site Navigation

### Main Menu (configured in _config.yml)
```yaml
menu:
  - title: About
    url: /about/
  - title: Blog
    url: /blog/
  - title: Résumé
    url: /resume/
```

### Commented Out Sections
- Projects menu item (can be enabled)
- Documentation section (can be enabled)

## Content Creation Workflow

### Using Jekyll Compose
```bash
# Create new post
bundle exec jekyll post "New Post Title"

# Create new draft
bundle exec jekyll draft "Draft Title"

# Create new project
bundle exec jekyll project "Project Name"

# Publish draft
bundle exec jekyll publish _drafts/draft-name.md
```

### Manual Content Creation
1. Create file in appropriate directory (`_posts/`, `_projects/`, etc.)
2. Add proper front matter
3. Write content in Markdown
4. Add images to `assets/img/` if needed
5. Test locally with `bundle exec jekyll serve`

## Image Management

### Image Directories
- **Main images**: `assets/img/`
- **Resized images**: `assets/resized/`
- **Author photo**: `/assets/img/author/me/sang.nguyenngoc_w_506.webp`
- **Default sidebar**: `/assets/img/sidebar-bg.jpg`

### Image Best Practices
- Use WebP format for better performance
- Optimize images for web
- Provide descriptive alt text
- Use consistent naming conventions
- Store in logical subdirectories

## SEO and Metadata

### Required Meta Information
- **Title**: Descriptive and keyword-rich
- **Description**: 150-160 characters for search engines
- **Keywords**: Relevant tags and categories
- **Image**: Social media preview image
- **Author**: Sang Nguyen (configured globally)

### Social Media Optimization
- Twitter cards enabled
- Open Graph meta tags
- Structured data for rich snippets
- Proper image dimensions for social sharing