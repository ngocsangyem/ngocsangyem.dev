This project is a Jekyll-based personal blog and portfolio. Here is a more detailed breakdown of the project structure:

*   **`/` (Root Directory)**
    *   `_config.yml`: Main Jekyll configuration file. Contains site-wide settings like title, author, theme, plugins, etc.
    *   `Gemfile`: Defines the project's Ruby dependencies (gems), managed by Bundler.
    *   `index.md`: The home page of the site.
    *   `about.md`: The about page.
    *   `resume.md`: The resume page.
    *   `posts.md`: A page that likely lists all blog posts.
    *   `projects.md`: A page that lists projects.

*   **`_posts/`**: Contains all the blog posts as Markdown files.
    *   `YYYY-MM-DD-post-title.md`: Individual blog posts.
    *   `html/`: Posts related to HTML.
    *   `javascript/`: Posts related to JavaScript.
    *   `jekyll/`: Posts related to Jekyll.
    *   `vue/`: Posts related to Vue.js.

*   **`_data/`**: Contains data files used by the site.
    *   `authors.yml`: Information about the site's author(s).
    *   `social.yml`: Social media links and icons.
    *   `resume.yml`: Data for the resume page.
    *   `strings.yml`: Reusable strings for the theme.
    *   `variables.yml`: Custom variables.

*   **`_sass/`**: Contains custom Sass/SCSS files for styling.
    *   `my-inline.scss`: Inline styles.
    *   `my-style.scss`: Main custom stylesheet.

*   **`assets/`**: Contains all static assets.
    *   `img/`: Images used in the blog posts and pages.
    *   `resized/`: Resized images for responsive design.

*   **`#jekyll-theme-hydejack/`**: Contains the Hydejack theme files. This is a submodule or a local copy of the theme.
    *   `_layouts/`: HTML layouts for different types of pages (e.g., `post.html`, `page.html`).
    *   `_includes/`: Reusable HTML snippets.
    *   `_sass/`: The theme's Sass files.
    *   `_js/`: The theme's JavaScript files.
    *   `assets/`: The theme's static assets.

*   **`docs/`**: Contains the documentation for the Hydejack theme.

*   **`.github/`**: Contains GitHub-related files.
    *   `workflows/`: GitHub Actions workflows (e.g., for CI/CD).

*   **`.serena/`**: Contains files related to the Serena CLI agent.
    *   `memories/`: Stores the memory files created during onboarding.
