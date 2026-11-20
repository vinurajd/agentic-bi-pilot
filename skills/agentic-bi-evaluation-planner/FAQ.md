# Agentic BI Evaluation Planner — FAQ

## Getting started

**What does this skill do?**
It builds an evaluation plan for an analytics agent that goes beyond "did the answer look right." The plan checks whether every number the agent reports can be recomputed from the data and the governed metric definitions, whether the analysis did all the steps the task required, whether certified definitions were used, and — with proper bias controls — whether the insights are worth acting on. It also sets cost and latency budgets, because an agent makes dozens of model calls per question.

**How do I start?**
Describe the agent, its job, and what is measured today. If a failure brought you here, describe it concretely: a wrong revenue figure that finance caught will shape a better plan than a general worry.

**Who is it for?**
An analytics leader setting an evaluation program and ship gates, and a practitioner with one agent — often one that demos well and misbehaves in production.

## The framework

**What is wrong with measuring correctness?**
Nothing, except that it is not the whole job. The field's metrics have evolved along one axis — correctness, then efficiency, then insightfulness — and most evaluations stop at the first. An agent can return a correct-looking number computed from a metric definition it invented. That is a production failure no correctness benchmark catches.

**Which benchmarks does it use?**
Analytics-native ones, matched to your agent's task shape: Spider 2.0 and DABStep for multi-step workflows, BIRD where efficiency matters, DS-1000 as a coding floor, and others from the lineage in the framework. General agent benchmarks are labelled sanity checks only. For calibration: the best agents complete roughly 21% of Spider 2.0's enterprise workflows and 14.55% of DABStep's hard tasks, so a plan that expects near-perfection is measuring the wrong thing.

**Can an LLM judge score our agent's insights?**
It can score them, but the score is not validated measurement, and this skill will not present it as such. No validated metric for open-ended insight quality exists. Where judgment is used, the plan requires the controls that make it defensible: blinded judges, reported agreement between raters, and calibration against gold-standard analyses. DABStep, the most production-like benchmark in the field, avoids LLM judges entirely because of judge bias.

**Where does the framework come from?**
Vinuraj Devaraj, "Agentic AI Meets BI: Architectures, Evaluation, and Deployment for Analytics Agents," under review at IEEE IT Professional.

## The plan

**What do I receive?**
An evaluation plan as a markdown file — where your current evaluation sits on the correctness–efficiency–insightfulness axis, the instruments chosen and why, the deterministic checks specified, the judgment rubric with its bias controls, the cost and latency budgets, and the ship or no-ship gate — plus a golden question set as a CSV, each item with its expected result computed from governed definitions.

**Our agent demos beautifully and fails in production. Will this help?**
That gap is exactly what the plan is built to close. The first step is classifying the production failures — misunderstanding the request, agents working at cross-purposes, or failures of checking — because each class needs different tests. The plan then targets the class you actually have.

**We have no governed metric definitions. Can we still evaluate?**
Partially, and the plan will say so. Grounding checks need certified definitions to check against. Without them, the plan's first item is that absence, because it is also a production risk, not only an evaluation gap.
