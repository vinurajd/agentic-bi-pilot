# Cold test C — Agentic BI Deployment Readiness (practitioner, pre-deployment)

Persona (fictional): a practitioner about to ship an agent that reads vendor spreadsheets and supplier emails, summarises deliveries and pricing, and can draft purchase orders in the purchasing system. Access control today: the system prompt tells the agent which suppliers' data each user may see. No injection threat model. Metrics come from a governed semantic layer; the Contract Checker audit has not been run.

## What the skill produced (following SKILL.md)

**Scorecard (abridged to the decisive checks).**

- Area 1, Cost and latency: **Not assessable** — per-task cost unmeasured; the evidence that would decide it (a metered pilot week) is named.
- Area 2, Reliability: **Ready with controls** — intermediate artifacts (extracted tables, drafted orders) are inspectable; gap named: no failure-class mapping yet, compensating control is human approval on every drafted order.
- Area 3, Security: **Not ready** — the agent ingests spreadsheets and emails (untrusted input by the framework's definition) with no injection threat model, and a followed injection could reach the purchase-order drafting tool, whose permissions are unscoped. Evidence: intake answers; the literature position recorded honestly (evaluation more mature than defences; AgentDojo's finding that socially engineered injections outperform naive ones).
- Area 4, Privacy: **Not ready** — access control is prompt-level only. The special-weight rule applies verbatim: privacy by prompting is not ready (PrivacyLens: 90–95% on privacy questions, 25–40% leakage in actions). Enforcement must move to query time, per user entitlement.
- Area 5, Oversight and governance: **Ready with controls** — human approval gate exists for orders; gap: no OWASP/NIST mapping yet (LLM01, LLM02, LLM06, LLM10 named as the mapping to complete).
- Area 6, Trust contract: **Ready with controls** — metrics drawn from the governed layer; the gap is that the Contract Checker audit has not been run, and the scorecard recommends it and records that Area 6 cannot rise to Ready until it has.

**Overall verdict: Do not ship** — follows the worst blocking areas (3 and 4), not an average. Blocking gaps ordered: runtime access enforcement; injection threat model with scoped tool permissions; then the semantic-layer audit.

Framework cited exactly as: Vinuraj Devaraj, "Agentic AI Meets BI: Architectures, Evaluation, and Deployment for Analytics Agents," under review at IEEE IT Professional.

## Verification against the skill's hard rules
- No check passed on assertion alone; every verdict names evidence: PASS.
- No averaging away of blocking failures: PASS (overall follows Areas 3 and 4).
- Only reference figures used, with citations: PASS (PrivacyLens figures; no invented incident rates).
- Injection gap recorded honestly rather than argued away: PASS.
- OWASP/NIST mapping limited to the reference's items: PASS (LLM01/02/06/10; Govern/Map/Measure/Manage referenced as the scaffold).
- Citation status exact: PASS.
