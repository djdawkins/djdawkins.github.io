---
layout: case-study
title: "Slater: a private, voice-first AI assistant"
eyebrow: Flagship personal system · Independent engineering
intro: A locally hosted assistant built to make household intelligence conversational without turning the model into the database, the authorization layer, or the deployment strategy.
permalink: /projects/slater/
description: Technical case study of Slater, DJ Dawkins' local-first AI assistant architecture, orchestration, evaluation, security, and evolution.
meta:
  Status: Implemented · evolving
  Stack: TypeScript · React · Express
  Inference: Local · RTX 5090 workstation
  Interfaces: Web · Voice · MCP
sections:
  - id: problem
    label: Problem
  - id: architecture
    label: Architecture
  - id: decisions
    label: Decisions
  - id: orchestration
    label: LLM infrastructure
  - id: evaluation
    label: Evaluation
  - id: security
    label: Security & deployment
  - id: challenges
    label: Challenges
  - id: evolution
    label: Evolution
  - id: current
    label: Current functionality
  - id: roadmap
    label: Roadmap
---
## The problem {#problem}

Most assistants become fragile at the seams: one prompt accumulates every domain, tool access is implicit, transport logic forks the reasoning path, and a working development server is mistaken for an operable product. Slater began as a way to ask natural-language questions about household security and grew into a test bed for a harder question:

> How do you build a personal assistant that can gain capabilities without gaining hidden access, duplicated orchestration, or unverifiable behavior?

The product goal is private, useful interaction across web, voice, and machine clients. The engineering goal is a system in which each new domain has an explicit data contract, authorization boundary, context policy, evaluation path, and deployment story.

## Current architecture {#architecture}

Slater runs across a dedicated local AI workstation and a separate household-services node. The AI workstation hosts local inference and one supervised application instance per environment. A household integration API provides server-side access to camera events, media, and structured services; credentials never enter the browser or model arguments.

<figure class="diagram">
  <img src="{{ '/assets/images/slater-architecture.svg' | relative_url }}" width="1080" height="620" alt="Architecture diagram showing three clients sharing one API and chat core, an authorized capability registry, local model gateway, owner-scoped SQLite storage, and a separate household integration API.">
  <figcaption>Current verified shape after Phase 0 V2. Dashed Finance and Health modules are contracts only; they are not registered capabilities.</figcaption>
</figure>

### Runtime boundaries

- **React web UI:** saved conversations, source cards, authenticated media, and live view.
- **iPhone Shortcut:** spoken requests with optional rich response and camera links.
- **MCP:** authenticated machine access to the same core; currently Security only.
- **Express API:** composition root for ingress, authentication, persistence, media relays, voice, and MCP.
- **Chat core:** prompt assembly and a bounded model/tool loop. It imports no domain implementation.
- **Capability registry:** resolves one subject-scoped view of tools, instructions, authorization, and opt-in context.
- **SQLite:** owner-scoped conversations, sessions, request deduplication, and voice idempotency state.
- **Local model gateway:** OpenAI-compatible text and optional vision inference under an endpoint policy.

## Engineering decisions {#decisions}

### One core, multiple transports

Web conversations, voice requests, and MCP calls all enter `createChatCore().run()`. A transport decides authentication, persistence, and presentation—not what the assistant knows or how tools execute. This avoids three assistants drifting behind three interfaces.

### Capabilities own domain behavior

A capability owns its tool schemas, validation, execution, prompt rules, authorization, client exposure, and optional injected context. The core receives an authorized view from the registry. Duplicate capability IDs and tool names fail during composition; unauthorized and unknown tools return the same refusal.

### Context is opt-in policy

Security retains an always-injected digest because current behavior depends on it. New domains inject nothing by default and expose data only through an authorized tool call. This makes context cost and privacy a reviewed decision instead of an accidental consequence of registration.

### Deterministic code owns facts

Time windows, camera roster checks, source retrieval, card construction, and future numeric facts are server-side. The model selects tools and explains returned evidence; it does not widen a time range, invent a camera, or calculate a financial total from a capped feed.

## LLM and agent infrastructure {#orchestration}

<figure class="diagram">
  <img src="{{ '/assets/images/slater-request-flow.svg' | relative_url }}" width="1080" height="470" alt="Sequence diagram of authentication, conversation storage, capability resolution, prompt construction, local model inference, validated tool execution, and transport-specific response delivery.">
  <figcaption>The subject comes from authenticated ingress. Model-generated arguments cannot change identity or the authorized tool menu.</figcaption>
</figure>

The prompt is assembled from general rules, a transport-specific media policy, authorized capability instructions, local time, opt-in capability context, and bounded history. History includes complete turns only, with limits of 24 turns, 8,000 characters overall, and 4,000 per turn. Prior assistant prose is marked stale.

The model loop is deliberately bounded to four steps and 900 completion tokens per step. Security exposes three tools: open a live view, inspect a current camera frame, and retrieve camera events within a validated period. Results can carry prose for the model plus typed sources, facts, actions, and errors for transports.

Voice adds owner-scoped continuation and request idempotency around the same core. A reserve → generate → complete ledger replays an identical retry rather than running probabilistic generation twice. MCP supports thread continuity but does not yet have equivalent idempotency.

## Evaluation and reliability {#evaluation}

<div class="evidence-strip" aria-label="Verified Slater evidence">
  <div><strong>413</strong><span>tests across 38 files</span></div>
  <div><strong>19 / 19</strong><span>offline evaluation replay checks</span></div>
  <div><strong>3</strong><span>transports sharing one core</span></div>
</div>

The evaluation harness runs frozen fixtures through the real chat core with a scripted model and no network. It asserts structural behavior—not only answer wording:

- exact tool selection and argument subsets;
- offered tools and authorized capability IDs;
- prompt inclusion and exclusion for context isolation;
- returned facts and provenance;
- multi-turn history carry;
- source/action bounds and maximum steps;
- deterministic, normalized traces.

A synthetic Finance-like capability proves that a second domain can register and return a typed fact without editing the core. Mutation checks deliberately removed authorization and history inputs to prove the assertions fail for the defects they claim to catch. Prompt and tool fingerprints also prove that moving Security behind the capability boundary preserved existing behavior byte-for-byte.

Reliability controls include request deduplication, explicit retry state, bounded model calls, owner-scoped thread resolution, graceful storage degradation for voice/MCP, model and MCP timeouts, a single-writer database lock, and clear mock/unavailable labeling when household data cannot be reached.

## Security and deployment {#security}

Slater is local-first by enforced default, not by marketing language.

- Model endpoints are checked by origin, DNS resolution, and CIDR; redirects are refused. Loopback is the default allowlist for text and vision.
- Household data routes and the live-stream WebSocket require an owner session.
- The subject is derived by the server. Tool arguments cannot elevate access.
- Machine clients are default-deny per capability. Security explicitly allows MCP; future sensitive domains do not inherit that access.
- Production and development have separate supervised processes, databases, credentials, cookies, origins, and instance markers.
- Startup refuses unsafe combinations such as production auth bypass, a bypass on a public bind, a database marker mismatch, or two live writers.

<div class="callout callout--boundary">
  <h3>Privacy boundary</h3>
  <p>Local-only inference is an enforced default, not a complete privacy guarantee. Conversations are not encrypted at rest; retention policy, data classification, per-read audit, and per-client MCP identity remain open work.</p>
</div>

## Technical challenges {#challenges}

### Refactoring without changing model behavior

Moving Security out of the core risked silent prompt or tool drift. The migration moved code rather than rewriting it, captured fixed-clock fingerprints before the refactor, and pinned prompt variants, tool payloads, ordering, and existing replay fixtures afterward.

### Retry-safe probabilistic APIs

A voice retry can be expensive and return a different answer. The solution fingerprints the request and thread, reserves before inference, stores the completed payload, and replays exact results. The schema addition is inert to older code, so rollback does not require a database restore.

### Honest future-domain semantics

The existing finance feed uses capped retrieval and unsafe aggregate semantics; Health is still mock data. Instead of wiring them into chat, Phase 0 defined contracts for complete pagination, calendar windows, currency separation, pending/transfer/refund handling, provenance, permissions, and missing-versus-zero behavior. The decision was to delay capability registration until the data can answer truthfully.

## Architecture evolution {#evolution}

| Stage | System shape | Why it changed |
|---|---|---|
| Initial implementation | One useful Security assistant; shared chat core; web and voice; camera tools | Proved the interaction and deterministic retrieval boundary |
| Pre-Phase 0 V2 | Security assumptions spread across prompt, dependencies, and tools; one shared operational environment | New domains required core edits; deployment and authorization had unsafe implicit assumptions |
| Phase 0A | Two enforced environments; route auth; model egress policy; supervised processes | Made deployment identity, access, and model data movement explicit |
| Phase 0B/C | Capability registry; opt-in context; synthetic domain; generalized replay | Turned modularity and context isolation into tested interfaces |
| Phase 0D | Voice/MCP continuity; voice idempotency; additive storage | Made retries safe and transport history consistent without forking orchestration |
| Phase 0E | Typed facts/errors; Finance and Health contracts; machine default-deny | Specified correctness and privacy before exposing sensitive domains |

The differentiator is not the number of integrations. It is the progression from implicit assumptions to enforceable boundaries, with evidence that the refactor preserved current behavior.

## Current functionality {#current}

<div class="callout callout--verified">
  <h3>Implemented and verified</h3>
  <p>Saved web conversations; local text inference; Security context and three camera tools; source cards and authenticated media; iPhone voice requests; server-side conversation continuity; voice idempotency; MCP Security access; local model endpoint policy; production/development isolation; offline replay evaluation; typed capability outcomes.</p>
</div>

**Explicitly not claimed:** conversational Finance or Health, persistent personal memory, proactive tasks, per-client MCP identity, comprehensive metrics/alerting, encrypted-at-rest conversations, or immutable artifact promotion. The phone Shortcut remains stateless; saved voice threads continue in the web UI.

## Roadmap {#roadmap}

Planned work is separated from current capability:

1. **Finance adapter and capability:** complete source pagination, authoritative provenance, deterministic calculations, answer-safety fixtures, and transport rendering of facts.
2. **Health ingestion:** evidence-based source overlap rules, permissions, retention/deletion, artifact access, and no silent missing-as-zero behavior.
3. **Typed conversation state:** carry domain, entity, and time-window scope without relying on re-inference from prose.
4. **Operational maturity:** immutable deployment artifacts, commit identity, correlation IDs, durable metrics, alerting, and dependency health.
5. **Machine authorization:** per-client MCP identity, domain grants, recorded opt-in, revocation, and per-read audit before sensitive exposure.

### Selected lessons

- A good model loop does not compensate for weak trust boundaries.
- Context injection is an authorization and privacy policy, not a prompt convenience.
- Replay evaluation is strongest when it asserts structure and is mutation-tested.
- Contracts can be meaningful delivery when they prevent an unsafe integration—but they must never be described as the integration itself.
