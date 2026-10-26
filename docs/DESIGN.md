# Portfolio design and architecture decisions

## Decision

Keep Jekyll and preserve the existing `devlopr-jekyll` theme.

The portfolio's familiar hero, project-card presentation, typography, colors, and About layout remain intact. The update changes professional content and adds themed Markdown pages rather than introducing a second visual system or a client framework.

## Information architecture

- **Home:** existing hero and project cards, updated with the current AI Engineer identity and relevant work.
- **Experience:** chronological professional progression and education.
- **Projects:** current case studies plus selected earlier work.
- **Slater:** flagship technical case study covering architecture, orchestration, evaluation, security, evolution, current capability boundaries, and roadmap.
- **Flock Safety case studies:** evidence-safe descriptions of software engineering automation and request triage.
- **Engineering writing:** completed technical material only.
- **About:** existing themed profile layout, updated bio, work history, skills, education, projects, and contact links.

## Professional narrative

DJ Dawkins designs AI-powered applications and workflows as software systems: explicit boundaries, tools, context, evaluation, authorization, failure handling, and operating constraints. Slater provides public technical depth. Flock Safety provides enterprise application context without disclosing proprietary implementation.

## Evidence model

- **Verified:** supplied facts, reviewed resume, public repositories, or Slater audit/code evidence.
- **Reported:** internal outcomes stated in the reviewed resume; measurement details are not public.
- **Planned:** explicitly separated from implemented functionality.
- **Not published:** credentials, internal addresses, camera locations, account details, proprietary source, internal data, and unverified production claims.

## Deployment

The site remains a static Jekyll portfolio hosted at the existing GitHub Pages URL. Pull-request work is reviewed before merge; this branch is not deployed to production.
