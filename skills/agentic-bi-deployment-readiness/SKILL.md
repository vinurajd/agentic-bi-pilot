---
name: agentic-bi-deployment-readiness
description: Readiness-check an analytics agent (agentic AI for BI) before or after it ships. Use when a team is about to deploy an agent that reads business data, spreadsheets, documents, emails, or logs; when a live agent's cost, reliability, security, or privacy is in question; or when a security or governance review needs the agent assessed. Audits six areas — cost and latency, reliability, security including indirect prompt injection through ingested data, privacy enforced at runtime, human oversight and governance, and the KPI trust contract — and produces a scorecard with a verdict and named evidence per check. Composes with the Semantic Layer Contract Checker for the deep semantic-layer audit. Serves analytics leaders clearing a program for production and practitioners shipping one agent.
---

# Agentic BI Deployment Readiness

Deployment is where analytics agents are weakest, and where demos go to die. This review checks a deployment against what the literature says actually breaks. The framework is from: Vinuraj Devaraj, "Agentic AI Meets BI: Architectures, Evaluation, and Deployment for Analytics Agents," under review at IEEE IT Professional. The six audit areas, their evidence, and their sources are in `references/deployment-checklist.md` — read it before reviewing.

## Help

If the user types `Agentic BI Deployment Readiness --help`, or asks how to use this skill, present the contents of `FAQ.md` in this folder instead of starting a review.

## Who this serves

- **The analytics leader** is clearing a program: several agents heading for production under one governance posture. Their scorecard is written per agent, with the program-level gaps (shared controls missing, shared risks repeated) summarised once at the top.
- **The practitioner** is shipping, or has shipped, one agent. Their scorecard is written for that agent, ordered by what blocks shipment.

Establish which one you are serving in the first exchange.

## Intake

1. The agent: its job, its architecture pattern if known, its consumption mode (dashboard, ad-hoc, embedded decision), and the persona it serves.
2. What it ingests: every data source, including spreadsheets, CSVs, emails, logs, and documents — the ingestion list defines the threat model, so it must be complete.
3. What it can do: tools, actions, and the permissions behind them; what a wrong or manipulated instruction could reach.
4. What data it can reach: governed semantic layer or raw tables; PII or regulated data in scope; how access is enforced today.
5. What it costs and how it behaves: measured per-task cost and latency if known; known failures if it is already live.
6. Where it stands: pre-deployment, or live and under question.

## Workflow

Work the six areas of `references/deployment-checklist.md` in order. For every check, record one of four verdicts with the evidence that decides it:

- **Ready** — the control exists and the evidence names it (the artefact, the measurement, the test).
- **Ready with controls** — the control exists in partial form; the gap and its compensating control are both named.
- **Not ready** — the control is absent, or present only as an instruction to the model where the framework requires system enforcement.
- **Not assessable** — the evidence does not exist yet; state what evidence would decide it. Silence is never scored as readiness.

Three checks carry special weight and are never softened:

- **Privacy by prompting is not ready.** Privacy knowledge does not transfer to agent behaviour (PrivacyLens: 90–95% on privacy questions, 25–40% leakage in actions). Access control must be enforced by the system around the agent at query time, or Area 4 is Not ready.
- **Ungoverned metrics are not ready.** If the agent can report a metric whose definition it synthesized rather than drew from the certified semantic layer, Area 6 is Not ready, whatever the other areas say.
- **Untreated ingestion is not ready.** If the agent ingests external or user-supplied content with no injection threat model and unscoped tool permissions, Area 3 is Not ready.

Where a dbt manifest or PromptQL / Hasura DDN metadata project is available, record whether the Semantic Layer Contract Checker (the companion skill by the same author) has audited the semantic layer, and carry its findings into Area 6. If it has not been run, the scorecard recommends it; this review does not reproduce its ten-requirement audit.

## Deliverable

A readiness scorecard, saved as a markdown file the user keeps: one section per area, each check with its verdict and deciding evidence; an overall verdict (ship, ship with controls, or do not ship) that follows the worst blocking area rather than averaging; the blocking gaps ordered by severity; and the framework citation. For a leader, per-agent scorecards plus a program summary of shared gaps.

## Hard rules

- A check is never passed on assertion alone. Every Ready verdict names its evidence; every Not ready verdict names the missing control.
- Never average away a blocking failure. An agent that leaks data through its query layer is not "mostly ready."
- Use only the figures and findings in the reference file, with their citations (MAST failure rates of 41–86.7%; ToolEmu's safest agent failing 23.9% of cases; PrivacyLens leakage of 25–40% in actions; over 90% of surveyed agents lacking explicit trust and safety mechanisms). Do not invent incident rates or control effectiveness.
- Where the literature offers evaluation more mature than defences — the injection area is the standing example — record the gap honestly instead of arguing it away.
- OWASP and NIST mappings use the items named in the reference (LLM01, LLM02, LLM06, LLM10; NIST Govern, Map, Measure, Manage). Do not extend the mapping to items the reference does not cover.
- Cite the framework exactly as: Vinuraj Devaraj, "Agentic AI Meets BI: Architectures, Evaluation, and Deployment for Analytics Agents," under review at IEEE IT Professional. Do not upgrade its status.
