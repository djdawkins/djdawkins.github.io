---
layout: page
title: AI request triage agent
permalink: /projects/request-triage-agent/
description: Evidence-safe case study of DJ Dawkins' operational AI request triage agent at Flock Safety.
---
# AI request triage agent

**Flock Safety · Enterprise AI · Demonstrated workflow**

An evidence-grounded agent for operational request analysis, structured resolution, tool orchestration, and explicit escalation—with a clear boundary between demonstrated behavior and production readiness.

**Role:** AI Engineer  
**Runtime:** Python  
**Disclosure:** Architecture-level only

[← All projects]({{ '/projects/' | relative_url }})
## Problem {#problem}

Operational requests arrive with incomplete context, inconsistent language, and different levels of urgency. A person must identify the request type, gather evidence from enterprise systems, determine whether a known resolution applies, and route anything unresolved to the right stakeholder. Repeating that process delays response and consumes specialist time.

The system goal was to automate the evidence-gathering and repeatable resolution path without hiding uncertainty or preventing human intervention.

## My role {#role}

I architected and developed the Python-based agent workflow, including execution flow, tool invocation, enterprise data grounding, structured outputs, escalation policy, and evaluation infrastructure. The work also covered deployment planning and the operational controls needed to move from a successful proof of concept toward a dependable service.

## Agent runtime architecture {#architecture}

```text
Slack request
  → validate + normalize
  → enqueue execution
  → classify intent and required evidence
  → invoke approved data / workflow tools
  → assemble source-grounded result
  → apply resolution and escalation policy
  → respond or route to a human owner
  → record outcome for evaluation and operations
```

The queue separates user-facing intake from variable-latency reasoning and tool calls. The runtime persists enough state to identify the request, its evidence, tool outcomes, and final disposition. Structured output provides a stable contract for downstream routing rather than forcing operational code to parse prose.

## Grounding and tool orchestration {#grounding}

The agent retrieves SQL-backed evidence and invokes approved enterprise tools instead of answering from general model knowledge. Query caching reduces repeated retrieval for stable context. YAML-configured escalation policies keep routing rules reviewable and separate from prompt behavior.

Key controls:

- tool schemas constrain names, arguments, and response shapes;
- returned evidence is attached to the result before generation;
- unsupported or incomplete evidence becomes an escalation signal;
- structured fields distinguish resolution, confidence/evidence state, and next owner;
- a person remains available for exceptions and policy-sensitive decisions.

## Evaluation methodology {#evaluation}

I built an LLM evaluation harness to compare changes to models, prompts, and pipeline behavior. The important unit is the resolved request—not a fluent answer in isolation.

Evaluation dimensions include:

- classification and routing correctness;
- evidence completeness and factual support;
- resolution quality;
- unsupported-claim and escalation behavior;
- tool-selection and structured-output validity;
- regressions introduced by model, prompt, or orchestration changes.

A useful evaluation set includes representative resolved requests and difficult boundary cases. Production feedback should extend that set; it should not silently redefine success after every model change.

## Observability and deployment planning {#operations}

The operating design calls for queue depth and age, execution state, tool latency/errors, evidence retrieval outcomes, resolution/escalation rates, and evaluation version to be visible. Logs must identify a request and tool outcome without copying sensitive payloads unnecessarily.

Deployment planning separates configuration from code, versions prompts and policies, and retains human rollback paths. Failure handling must prefer a visible escalation over an unsupported automated resolution.

## Demonstrated versus production-ready {#status}

> **Demonstrated:** Python agent execution, Slack-oriented intake, SQL-backed evidence retrieval, tool orchestration, query caching, structured outputs, configurable escalation, and an evaluation harness.

> **Production-readiness work:** Long-running operational proof, alert thresholds, capacity behavior, broader failure drills, access review, and deployment controls require continued validation. This case study does not claim that proof-of-concept success alone establishes production maturity.

## Reported outcomes {#outcomes}

The reviewed current resume reports approximately **70% autonomous resolution** of incoming requests and approximately **8 hours saved per employee per week**.

These figures are internal outcomes summarized in the resume. Their source data and measurement definition are not published; the portfolio does not expose enterprise request content or operational data.

## Lessons {#lessons}

1. Evidence retrieval and escalation policy are first-class agent components, not prompt footnotes.
2. Structured results create a dependable boundary between probabilistic reasoning and deterministic workflow routing.
3. A queue improves resilience only when execution state and failure ownership are observable.
4. Evaluation must measure supported resolution and appropriate refusal—not answer style alone.
5. Production readiness is a separate claim that requires operational evidence, not just a working demonstration.
