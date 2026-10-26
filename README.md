# DJ Dawkins — AI Engineering Portfolio

Personal portfolio hosted at [djdawkins.github.io](https://djdawkins.github.io/).

The site preserves the existing [`devlopr-jekyll`](https://github.com/sujaykundu777/devlopr-jekyll) theme while updating its content for current AI engineering work. Featured material includes Slater, agentic software engineering automation, AI request triage, professional experience, and selected earlier projects.

## Local development

Requirements:

- Ruby version from `.ruby-version`
- Bundler

```bash
bundle install
bundle exec jekyll serve
```

Open `http://127.0.0.1:4000/`.

## Production build

```bash
JEKYLL_ENV=production bundle exec jekyll build
```

The configured output directory is `build/`.

## Content structure

- `_config.yml` — identity, navigation, experience, education, social links, and homepage projects
- `experience.md` — professional history and education
- `projects/` — project index and technical case studies
- `writing/` — completed engineering writing
- `about.md` — entry point for the theme's profile layout
- `assets/img/` — theme and project imagery
- `docs/` — audit, content decisions, and facts requiring review

## Deployment

The production site remains on GitHub Pages. Review changes through a pull request; do not merge or deploy without approval.
