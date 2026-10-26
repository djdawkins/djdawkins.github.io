---
layout: page
title: About
eyebrow: Background and approach
intro: Industrial engineering taught me to see systems. Data science taught me to model uncertainty. AI engineering brings those disciplines together in software that has to work.
permalink: /about/
description: About DJ Dawkins, an AI Engineer in Atlanta focused on agentic systems, LLM applications, and intelligent automation.
---
<div class="profile-grid">
  <div>
    <img class="profile-image" src="{{ '/assets/images/dj-dawkins.webp' | relative_url }}" width="900" height="900" alt="DJ Dawkins">
  </div>
  <div>
    <h2>Engineering the system around the model</h2>
    <p>I am an AI Engineer at Flock Safety, based in the Atlanta metropolitan area. My work sits where software engineering, applied AI, operational data, and business process design meet.</p>
    <p>I began in industrial engineering and semiconductor planning, building models and decision systems for constrained, high-consequence operations. I moved into data science through a master's program and retail pricing work, then into AI engineering as LLMs made it possible to build software that can reason over context, invoke tools, and participate in workflows.</p>
    <p>The part I care about most is everything required after a promising demo: clear interfaces, grounded context, evaluation, authorization, observable failure modes, human control, and a deployment model that matches the sensitivity of the data.</p>
    <div class="button-row">
      <a class="button button--primary" href="{{ site.linkedin_url }}">LinkedIn</a>
      <a class="button" href="{{ site.github_url }}">GitHub</a>
      <a class="button" href="mailto:{{ site.email }}">Email</a>
    </div>
  </div>
</div>

## Engineering principles

1. **Design the deterministic boundary first.** Retrieval, authorization, validation, scope, arithmetic, and side effects should not depend on model prose.
2. **Treat context as governed data movement.** A prompt is an integration boundary with cost, privacy, and authorization implications.
3. **Test architecture claims.** Replay, mutation checks, HTTP tests, and runtime smoke checks are stronger than a diagram alone.
4. **Name what is not implemented.** A contract is not an integration. A proof of concept is not a production service. A local default is not a complete privacy guarantee.
5. **Connect engineering to the decision it improves.** Systems earn their complexity through useful outcomes, not novelty.

## Outside the current role

Slater is my primary independent engineering project: a private, locally hosted assistant used to explore capability architecture, local inference, voice interfaces, computer vision, MCP integration, evaluation, and safe operation on personal infrastructure.
