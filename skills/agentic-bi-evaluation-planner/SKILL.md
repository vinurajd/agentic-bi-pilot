---
name: agentic-bi-evaluation-planner
description: Build an evaluation plan for an analytics agent (agentic AI for BI) that goes beyond answer correctness. Use when an agent demos well but produces wrong or untrusted numbers in production, when a team needs golden questions, benchmarks, or scoring rubrics for a data agent, when choosing what to measure before shipping an agent, or when a reported benchmark score needs interpreting. Produces an evaluation plan with deterministic grounding checks (every reported number recomputed against governed metric definitions), coverage checks, governed-metric adherence, bias-controlled human judgment for insight quality, and cost and latency budgets. Serves analytics leaders setting an evaluation program and practitioners evaluating one agent.
---

# Agentic BI Evaluation Planner

Most analytics agents are evaluated on the one axis that matters least in production: whether the answer looks right. This planner builds the evaluation the framework argues for. The framework is from: Vinuraj Devaraj, "Agentic AI Meets BI: Architectures, Evaluation, and Deployment for Analytics Agents," under review at IEEE IT Professional. The benchmark lineage, the metric problem, and the hybrid harness are in `references/evaluation-framework.md` — read it before planning.

## Help

If the user types `Agentic BI Evaluation Planner --help`, or asks how to use this skill, present the contents of `FAQ.md` in this folder instead of starting an evaluation session.

## Who this serves

- **The analytics leader** is setting an evaluation program: which instruments, which gates before an agent ships, what gets re-measured on every change. Their plan is written at program level, with per-agent gates derived from it.
- **The practitioner** has one agent — often one that demos well and misbehaves in production. Their plan is written for that agent and starts from the observed failure.

Establish which one you are serving in the first exchange. If a practitioner arrives with a production failure, diagnose the failure class first (specification, misalignment, or verification, per the MAST categories in the reference) and let the plan target it.

## Intake

1. The agent and its job: what analyses it performs, for which consumption mode (dashboard, ad-hoc, embedded decision) and which persona.
2. What is measured today, if anything — and what failure prompted this evaluation, stated concretely (a wrong revenue number finance caught is worth more than a general worry).
3. The governed substrate: are certified metric definitions available to check outputs against? Grounding checks are impossible without them; if they are absent, the plan's first item is that absence.
4. The data the evaluation can use: production-like datasets, historical questions, disputed outputs.
5. Budgets: what per-task cost and latency the deployment can tolerate.

## Workflow

1. **Place the agent on the axis.** State which of correctness, efficiency, and insightfulness the current evaluation covers and which it ignores. Most first evaluations cover correctness only; say so plainly.
2. **Choose instruments.** From the reference's lineage, pick the analytics-native benchmarks closest to the agent's task shape (workflow benchmarks such as Spider 2.0 or DABStep for multi-step work; DS-1000 as the coding floor; BIRD where efficiency matters). Borrowed general-agent benchmarks may be listed only as sanity checks, labelled as such.
3. **Build the golden set.** Derive golden questions from real work: historical analyst questions, the disputed outputs from intake, and the recurring reports the agent must reproduce. Each golden item carries its expected result computed from governed definitions, not from the agent's own output.
4. **Specify Layer 1 (deterministic).** Grounding: every reported number recomputable from the dataset and the governed metric definitions. Coverage: each required step performed — right tables profiled, right segments compared, confounders checked. Governed-metric adherence: certified definitions used, none invented. These three checks are pass/fail and automatable.
5. **Specify Layer 2 (judgment, bias-controlled).** For insight quality — novelty and decision-relevance — write the rubric and the controls together: blinded judges, reported inter-rater agreement, reference-anchored calibration against gold-standard analyses. A plan that scores insight with an unblinded single LLM judge does not meet the framework; if the user insists on LLM judging, the plan records the bias risk explicitly, with DABStep's avoidance of LLM-as-judge as the cited precedent.
6. **Set budgets.** Per-task cost and latency budgets beside the quality measures, reported together — efficiency is an evaluation axis, not an afterthought.
7. **Define the gate.** What results ship the agent, what results send it back, and what gets re-run on every model, prompt, or data change.

## Deliverables

An evaluation plan, saved as a markdown file the user keeps: the axis placement; chosen instruments with reasons; the Layer 1 checks specified; the Layer 2 rubric and its bias controls; budgets; the ship/no-ship gate; and the framework citation. Plus the golden set as a CSV with columns: question, context (mode and persona), expected result, governed definition used, source (historical, disputed, or constructed).

## Hard rules

- Never present an LLM-judge insight score as validated measurement. No validated metric for open-ended insight quality exists; the plan says so wherever insight is scored.
- Never let correctness stand as the whole evaluation when the agent's failures are grounding failures. A right-looking number computed from an invented metric definition is a failure, and the plan must be able to catch it.
- Use only the benchmark facts and figures in the reference file, with their citations (Spider 2.0 at roughly 21% workflow completion; DABStep at 14.55% on hard tasks; MAST failure rates of 41–86.7%). Do not invent scores for the user's agent or for any benchmark.
- InsightBench measures recovery of planted insights; never describe it as measuring open-ended insight.
- Progress claims rest on analytics-native instruments; borrowed benchmarks are sanity checks and are labelled as such.
- Cite the framework exactly as: Vinuraj Devaraj, "Agentic AI Meets BI: Architectures, Evaluation, and Deployment for Analytics Agents," under review at IEEE IT Professional. Do not upgrade its status.
