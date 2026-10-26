---
layout: page
title: Engineering projects
eyebrow: Case studies
intro: Systems presented through problems, decisions, evidence, and boundaries—not feature lists.
permalink: /projects/
description: AI engineering case studies by DJ Dawkins, including Slater and enterprise agentic systems.
---
<div class="project-grid">
  {% include project-card.html featured=true type="Flagship personal system" status="Implemented" title="Slater — private, voice-first AI assistant" description="A distributed, locally hosted assistant built around one chat core, capability boundaries, tool orchestration, evaluation replay, and explicit trust boundaries." tags="Local LLM, Agent tools, Context, Evaluation, MCP, Voice, Security" url="/projects/slater/" %}
  {% include project-card.html type="Enterprise AI · Flock Safety" status="Operational" title="Agentic software engineering automation" description="A human-governed workflow for decomposing engineering requests, retrieving organizational context, modifying repositories, and processing review feedback." tags="Coding agents, Planning, GitHub, Human approval, Enterprise integration" url="/projects/agentic-software-engineering/" %}
  {% include project-card.html type="Enterprise AI · Flock Safety" status="Demonstrated" title="AI request triage agent" description="An evidence-grounded Python agent for request analysis, tool use, structured resolution, evaluation, and explicit escalation." tags="Python, Tool invocation, Structured outputs, Evaluation, Observability" url="/projects/request-triage-agent/" %}
</div>

## Earlier work

These projects remain useful as evidence of the path into AI engineering. They are intentionally secondary to current systems work.

<div class="earlier-grid">
  <article class="earlier-card"><p class="eyebrow">Voice interface · 2020</p><h3>Celebrity Jeopardy</h3><p>An Alexa trivia skill that introduced voice interaction design, intent handling, and consumer-facing conversational UX.</p><a href="https://github.com/djdawkins/alexaVOICE_NUG">Source repository <span aria-hidden="true">↗</span></a></article>
  <article class="earlier-card"><p class="eyebrow">Applied NLP</p><h3>ClassMate</h3><p>An essay-feedback application exploring how machine learning could support teachers and students. Retained for the problem framing; the original hosted demo is no longer presented as maintained.</p></article>
  <article class="earlier-card"><p class="eyebrow">Predictive analytics</p><h3>NBA Top Scout</h3><p>A graduate analytics project modeling prospective NBA player value, demonstrating feature design, predictive modeling, and interactive decision support.</p><a href="https://github.com/djdawkins/NbaBizAnalytics">Source repository <span aria-hidden="true">↗</span></a></article>
</div>
