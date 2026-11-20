# Agentic BI Design Advisor — FAQ

## Getting started

**What does this skill do?**
It helps you choose and specify an architecture for an analytics agent — an AI agent that answers questions, runs analyses, or produces reports from business data — before you build it. It works from a four-pattern taxonomy of analytics-agent architectures and produces a design brief you can hand to a builder.

**How do I start?**
Describe the job the agent must do, in the terms a human analyst does it today. The skill will ask about the consumption mode (dashboard, ad-hoc analysis, or embedded decision), who the agent serves, and whether your data sits behind a governed semantic layer.

**Who is it for?**
Two users equally: an analytics leader planning a program of agents across several use cases, and a practitioner designing a single agent. Tell the skill which you are; the brief is shaped differently for each.

## The framework

**What are the four patterns?**
Planner–executor(–critic) loops, which separate deciding what to do from doing it. Role-specialized pipelines, which assign agents fixed professional roles along an assembly line. Graph-orchestrated swarms, which treat the agent collective as a computational graph. And search-augmented planners, which explore a space of solution paths instead of committing to a first plan.

**Which pattern is best?**
None, and the skill will not pretend otherwise. Each pattern fits a task shape: governed repeatable reporting suits role pipelines, multi-step decomposable analysis suits planner–executor loops, open-ended exploration suits swarms, and optimization problems suit search-augmented planners. The brief recommends from your task shape and states what the choice trades away.

**Where does the framework come from?**
Vinuraj Devaraj, "Agentic AI Meets BI: Architectures, Evaluation, and Deployment for Analytics Agents," under review at IEEE IT Professional. The taxonomy, the comparison axes, and the system examples are the survey's, cited in the brief.

**Why does it keep asking about a semantic layer?**
Because in a governed BI practice, metric definitions live in a semantic layer, and an agent that bypasses it and queries raw tables will invent definitions — the failure mode enterprises fear most. A design that cannot ground in governed definitions carries that risk, and the brief names it rather than passing over it.

## The brief

**What do I receive?**
A design brief as a markdown file: the use case and mode, the persona served, the recommended pattern with its task-shape reasoning, a trade-off table across coordination, failure modes, cost, debuggability, and fit, the runner-up pattern and why it lost, the grounding strategy, the oversight points, and the failure classes the design must defend against.

**Will it tell me to use more agents?**
Only if the task shape buys something with them. Adding agents raises coordination failures, multiplies token cost, and makes the system harder to debug. The brief must state what each added agent earns.

**Can it redesign an agent we already run?**
Yes. Describe the current architecture and where it hurts. The skill maps the existing design onto the taxonomy and writes the brief as a redesign, naming the failure classes the current pattern is exposed to.
