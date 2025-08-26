# Code Style and Conventions

## Jekyll/Markdown Conventions

### Front Matter Structure
```yaml
---
layout: post                    # or 'project', 'about', etc.
title: "Post Title"
description: >
  A short ~160 character description for SEO and social media previews
image:
  path: /assets/img/sidebar-bg.jpg
categories: [category1, category2]
tags: [tag1, tag2]
---
```

### File Naming Conventions
- **Posts**: `YYYY-MM-DD-title-with-hyphens.md` in `_posts/`
- **Projects**: `project-name.md` in `_projects/`
- **Images**: Descriptive names in `assets/img/`
- **Categories**: Use subdirectories in `_posts/` (e.g., `_posts/javascript/`)

### Content Organization
- Use meaningful category subdirectories: `jekyll/`, `vue/`, `html/`, `javascript/`
- Keep post descriptions under 160 characters for SEO
- Use consistent image paths: `/assets/img/sidebar-bg.jpg` as default

## Sass/CSS Conventions

### File Structure
- Custom styles in `_sass/my-style.scss`
- Inline styles in `_sass/my-inline.scss`
- Follow BEM methodology for CSS classes
- Use compressed Sass output for production

### Color Scheme
- **Accent Color**: `rgb(79,177,186)` (teal blue)
- **Theme Color**: `rgb(25,55,71)` (dark blue)
- **Background**: Custom sidebar image at `/assets/img/sidebar-bg.jpg`

## Configuration Conventions

### _config.yml Structure
- Keep personal information in author section
- Use meaningful descriptions for SEO
- Configure plugins in logical order
- Use compressed HTML/CSS for production
- Enable dark mode with dynamic switching

### Data Files (_data/)
- `authors.yml` - Author information and social links
- `resume.yml` - Structured resume data
- `social.yml` - Social media configurations
- `strings.yml` - Site text and translations

## Content Guidelines

### Writing Style
- Technical posts should be educational and practical
- Include code examples with proper syntax highlighting
- Use descriptive headings and subheadings
- Add meta descriptions for all posts

### Image Guidelines
- Use WebP format when possible for performance
- Provide alt text for accessibility
- Optimize images for web (compressed)
- Use consistent aspect ratios

### SEO Best Practices
- Include relevant keywords in titles and descriptions
- Use proper heading hierarchy (H1, H2, H3)
- Add structured data for posts and projects
- Include social media meta tags