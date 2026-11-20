# Deployment Readiness Checklist for Analytics Agents

Reference for the Agentic BI Deployment Readiness review. Distilled, without alteration of substance, from: Vinuraj Devaraj, "Agentic AI Meets BI: Architectures, Evaluation, and Deployment for Analytics Agents," under review at IEEE IT Professional (Section 7, with Sections 2 and 6).

Context: deployment is where analytics agents are currently weakest and where the gap between research prototypes and production systems is widest. Rahman et al. (2025) found business understanding, deployment, and monitoring the most neglected stages of the data-science agent lifecycle, with over 90% of surveyed agents lacking explicit trust and safety mechanisms.

Each area below lists what to check and the evidence a "ready" verdict must rest on. A check is never passed on assertion alone: name the artefact, control, or measurement that decides it.

## 1. Cost and latency
Agentic analytics multiplies per-task LLM calls: one user question becomes a planning pass, several rounds of code generation and execution, self-correction loops, and verification steps — dozens of billed invocations where a text-to-SQL system makes one.
- Per-task cost is measured, not estimated, and a budget exists per consumption mode (dashboard refresh, ad-hoc question, embedded decision).
- A cost strategy is in place where call volume warrants it: LLM cascades that learn which model combination to query per request (FrugalGPT: up to 98% inference-cost reduction while matching accuracy) and/or pre-call routers matching difficulty to model strength (RouteLLM: 2× or more cost reduction without quality loss). Inside multi-agent pipelines, step difficulty varies enormously — trivial SQL generation does not need the same model as hard multi-hop reasoning.
- Latency is measured at the task level, including planning and verification rounds, against the mode's tolerance (embedded decisions are the least forgiving).

## 2. Reliability
The MAST taxonomy (Cemri et al., 2025) — 14 failure modes in three categories (system design and specification; inter-agent misalignment; task verification), from 1,642 expert-annotated traces — reports system failure rates of 41–86.7%. Specification breakdowns and coordination breakdowns dominate, and both are worse in analytics, where intermediate artifacts (a filtered table, a chosen join grain, a defined metric) silently propagate downstream. DABStep's 14.55% ceiling on hard tasks is the same story as a benchmark number.
- The deployment's expected failure classes are named, mapped to the MAST categories, and each has a detection point.
- Verification is independent of generation where the stakes warrant it; the verifier's own competence limits are stated (a critic catches only what it can verify).
- Intermediate artifacts are inspectable, so a wrong number can be traced to the step that produced it.
- "More agents" has not been treated as a reliability strategy.

## 3. Security — the ingestion threat model
Analytics agents inherit a threat model defined by what they ingest. Indirect prompt injection (Greshake et al., 2023) embeds malicious instructions in retrieved data — web pages, documents — rather than the user prompt. For analytics agents the translation is direct: a poisoned cell in a dataset, a malicious line in a log file, or a crafted string in a scraped table becomes an instruction the agent may follow. AgentDojo (Debenedetti et al., 2024), the standard evaluation apparatus (97 tasks, 629 security cases), found that polite, socially engineered injections dramatically outperform naive attacks. BIPIA (Yi et al., 2025) extends the line with dedicated benchmarking and defences.
- Every ingested source (datasets, spreadsheets, CSVs, emails, logs, documents) is treated as untrusted input — a data-trust boundary, under the same posture applied to user uploads and third-party feeds.
- An explicit injection threat model exists for the deployment, naming sources, the actions an injected instruction could trigger, and the controls at the boundary.
- The agent's tool permissions are scoped so that a followed injection cannot reach actions beyond the task (see also OWASP LLM06, Excessive Agency).
- Evaluation for this threat has been run or scheduled (AgentDojo-style cases adapted to the deployment's own sources). Note the literature's position: evaluation here is far more mature than deployed defences — a "no known defence" finding is recorded honestly, not argued away.

## 4. Privacy — enforce at runtime, never by prompting
ToolEmu (Ruan et al., 2024), the first scalable risk-evaluation framework for tool-using agents (144 high-stakes cases, 36 toolkits, 9 risk categories), found even the safest agent fails 23.9% of cases, including private-data leaks and financial-loss scenarios. PrivacyLens (Shao et al., 2024) isolated the mechanism across 493 contextual-integrity vignettes: models answer privacy-appropriateness questions at roughly 90–95% accuracy yet leak the same sensitive data in 25–40% of agent actions. Declarative privacy knowledge does not transfer to agentic behaviour. SecureSQL (Song et al., 2024) adds the analytics-specific vector: leakage through the natural-language database interface itself.
- Access control is enforced by the system around the agent at query time — row-level, per user entitlement — not requested of the agent in a prompt.
- The data the agent can reach is inventoried, including PII and regulated data, and the query layer is treated as an exfiltration path.
- Privacy behaviour has been tested in action scenarios, not by asking the model privacy questions.

## 5. Human oversight and governance
- The oversight interface fits iterative analysis: linear chat suffers context collapse as analyses iterate; multi-threaded conversational analytics — separating the main conversation from refinement threads (AI Threads, Hong & Crisan, 2023, preprint) — is the strongest empirically evaluated oversight pattern the survey found. At minimum: visible reasoning steps, editable intermediate artifacts, and the ability to intervene mid-workflow for the analyst persona.
- The deployment is mapped onto the governance frameworks enterprise teams actually use: the OWASP Top 10 for LLM Applications (v2025) — notably LLM01 Prompt Injection (the 2025 revision explicitly includes indirect injection via tool outputs), LLM02 Sensitive Information Disclosure, LLM06 Excessive Agency, LLM10 Unbounded Consumption — and the NIST AI Risk Management Framework 1.0 with its Generative AI Profile 600-1 (Govern, Map, Measure, Manage).
- Unbounded consumption is controlled: per-task and per-user call and cost ceilings exist (see Area 1).

## 6. The KPI trust contract
From Section 2: the requirements are structural, not cosmetic.
- **Certified definitions.** Every metric the agent reports is drawn from the governed semantic layer — certified definition, grain, and filters — never synthesized on the fly. An agent that invents a plausible-but-uncertified KPI definition produces output that looks authoritative while being wrong in exactly the way enterprises fear most; when two surfaces show different revenue numbers, the trust damage takes quarters to repair.
- **Auditability.** Every number is traceable to its definition and lineage.
- **Row-level access.** The agent sees only what its user is entitled to see, enforced at query time (see Area 4).
- Where a dbt manifest or PromptQL / Hasura DDN metadata project is available, the deep audit of these declarations is the Semantic Layer Contract Checker's job (the companion skill by the same author); this review records whether that audit has been run and what it found.

## The deployment gap, stated plainly

Per-task cost multiplies with agentic loops; reliability is empirically poor and dominated by specification and coordination failures; the threat model is defined by the untrusted data agents must ingest; privacy knowledge demonstrably fails to transfer into agent behaviour; and governance is the least-covered dimension in surveyed systems. A readiness review that does not surface at least the applicable parts of this gap has not done its work.
