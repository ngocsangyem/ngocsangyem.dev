# Contributing to ngocsangyem.dev

Thanks for your interest in improving this project! This repository powers a personal portfolio and blog. All respectful, focused contributions are welcome — especially fixes, content improvements, and documentation updates.

## Table of Contents
- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Submitting a Bug Report](#submitting-a-bug-report)
- [Proposing Enhancements](#proposing-enhancements)
- [Submitting a Pull Request](#submitting-a-pull-request)
- [Style and Content Guidelines](#style-and-content-guidelines)
- [License](#license)
- [Contact](#contact)

## Code of Conduct
Be kind and constructive. The maintainer may request revisions or decline changes that don’t fit the project’s goals.

## How Can I Contribute?
- Report bugs and broken links
- Fix typos and content issues
- Improve documentation (README, docs/*)
- Suggest small enhancements to layout or styles
- Add or improve tests/validation steps in docs

## Submitting a Bug Report
Please include the following details:
- What happened vs. what you expected
- Steps to reproduce (URLs/slugs, links to affected pages)
- Environment (OS, Ruby, Jekyll versions)
- Relevant output/logs (from `bundle exec jekyll build` / `serve`)
- Screenshots or snippets if helpful

## Proposing Enhancements
- Explain the motivation and scope
- Consider alternatives and trade-offs
- Keep changes focused and incremental
- Link to related issues or discussions

## Submitting a Pull Request
1. Fork the repository or create a feature branch
2. Create a descriptive branch name, e.g. `feat/blog-dark-mode-toggle` or `fix/about-broken-link`
3. Set up and validate locally:
   ```bash
   bundle install
   bundle exec jekyll serve --incremental
   JEKYLL_ENV=production bundle exec jekyll build
   ```
4. Ensure your changes meet these guidelines:
   - Content: correct front matter, file naming `YYYY-MM-DD-title-with-hyphens.md`, categories/tags, alt text, SEO description
   - Styles: test responsiveness and dark mode
   - Keep PRs small and focused; update docs if behavior changes
5. Commit and push:
   ```bash
   git checkout -b feat/scope-short-description
   git add -A
   git commit -m "feat(scope): short description"
   git push origin feat/scope-short-description
   ```
6. Open a PR describing the change, motivation, and screenshots if applicable. Link any related issues.

## Style and Content Guidelines
- Follow the conventions in `docs/writing.md` and `docs/build.md`
- Prefer WebP images, include descriptive alt text
- Keep descriptions to ~160 characters for SEO
- Use proper heading hierarchy and code fences with language identifiers

## License
By contributing, you agree your contributions will be licensed under this repository’s license. See [LICENSE.md](LICENSE.md).

## Contact
- Author: Sang Nguyen — <nnsang24@gmail.com>
- X: [@ngocsangyem](https://x.com/ngocsangyem)
- About: /about

