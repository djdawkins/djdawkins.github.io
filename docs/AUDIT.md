# Portfolio baseline audit

Audit date: 2026-10-26

## Current state

The repository is a lightly customized 2022-era `devlopr-jekyll` fork. The published site identifies DJ Dawkins as a Data Scientist in Chandler, lists Carter's as the current employer, and presents four early projects as the primary work. The content no longer matches the current AI Engineer role at Flock Safety or the Atlanta metropolitan area.

## Findings

### Content

- The homepage and metadata still use the theme's stock description.
- Current role, AI engineering systems, Slater, evaluation work, and agentic workflows are absent.
- Employer, location, title, and professional narrative are outdated.
- The ClassMate Heroku link is no longer a defensible project reference; no matching public source repository was found.
- Hotel Chatroom and Celebrity Jeopardy have one-line 2020 posts with template SEO keywords. NBA Top Scout has a public repository and remains useful as earlier analytical work.
- The supplied resume link is not visible to the authenticated Drive account used for this audit. A separately accessible Drive resume modified 2026-10-21 was reviewed as supporting evidence; the supplied link remains the public resume destination pending access confirmation.

### Design and accessibility

- The visual system is the stock Bootstrap/theme composition, including a generic hero image and typewriter effect.
- The navigation exposes only Home and About; experience and project depth are buried in one template page.
- Images lack consistent alternative text. Heading structure and repeated IDs in the About layout are invalid or ambiguous.
- The default layouts load unrelated Snipcart, Netlify Identity, Olvy, jQuery, Font Awesome, Bootstrap, and theme scripts.

### Architecture and maintenance

- The repository includes unused ecommerce, gallery, CMS, author, category, newsletter, comments, Firebase, Netlify, Heroku, Docker, Bower, and sample-content paths.
- The Sass bundle is approximately 60 KB before compiled vendor assets; `assets/bower_components` is committed.
- The Gemfile includes Jekyll Admin, pagination, gist, feed, rack/puma, and deploy tooling the portfolio does not need.
- The deployment action uses `actions/checkout@v2`, deprecated `set-output`, and a third-party Jekyll deployment action.
- The README is the upstream theme manual rather than project documentation.

## Evidence reviewed

- Portfolio repository and live site.
- Supplied professional identity and project brief.
- Current accessible Drive resume, modified 2026-10-21.
- Slater Phase 0 V2 baseline audit, living architecture, evolution journal, phase completion reports, capability contracts, deployment and evaluation evidence.
- Public GitHub repositories and current public project metadata.
- Netflix Software Engineer 5 — Agent Platform posting as a competency reference, not a tailoring target.

## Redesign opportunities

1. Lead with the working identity: AI Engineer building reliable intelligent systems beyond prototypes.
2. Make Slater the flagship proof of architecture, orchestration, evaluation, security, and operations.
3. Present Flock Safety work as evidence-safe system case studies: problem, contribution, system shape, controls, result, and confidentiality boundary.
4. Map competencies to concrete decisions and evidence instead of a generic skills cloud.
5. Retain only earlier work that demonstrates trajectory: voice interfaces, applied NLP, and predictive analytics.
6. Replace the template with a small, first-party Jekyll system that GitHub Pages can build without a client framework.
