# Development Guidelines

## Design Patterns and Architecture

### Jekyll Site Architecture
- **Static Site Generation**: Content is pre-built into static HTML/CSS/JS
- **Liquid Templating**: Uses Liquid template engine for dynamic content
- **Collection-Based**: Organized around Jekyll collections (posts, projects, pages)
- **Plugin Ecosystem**: Extensible through Jekyll plugins
- **Theme-Based**: Built on Hydejack theme with local customizations

### Content Organization Patterns
- **Category-Based Structure**: Posts organized by technology/topic subdirectories
- **Front Matter Driven**: Content metadata drives layout and functionality
- **Data-Driven Components**: Resume and author info stored in `_data/` files
- **Asset Management**: Images and static files in `assets/` directory

## Code Quality Standards

### Markdown Standards
- Use consistent heading hierarchy (H1 for titles, H2 for sections, etc.)
- Include proper front matter for all content files
- Write descriptive alt text for all images
- Use code fencing with language specification for syntax highlighting

### Sass/CSS Standards
- Follow BEM methodology for CSS class naming
- Use semantic color variables and mixins
- Maintain responsive design principles
- Keep custom styles in designated `_sass/` files

### Performance Guidelines
- Optimize images for web (compress, use appropriate formats)
- Minimize custom CSS and JavaScript
- Leverage Jekyll's built-in optimization features
- Use compressed output for production builds

## Security and Privacy

### Privacy Considerations
- Google Fonts disabled by default for privacy
- Cookie banner available but disabled
- No user tracking without explicit consent
- Social media integration respects privacy

### Content Security
- Validate all external links regularly
- Use HTTPS for all external resources
- Sanitize any user-generated content
- Keep dependencies updated for security patches

## Accessibility Guidelines

### Content Accessibility
- Provide alt text for all images
- Use semantic HTML structure
- Maintain proper heading hierarchy
- Ensure sufficient color contrast

### Navigation Accessibility
- Keyboard navigation support
- Screen reader compatibility
- Clear focus indicators
- Logical tab order

## SEO Best Practices

### Technical SEO
- Use `jekyll-seo-tag` plugin for meta tags
- Generate XML sitemap automatically
- Implement structured data for rich snippets
- Optimize page loading speed

### Content SEO
- Write descriptive, keyword-rich titles
- Create compelling meta descriptions (150-160 characters)
- Use proper heading structure
- Include relevant internal and external links

## Maintenance Guidelines

### Regular Maintenance Tasks
- Update Ruby gems monthly: `bundle update`
- Check for broken links quarterly
- Review and update content for accuracy
- Monitor site performance and loading times

### Backup and Version Control
- Use Git for version control
- Commit frequently with descriptive messages
- Keep production and development branches
- Backup `_data/` files regularly

### Monitoring and Analytics
- Monitor site performance
- Track user engagement (if analytics enabled)
- Review search engine rankings
- Check for 404 errors and broken links

## Deployment Considerations

### Build Process
- Test locally before deploying: `bundle exec jekyll serve`
- Use production environment variables: `JEKYLL_ENV=production`
- Validate HTML and links before deployment
- Check responsive design on multiple devices

### Performance Optimization
- Enable LSI for better related posts: `--lsi` flag
- Use compressed assets in production
- Optimize images before adding to repository
- Minimize plugin usage for faster builds