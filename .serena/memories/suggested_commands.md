# Suggested Development Commands

## Essential Jekyll Commands

### Development Server
```bash
# Install dependencies
bundle install

# Start development server with live reload
bundle exec jekyll serve

# Start with incremental builds (faster)
bundle exec jekyll serve --incremental

# Start with drafts included
bundle exec jekyll serve --drafts
```

### Building for Production
```bash
# Build for production
JEKYLL_ENV=production bundle exec jekyll build

# Build with LSI (Latent Semantic Indexing) for better related posts
JEKYLL_ENV=production bundle exec jekyll build --lsi
```

### Content Creation (jekyll-compose plugin)
```bash
# Create a new post
bundle exec jekyll post "Post Title"

# Create a new draft
bundle exec jekyll draft "Draft Title"

# Create a new project
bundle exec jekyll project "Project Title"

# Publish a draft
bundle exec jekyll publish _drafts/draft-name.md
```

## System Commands (macOS/Darwin)

### File Operations
```bash
# List files and directories
ls -la

# Find files
find . -name "*.md" -type f

# Search in files
grep -r "search_term" .

# Navigate directories
cd path/to/directory
```

### Git Operations
```bash
# Check status
git status

# Add changes
git add .

# Commit changes
git commit -m "commit message"

# Push changes
git push origin main
```

### Ruby/Bundle Management
```bash
# Update gems
bundle update

# Check gem versions
bundle list

# Install specific gem
bundle add gem_name

# Remove gem
bundle remove gem_name
```