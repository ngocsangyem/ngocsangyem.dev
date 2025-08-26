# Codebase Structure

## Root Directory Layout
```
├── _config.yml              # Main Jekyll configuration
├── Gemfile                  # Ruby dependencies
├── Gemfile.lock            # Locked dependency versions
├── index.md                # Homepage
├── about.md                # About page
├── resume.md               # Resume page
├── posts.md                # Blog posts index
├── projects.md             # Projects index
├── 404.md                  # Error page
├── offline.md              # Offline page
└── forms-by-example.md     # Forms example page
```

## Content Directories
```
├── _posts/                 # Blog posts
│   ├── jekyll/            # Jekyll-related posts
│   ├── vue/               # Vue.js posts
│   ├── html/              # HTML posts
│   └── javascript/        # JavaScript posts
├── _projects/             # Project portfolio items
├── _drafts/               # Draft posts
├── _featured_categories/  # Category pages
└── blog/                  # Blog layout files
```

## Configuration & Data
```
├── _data/                 # Site data files
│   ├── authors.yml        # Author information
│   ├── resume.yml         # Resume data
│   ├── social.yml         # Social media links
│   ├── strings.yml        # Site strings/translations
│   ├── variables.yml      # Site variables
│   └── countries.yml      # Country data
└── _includes/             # Reusable template parts
```

## Styling & Assets
```
├── _sass/                 # Custom Sass files
│   ├── my-style.scss      # Main custom styles
│   └── my-inline.scss     # Inline styles
├── assets/                # Static assets
│   ├── img/               # Images
│   └── resized/           # Resized images
└── #jekyll-theme-hydejack/ # Theme files (local)
```

## Development & Deployment
```
├── .github/               # GitHub workflows
│   └── workflows/         # CI/CD configurations
├── .vscode/               # VS Code settings
├── .idea/                 # IntelliJ IDEA settings
├── .serena/               # Serena configuration
├── docs/                  # Documentation
└── licenses/              # License files
```

## Key Configuration Files
- `_config.yml` - Main site configuration, theme settings, plugins
- `Gemfile` - Ruby gem dependencies
- `.gitignore` - Git ignore patterns
- `LICENSE.md` - Site license
- `CHANGELOG.md` - Version history