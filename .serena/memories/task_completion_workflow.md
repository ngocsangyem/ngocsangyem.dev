# Task Completion Workflow

## When a Development Task is Completed

### 1. Code Quality Checks
```bash
# Build the site to check for errors
bundle exec jekyll build

# Check for any build warnings or errors
JEKYLL_ENV=production bundle exec jekyll build --verbose
```

### 2. Content Validation
- **Markdown Syntax**: Ensure proper front matter and markdown formatting
- **Links**: Verify all internal and external links work
- **Images**: Check image paths and alt text
- **SEO**: Validate meta descriptions and titles

### 3. Local Testing
```bash
# Start development server
bundle exec jekyll serve

# Test with drafts if applicable
bundle exec jekyll serve --drafts

# Test incremental builds
bundle exec jekyll serve --incremental
```

### 4. Performance Optimization
```bash
# Build with profiling to check performance
bundle exec jekyll build --profile

# Check for LSI improvements (if applicable)
JEKYLL_ENV=production bundle exec jekyll build --lsi
```

### 5. Git Workflow
```bash
# Check current status
git status

# Add changes
git add .

# Commit with descriptive message
git commit -m "feat: add new blog post about [topic]"
# or
git commit -m "fix: update broken link in about page"
# or
git commit -m "style: improve mobile responsiveness"

# Push to repository
git push origin main
```

### 6. Deployment Verification
- Check that the site builds successfully in production environment
- Verify all new content appears correctly
- Test responsive design on different devices
- Validate SEO meta tags and social media previews

## Quality Assurance Checklist
- [ ] Site builds without errors
- [ ] All links are functional
- [ ] Images load correctly
- [ ] Mobile responsiveness works
- [ ] SEO meta tags are present
- [ ] Social media previews work
- [ ] Performance is acceptable
- [ ] Content is properly formatted
- [ ] Git commit message is descriptive