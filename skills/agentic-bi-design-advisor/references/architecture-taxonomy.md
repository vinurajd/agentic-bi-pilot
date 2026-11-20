# Architecture Taxonomy for Analytics Agents

Reference for the Agentic BI Design Advisor. Distilled, without alteration of substance, from: Vinuraj Devaraj, "Agentic AI Meets BI: Architectures, Evaluation, and Deployment for Analytics Agents," under review at IEEE IT Professional (Section 3, with Sections 2 and 5).

## The four patterns

Every analytics-agent design answers the same question differently: how should work be divided among agents, and how should they coordinate? Four patterns recur.

### (a) Planner–executor(–critic) loops
A planner decomposes the request into a task graph; executors carry out the steps, typically by generating and running code; an optional critic or verifier checks intermediate and final outputs and triggers replanning on failure.
- Exemplars: TaskWeaver (analytics-native; plans requests, converts them to executable code with user-defined plugins, sandboxed execution). Data Interpreter (mature form: hierarchical graph-based decomposition, dynamic replanning, tool integration, confidence-based verification, experience replay; 94.9% on InfiAgent-DABench). AutoGen (conversable agents coordinating through structured dialogue) is the framework such systems build on or position against.
- Strength: generality. Weakness: error compounding — a misplanned step poisons everything downstream, and the critic only catches what it is competent to verify.

### (b) Role-specialized pipelines
Agents hold fixed professional roles and pass structured artifacts along an assembly line, decomposing expertise rather than tasks.
- Exemplars: MetaGPT (human Standardized Operating Procedures encoded into role-based teams with structured artifacts at each handoff). ChatDev (a virtual software company as a chain of atomic two-role dialogues; rigid phase structure beats open-ended chat; "communicative dehallucination" — agents ask clarifying questions rather than hallucinating through ambiguity). CrewAI (industry framework, no peer-reviewed paper) productized role-based "crews" and is the most widely copied template for virtual analyst teams.
- Analytics mapping: profiler → transformer → modeler → reporter, mirroring how human analytics teams divide labour.

### (c) Graph-orchestrated swarms
The agent collective is a computational graph — nodes as operations, edges as information flow — rather than a chat transcript or a pipeline.
- Exemplars: GPTSwarm (peer-reviewed foundation: agents as graphs whose nodes and edges are automatically optimizable, so the swarm's structure is itself learned). LangGraph (open-source framework, no peer-reviewed paper) is the dominant production substrate: stateful cyclic graphs with explicit control flow, human-in-the-loop hooks, and persistence.
- Strength: adaptivity — cyclic graphs express iterative refinement and conditional branching that linear pipelines cannot; optimizable topology answers how many agents a task needs. Costs: opacity and tuning complexity; learned topologies are harder to debug and topology search is computationally expensive.
- Analytics fit: workflows whose structure is not known in advance — exploratory analysis where the next step depends on what the data reveals.

### (d) Search-augmented planners
The planner–executor skeleton, but naive sequential planning is replaced by explicit search over the solution space.
- Exemplars: SELA (Monte Carlo tree search fused with LLM agents for automated machine learning; pipeline configurations as search-tree nodes; 65–80% win rates across 20 datasets). AIDE (ML-engineering trial-and-error framed as tree search over code solutions; independently validated on OpenAI's MLE-bench, where its tree search won four times more medals than the best linear agent).
- Lesson: whenever a task admits many plausible solution paths, explicitly exploring the space beats committing to the planner's first plan. Cost: this is the most expensive pattern per task — tree search multiplies agentic loops' already-multiplied LLM calls.

## Comparison on five axes

**Coordination mechanism.** Planner–executor: task graphs and verification gates. Role pipelines: structured artifact handoffs. Swarms: graph edges and message passing. Search-augmented planners: tree expansion and selection policies. The trend runs from implicit coordination (conversation) toward explicit coordination (graphs, trees, artifacts) — and explicit coordination is easier to audit.

**Failure modes.** The MAST taxonomy (Cemri et al., 2025) — 14 failure modes in three categories (system design and specification; inter-agent misalignment; task verification), derived from 1,642 expert-annotated traces, with observed system failure rates of 41–86.7% — maps differentially:
- Role pipelines are most exposed to *specification* failures: a misunderstood requirement corrupts every downstream artifact.
- Planner–executor loops concentrate risk in *task verification*: the critic is a single point of failure.
- Swarms amplify *misalignment*: more agents through learned topologies means more coordination breakdowns. More agents is not automatically better.
- Search-augmented planners mitigate planning failures by construction but concentrate cost and latency risk.

**Token and compute cost** (ascending): role pipelines (one pass per role) < planner–executor loops (planning and verification rounds multiply calls) < swarms (multiplied further by agent count and topology complexity) < search-augmented planners (most expensive). Per-step cost optimisation — cascades that learn which model to query per request (FrugalGPT), routers matching difficulty to model strength (RouteLLM) — matters most for patterns (c) and (d).

**Debuggability.** Linear structures debug linearly: pipelines and simple planner–executor loops let an analyst inspect each step in order. Cyclic learned topologies resist this — tracing which interaction produced a wrong number is genuinely hard. Search trees sit in between: the winning path is inspectable, the search that found it less so. For the analyst who must supervise the agent, debuggability is a deployment precondition, not a nice-to-have.

**Fit to analytics task shapes.** No pattern dominates, because task shapes differ:
- Governed, repeatable reporting (the dashboard mode) → role pipelines: stable phases, standardized artifacts, free auditability.
- Open-ended exploration → swarms, where workflows cannot be scripted in advance.
- Optimization-flavoured problems (feature engineering, model selection) → search-augmented planners.
- The common middle — multi-step but decomposable analyses → planner–executor loops, which is why they prevail in the best-evaluated systems.

## BI context the design must respect (from Section 2)

**Three consumption modes.** *Dashboards*: curated, scheduled, governed; the agent must respect certification and produce reproducible, lineage-attached outputs. *Ad-hoc analysis*: the analyst's iterative loop; speed and interactivity matter, but every step must still ground in governed definitions. *Embedded decisions*: the agent's output feeds an operational decision (a risk score, a forecast, an anomaly flag), raising the stakes on correctness, latency, and auditability simultaneously.

**Three personas.** The *business user* asks in business language, trusts the numbers implicitly, and cannot verify a query — governed grounding is everything, because no human in the loop can catch a fabricated metric. The *analyst* supervises, corrects, and learns from the agent; needs visible reasoning steps, editable intermediate artifacts, and the ability to intervene mid-workflow. The *data engineer* owns pipelines, access controls, cost, and reliability; for this persona the agent is a workload to be governed.

**The semantic layer is not optional.** In a mature BI practice, analysts query a governed semantic layer — certified metric definitions, hierarchies, access rules — not raw tables. An agent that bypasses the semantic layer and writes SQL against raw tables is violating the enterprise's contract about what the numbers mean. Every design must state how the agent grounds in governed definitions.

## The design lesson

No best architecture exists, only task-shaped choices. Adding agents trades on every axis: coordination failures rise, token costs multiply, debuggability degrades. The best-evaluated systems win not by maximizing agent count but by structuring coordination explicitly and verifying aggressively.
