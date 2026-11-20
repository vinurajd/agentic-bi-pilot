# Cold test B — Agentic BI Design Advisor (leader)

Persona (fictional): head of analytics at a retail chain, planning a program with two use-case classes: (1) weekly trading reports for regional managers, produced on a schedule; (2) ad-hoc questions from merchandisers during the trading week.

## What the skill produced (following SKILL.md)

**Persona and scope.** Leader; brief written per use-case class with a program summary.

**Class 1 — weekly trading reports.** Consumption mode: dashboard. Persona served: business user (regional managers trust the numbers and cannot verify a query). Task shape: governed, repeatable reporting. Recommendation: **role-specialized pipeline** (profiler → transformer → modeler → reporter), because stable phases and standardized artifacts give free auditability, the cheapest cost profile, and linear debuggability. Five-axis table completed from the reference; named exposure: specification failures (a misunderstood reporting requirement corrupts every downstream artifact), mitigated by a fixed requirements artifact at the head of the pipeline. Runner-up: planner–executor loop, rejected because its generality buys nothing for a fixed report and its verification risk concentrates in the critic. Grounding: certified definitions only, lineage attached to every published figure. Oversight: analyst persona reviews artifacts before publication.

**Class 2 — merchandiser ad-hoc questions.** Consumption mode: ad-hoc analysis. Persona served: business user, supervised by analysts. Task shape: multi-step but decomposable. Recommendation: **planner–executor(–critic) loop**, the taxonomy's common middle, with the critic scoped to definition and grain checks. Named exposure: error compounding and critic competence limits, stated in the brief. Swarm pattern considered and rejected: the questions are decomposable, so the swarm's adaptivity buys little while its opacity harms the analyst's ability to trace a wrong number. Search-augmented planning rejected on cost for this task shape.

**Program summary.** Two patterns, deliberately; the brief states the framework's design lesson verbatim in substance: no best architecture exists, only task-shaped choices, and the program does not standardise on one pattern for tidiness. Shared program controls: one grounding strategy (semantic layer only), one oversight model, per-class cost profiles (pipeline cheapest; loop multiplied by planning and verification rounds).

Framework cited exactly as: Vinuraj Devaraj, "Agentic AI Meets BI: Architectures, Evaluation, and Deployment for Analytics Agents," under review at IEEE IT Professional.

## Verification against the skill's hard rules
- No pattern recommended without its task shape: PASS (both classes shape-first).
- Multi-agent designs not presented as inherently better; additions justified: PASS (swarm and search patterns explicitly rejected with reasons).
- Only reference figures and exemplars used: PASS (no invented benchmarks; CrewAI/LangGraph not invoked).
- Semantic-layer bypass flagged as trust-contract risk: PASS (grounding strategy is layer-only, stated as a program control).
- Citation status exact: PASS.
