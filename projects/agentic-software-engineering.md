---
layout: case-study
title: Agentic software engineering automation
eyebrow: Flock Safety · Enterprise AI
intro: A human-governed coding workflow that connects organizational context, engineering tools, repository changes, and review feedback without treating autonomous execution as the goal.
permalink: /projects/agentic-software-engineering/
description: Evidence-safe case study of DJ Dawkins' agentic software engineering automation work at Flock Safety.
meta:
  Role: AI Engineer
  Status: Operational workflow
  Domain: Developer productivity
  Disclosure: Architecture-level only
sections:
  - id: problem
    label: Problem
  - id: role
    label: Role
  - id: architecture
    label: Architecture
  - id: decisions
    label: Decisions
  - id: challenges
    label: Challenges
  - id: outcomes
    label: Outcomes
  - id: lessons
    label: Lessons
---
## Problem {#problem}

Recurring engineering requests were slowed by the work around the code: locating business context, understanding repository conventions, decomposing ambiguous tasks, coordinating approvals, implementing changes, and responding to review feedback. The goal was not “let an agent code.” It was to shorten a governed engineering workflow while keeping humans in control of consequential decisions.

## My role {#role}

I architected and developed the agentic workflow as an AI Engineer. My contribution covered system shape, context and tool integration, task planning, approval points, code execution, repository interaction, and the loop that turns review feedback into an updated implementation.

The work connected enterprise knowledge and structured data with engineering systems through approved APIs and MCP-style tools. Proprietary prompts, source code, internal schemas, and workflow details are intentionally omitted here.

## Solution architecture {#architecture}

```text
Request
  → retrieve business + repository context
  → decompose into bounded engineering tasks
  → produce implementation plan and evidence
  → human approval
  → execute repository changes with tools
  → open/update GitHub work
  → ingest code-review feedback
  → revise or escalate
```

The architecture separates probabilistic planning from deterministic effects. The agent may propose a plan and select tools; repository writes, branch state, checks, approval status, and GitHub operations use explicit tool contracts and observable state.

### Core responsibilities

- **Context layer:** gather the organizational, ticket, repository, and data context needed for the specific request.
- **Planner:** turn the request into scoped steps with dependencies and acceptance criteria.
- **Approval gate:** require a person to validate the plan before consequential repository changes.
- **Executor:** invoke approved repository and engineering tools, preserving their results as evidence.
- **Review loop:** consume code-review feedback, distinguish actionable changes from questions, and route updates through the same controls.
- **Escalation:** stop when context is insufficient, a tool fails, or a decision exceeds the agent's authority.

## Decisions and trade-offs {#decisions}

### Human approval before execution

Autonomy was not the primary success metric. Approval separates fast synthesis from accountable engineering judgment and gives reviewers a compact point to correct scope before code changes compound a mistake.

### Tools over free-form side effects

Repository modification and enterprise integrations are modeled as bounded operations. This makes permissions, arguments, outcomes, and failures inspectable. It also avoids encoding business access inside prompts.

### Retrieve context for the task

The system assembles relevant context rather than copying broad organizational data into every request. This improves precision and reduces unnecessary exposure, but depends on retrieval quality and source freshness.

### Integrate with the existing workflow

GitHub and code-review feedback remain the collaboration surface. The agent participates in established engineering controls rather than requiring teams to adopt a parallel review system.

## Technical challenges {#challenges}

- **Ambiguous requests:** decomposition must expose assumptions and missing acceptance criteria instead of inventing scope.
- **Context conflicts:** ticket language, repository behavior, and organizational documentation can disagree; outputs need source-aware evidence and escalation.
- **Partial execution:** a sequence can fail after some changes exist, so branch and tool state must be recoverable and visible.
- **Review interpretation:** feedback can be a requested change, a question, or a disagreement; blindly editing on every comment creates churn.
- **Operational control:** tool permissions, approval state, retries, and auditability matter more than a persuasive generated plan.

## Reported outcomes {#outcomes}

The reviewed current resume reports that the workflow automated approximately **80% of recurring development work** and reduced typical request completion from **1–2 weeks to 2–3 days**.

<div class="callout callout--boundary">
  <h3>Measurement boundary</h3>
  <p>These are internally reported outcomes summarized in the current resume. The underlying request cohort, measurement window, and proprietary operational data are not published. They should be treated as directional evidence, not a public benchmark.</p>
</div>

## Lessons {#lessons}

1. The most useful coding agent is a workflow participant, not an isolated code generator.
2. Planning quality improves when the output must survive an explicit approval gate.
3. Agent reliability depends on deterministic tool contracts, recoverable state, and clear stop conditions.
4. Enterprise context is valuable only when its source, freshness, and access boundary remain visible.
5. Business impact comes from shortening the whole path to an accepted change—not maximizing generated lines of code.
