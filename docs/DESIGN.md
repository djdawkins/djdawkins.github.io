# Portfolio design and architecture decisions

## Decision

Keep Jekyll, replace the theme.

Jekyll remains the smallest architecture that preserves reusable layouts, includes, data-driven project cards, Markdown case studies, and first-class GitHub Pages support. A React/Vite or other client framework would add JavaScript, dependencies, hydration concerns, and a custom build for a content site that needs none of them.

## Information architecture

- **Home:** identity, specialties, featured systems, current role, evidence snapshot, contact actions.
- **Experience:** chronological professional progression and education.
- **Projects:** featured case studies plus a deliberately secondary Earlier Work section.
- **Slater:** flagship technical case study with architecture, request flow, evolution, evaluation, security, current capability boundary, limitations, and roadmap.
- **Flock Safety case studies:** evidence-safe descriptions of software engineering automation and request triage.
- **Engineering writing:** an honest index for published architecture notes; no fabricated articles.
- **About:** progression from industrial engineering and data science into AI systems engineering.
- **Resume/contact:** direct external resume, GitHub, LinkedIn, and email links.

## Visual direction

“System notebook”: warm paper-neutral surfaces, near-black typography, restrained electric-blue signal color, fine rules, compact metadata, and diagram-led technical storytelling. No gradients, stock imagery, animated hero, decorative AI motifs, or dependency-heavy icon library.

- Self-hosted/system fonts only; no font request.
- Content width capped for reading; broader diagram and project grids where useful.
- One small progressive-enhancement script for mobile navigation and current year.
- Motion limited to short hover/focus transitions and disabled under `prefers-reduced-motion`.
- WCAG-oriented contrast, visible focus, skip link, semantic landmarks, and keyboard-operable navigation.

## Professional narrative

DJ Dawkins designs AI-powered applications and workflows as software systems: explicit boundaries, tools, context, evaluation, authorization, failure handling, and operating constraints. Slater supplies public technical depth. Flock Safety supplies enterprise application and business-impact context without disclosing proprietary implementation.

## Evidence model

- **Verified:** supplied facts, reviewed resume, public repositories, or Slater audit/code evidence.
- **Reported:** internal outcomes stated in the reviewed resume; measurement details are not public.
- **Planned:** visually and verbally separated from implemented functionality.
- **Not published:** credentials, internal addresses, camera locations, account details, proprietary source, internal data, and unverified production claims.

## Deployment

A standard GitHub Pages workflow builds Jekyll and uploads `_site`. Pull requests build and validate but do not deploy. Pushes to `master` deploy after review and merge. This feature branch is never deployed by the workflow.
