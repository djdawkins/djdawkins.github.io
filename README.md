# DJ Dawkins — AI Engineering Portfolio

Source for [djdawkins.github.io](https://djdawkins.github.io/).

A small Jekyll site presenting evidence-backed AI engineering case studies, professional experience, and technical writing. The redesign intentionally avoids a client framework, analytics, remote fonts, and the previous theme's unused ecommerce/CMS dependencies.

## Architecture

- Jekyll 4 with Markdown pages
- Reusable layouts and includes in `_layouts/` and `_includes/`
- One first-party stylesheet and a small mobile-navigation script
- SVG architecture diagrams committed as static assets
- GitHub Actions build and GitHub Pages deployment

See [`docs/AUDIT.md`](docs/AUDIT.md) for the baseline audit, [`docs/DESIGN.md`](docs/DESIGN.md) for design decisions, and [`docs/REVIEW_NOTES.md`](docs/REVIEW_NOTES.md) for facts to confirm before merge.

## Local development

Prerequisites: Ruby 3.3 and Bundler.

```bash
bundle install
bundle exec jekyll serve --livereload
```

Open <http://127.0.0.1:4000/>.

## Verification

```bash
JEKYLL_ENV=production bundle exec jekyll build
bundle exec htmlproofer ./_site --disable-external --no-enforce-https
```

The pull-request workflow runs both commands. It does **not** deploy pull requests. Deployment occurs only after a reviewed change reaches `master`.

## Content accuracy

- Slater claims trace to the Phase 0 V2 architecture audit and supporting reports in the private project repository.
- Professional case studies stay at an architecture level and omit proprietary source, internal data, and confidential workflow details.
- Reported outcome metrics come from the current reviewed resume and are labeled with their measurement boundary.
- Planned Slater capabilities are explicitly separated from implemented behavior.

## Editing

1. Update Markdown content or the reusable layout/include.
2. Keep meaningful claims tied to a reviewed source.
3. Never add credentials, internal addresses, camera locations, account information, enterprise data, or private source excerpts.
4. Run the production build and generated-HTML check.
5. Verify the rendered desktop and mobile surfaces before opening a pull request.
