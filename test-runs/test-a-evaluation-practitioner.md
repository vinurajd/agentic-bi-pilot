# Cold test A — Agentic BI Evaluation Planner (practitioner)

Persona (fictional): a data analyst at a mid-size retailer. Their natural-language querying agent demos well, but finance has twice caught revenue figures that do not match the certified finance report. Nothing is measured today beyond spot checks.

## What the skill produced (following SKILL.md)

**Persona and scope.** Practitioner, one agent, ad-hoc mode serving business users. Intake surfaced the decisive fact: the agent generates SQL against warehouse tables directly; a certified revenue definition exists in the semantic layer, but the agent does not use it.

**Failure classification.** The observed failures are governed-metric adherence failures with a verification component (MAST categories: task verification, over a specification substrate). The agent's answers can be arithmetically consistent and still wrong, because the definition is wrong.

**Axis placement.** Current evaluation covers correctness only, and only anecdotally (spot checks). Efficiency unmeasured; insightfulness not yet in scope for a querying agent of this shape, and the plan says so rather than inflating the design.

**Instruments.** BIRD-style internal set for messy-schema querying with efficiency scoring; a DS-1000-style coding floor is not the binding constraint here and is noted as covered by vendor claims only — flagged as a sanity check, not evidence. Spider 2.0 cited for calibration of expectations on workflow tasks (roughly 21%).

**Layer 1 (deterministic).**
- Grounding: every revenue figure in the golden set recomputed from the certified definition (grain, filters, adjustments) — pass/fail.
- Governed-metric adherence: the agent must resolve "revenue" to the certified definition; any query whose definition cannot be traced to the semantic layer fails automatically.
- Coverage: for ratio and comparison questions, both segments and the stated period must appear in the executed queries.

**Golden set.** Seeded from finance's two disputed outputs (as constructed items with expected results computed from the certified definition), plus 40 historical analyst questions. CSV columns per spec.

**Layer 2.** Not applied to numeric answers. Applied only to the agent's written summaries, with a two-rater blinded rubric and agreement reported; the plan records that no validated insight metric exists.

**Budgets.** Per-question cost and p95 latency budgets set beside the quality gates.

**Gate.** Ship requires 100% governed-metric adherence on the golden set and ≥ the agreed grounding pass rate; any invented definition is an automatic no-ship.

Framework cited exactly as: Vinuraj Devaraj, "Agentic AI Meets BI: Architectures, Evaluation, and Deployment for Analytics Agents," under review at IEEE IT Professional.

## Verification against the skill's hard rules
- No LLM-judge score presented as validated measurement: PASS (Layer 2 bounded, caveat recorded).
- Correctness not allowed to stand as the whole evaluation where failures are grounding failures: PASS (adherence check is the gate).
- Figures used only from the reference, with citations: PASS (Spider 2.0 ~21%; no invented agent scores).
- InsightBench not misdescribed: PASS (not invoked for this agent shape).
- Citation status exact, not upgraded: PASS.
