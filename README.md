# Agentic BI Pilot

Three skills for the people who design, evaluate, and ship analytics agents — AI agents that answer questions, run analyses, and produce reports from business data. The skills operationalise one framework: Vinuraj Devaraj, "Agentic AI Meets BI: Architectures, Evaluation, and Deployment for Analytics Agents," under review at IEEE IT Professional.

The survey's argument, in one line: agents that do not understand metric layers and governance fail in production regardless of their benchmark scores. These skills turn that argument into three working instruments.

## The skills

**Agentic BI Design Advisor** (`skills/agentic-bi-design-advisor/`)
Choose the architecture before building. Walks a four-pattern taxonomy — planner–executor(–critic) loops, role-specialized pipelines, graph-orchestrated swarms, search-augmented planners — maps your use case to its task shape, BI consumption mode, and serving persona, and produces a design brief with the recommendation, its trade-offs across coordination, failure modes, cost, debuggability, and fit, and the grounding and oversight design.

**Agentic BI Evaluation Planner** (`skills/agentic-bi-evaluation-planner/`)
Evaluate beyond correctness. Builds an evaluation plan on the framework's axis — correctness, then efficiency, then insightfulness — with deterministic grounding checks (every reported number recomputed against governed metric definitions), coverage checks, governed-metric adherence, bias-controlled human judgment for insight quality, and cost and latency budgets. Ships with a golden-set CSV format.

**Agentic BI Deployment Readiness** (`skills/agentic-bi-deployment-readiness/`)
Readiness-check the deployment across the six areas where analytics agents actually break: cost and latency, reliability, security (including indirect prompt injection through the data agents ingest), privacy enforced at runtime rather than by prompting, human oversight and governance (OWASP LLM Top 10, NIST AI RMF), and the KPI trust contract. Produces a scorecard with a verdict and named evidence per check.

Each skill serves two users: the analytics leader planning or clearing a program, and the practitioner working on one agent. Tell the skill which you are.

## Companion tool

The [Semantic Layer Contract Checker](https://github.com/vinurajd/semantic-layer-contract-checker) (same author) audits a semantic-layer project — a dbt manifest or PromptQL / Hasura DDN metadata — against a ten-requirement machine-consumption contract. The Deployment Readiness skill composes with it: the checker audits the layer, the readiness review audits the agent built on top of it.

## Install

**Claude Code** (plugin):
```
/plugin marketplace add vinurajd/agentic-bi-pilot
/plugin install agentic-bi-pilot@vinurajd-skills
```

**Claude, Gemini CLI, Codex, and other SKILL.md hosts**: download the skill zip from the latest GitHub Release and place the skill folder you need (`skills/agentic-bi-design-advisor`, `skills/agentic-bi-evaluation-planner`, or `skills/agentic-bi-deployment-readiness`) in your assistant's custom-skills location. Each skill folder is self-contained, including its references and FAQ.

**Help**: type `<Skill Name> --help` in conversation, or ask the skill how to use it, and it presents its FAQ instead of starting a session.

## Honesty notes

- The framework paper is under review at IEEE IT Professional. The skills cite it exactly that way and do not present it as published.
- Every figure the skills use (benchmark results, failure rates, study findings) comes from the paper's reference apparatus with its source named. The skills do not invent numbers.
- No validated metric for open-ended insight quality exists. The Evaluation Planner says so wherever insight is scored, and designs judgment with bias controls rather than dressing up an LLM judge's opinion as measurement.

## Licence

MIT. See `LICENSE`.
