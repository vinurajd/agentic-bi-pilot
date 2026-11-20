# Evaluation Framework for Analytics Agents

Reference for the Agentic BI Evaluation Planner. Distilled, without alteration of substance, from: Vinuraj Devaraj, "Agentic AI Meets BI: Architectures, Evaluation, and Deployment for Analytics Agents," under review at IEEE IT Professional (Section 6, with Sections 2 and 7).

## The central claim

The field's metrics are evolving along a single axis: **correctness → efficiency → insightfulness**. Spider measured exact-match correctness. BIRD added efficiency. Spider 2.0 and DABStep measure realistic workflow completion — a harder, more honest form of correctness. InsightBench attempts insightfulness, but only for planted insights. What remains unmeasured is what decision-makers actually care about: open-ended insight quality, novelty, and decision-relevance. No validated metric exists for whether an agent's findings are worth acting on.

Until one does, benchmark leaderboards reward systems optimised for the measurable — query correctness, task completion — while the unmeasured dimensions (did the agent use the governed metric definition? is the finding novel? would a decision-maker trust it?) determine success or failure in production.

## Benchmark lineage (analytics-native instruments)

| Benchmark | What it tests | Key facts |
|---|---|---|
| Spider (2018) | Text-to-SQL, exact-match correctness | 10,181 questions, 200 databases, 138 domains; mostly clean single-domain schemas |
| BIRD (2023) | Text-to-SQL on messy real-world data, plus efficiency | 12,751 question–SQL pairs, 95 large databases; introduced the Valid Efficiency Score (VES) — runtime graded alongside correctness |
| Spider 2.0 (ICLR 2025) | Authentic enterprise workflows | 632 multi-step workflows (exploration, transformation, interpretation); best agents complete roughly 21% |
| DABStep (2025) | Multi-step analysis with contextual reasoning | 450+ tasks from a financial analytics platform; code processing plus reasoning over heterogeneous documentation (fee tables, category mappings, policy notes); factoid answers with automatic scoring; deliberately avoids LLM-as-judge because of judge bias; best agents reach 14.55% on hard tasks |
| DS-1000 (2023) | Data-science coding | 1,000 problems across seven Python libraries; the "can the model write analysis code" floor |
| InfiAgent-DABench (ICML 2024) | End-to-end analysis | 257 questions over 52 CSV files; the benchmark on which Data Interpreter reported gains from 75.9% to 94.9% |
| InsightBench (2025) | Insight quality | Known insights planted in 100 business datasets; evaluates question formulation, interpretation, insight summary, actionable steps via a two-way LLaMA-3 evaluator. Qualification: recovering planted insights is a tractable proxy, not open-ended novel insight; an LLM evaluator inherits the biases DABStep was designed to avoid |
| DiscoveryBench (ICLR 2025) | Hypothesis recovery | Agents recover known hypotheses from real datasets, with facet-based failure analysis |

**Borrowed instruments** — GAIA, AssistantBench, MLAgentBench, MLE-bench — were not designed for analytics. Results on them are sanity checks, not analytics-native evaluations. Progress claims for analytics agents should rest on analytics-native instruments. (MLE-bench earns one specific mention: it independently validated AIDE's tree-search organisation, 4× more medal wins than the best linear agent — a result about agent organisation measured on a general instrument.)

The table-QA cluster (WikiTableQuestions, TabFact, FeTaQA) is superseded for agentic purposes: answering questions about tables is not the same as doing analysis with them.

## The hybrid harness: how to operationalise insightfulness

No validated instrument exists today. The harness below is the survey's sketch of how insightfulness becomes measurable in principle — a composite of deterministic grounding checks and bias-controlled human judgment, with the boundary between the two drawn explicitly rather than blurred inside an LLM judge.

### Layer 1 — programmatic and deterministic
- **Factual grounding.** Every number the agent reports must be recomputable from the dataset and the governed metric definitions. Fully deterministic given lineage. An ungrounded "insight" is a hallucination, not a finding.
- **Coverage.** Did the analysis perform each step the task required — the right tables profiled, the right segments compared, the confounders checked?
- **Governed-metric adherence.** Did the agent use certified definitions, or invent its own? No mainstream benchmark measures this; in production it is the failure class enterprises fear most, because the output looks authoritative while being wrong.

### Layer 2 — qualitative, with bias controls
Novelty and decision-relevance can be scored on structured rubrics, but only with the controls current LLM-judge practice routinely skips:
- **Blinded judges** who do not know which system produced the analysis under review.
- **Reported inter-rater agreement**, not single-judge scores.
- **Reference-anchored calibration**: judges first score gold-standard analyses to fix the scale.

DABStep's deliberate avoidance of LLM-as-judge is the cautionary precedent: any harness that grades insight with the same class of models it evaluates inherits their biases by construction.

## Failure classes to design tests against (from MAST, Cemri et al., 2025)

14 failure modes in three categories, derived from 1,642 expert-annotated traces; observed system failure rates 41–86.7%:
1. **System design and specification** — the agent misunderstands what was asked; in analytics, a misunderstood requirement silently propagates through intermediate artifacts (a filtered table, a chosen join grain, a defined metric) into every downstream step.
2. **Inter-agent misalignment** — agents work at cross-purposes or duplicate work.
3. **Task verification** — failures of checking: the verifier catches only what it is competent to verify.

## Cost and latency belong in the evaluation

Efficiency became an evaluation axis with BIRD's VES and is a deployment constraint thereafter: an analytics agent routinely makes dozens of model calls per user question, where a text-to-SQL system makes one. Every evaluation plan sets a per-task cost budget and a latency budget alongside its quality measures, and reports results against all three.
