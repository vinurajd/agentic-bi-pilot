# Agentic BI Deployment Readiness — FAQ

## Getting started

**What does this skill do?**
It readiness-checks an analytics agent before or after it ships, across the six areas where deployments actually break: cost and latency, reliability, security, privacy, human oversight and governance, and the KPI trust contract. It produces a scorecard in which every check carries a verdict and the evidence that decides it.

**How do I start?**
Describe the agent, its job, everything it ingests, everything it can do, and the data it can reach. The ingestion list matters most: it defines the threat model, so it has to be complete.

**Who is it for?**
An analytics leader clearing a program of agents for production, and a practitioner shipping or running one agent.

## The framework

**What verdicts does the scorecard use?**
Ready, where the control exists and the evidence names it. Ready with controls, where it exists in partial form with the gap and its compensation named. Not ready, where the control is absent or exists only as an instruction to the model where system enforcement is required. Not assessable, where the evidence does not exist yet — silence is never scored as readiness. The overall verdict follows the worst blocking area; it is never an average.

**Why is privacy by prompting an automatic failure?**
Because the evidence says it does not work. In the PrivacyLens study, models answered privacy questions at roughly 90–95% accuracy and still leaked the same sensitive data in 25–40% of agent actions. Knowing the rule and following it in action are different things, so access control has to be enforced by the system around the agent, at query time. A prompt that asks the agent to be careful is not a control.

**What is the ingestion threat model?**
Analytics agents read untrusted content for a living: spreadsheets, CSVs, emails, logs, scraped tables. Indirect prompt injection hides instructions inside that content, and a poisoned cell or a crafted log line becomes an instruction the agent may follow. The review requires an explicit threat model naming the sources, what a followed injection could reach, and the controls at the boundary.

**Where does the framework come from?**
Vinuraj Devaraj, "Agentic AI Meets BI: Architectures, Evaluation, and Deployment for Analytics Agents," under review at IEEE IT Professional. The figures it cites — multi-agent failure rates of 41–86.7% in the MAST study, the safest agent in ToolEmu still failing 23.9% of high-stakes cases, over 90% of surveyed agents lacking explicit trust and safety mechanisms — are the survey's, with their sources.

## The review

**How does it relate to the Semantic Layer Contract Checker?**
They compose. This review covers the agent and its deployment; the Contract Checker, a companion skill by the same author, audits the semantic layer itself against a ten-requirement contract, from a dbt manifest or PromptQL metadata. If that audit has been run, this scorecard carries its findings into the trust-contract area. If it has not, the scorecard recommends it.

**Our agent is already live. Is it too late?**
No. The review works on live agents, and known failures from production are the best intake evidence there is.

**What do I receive?**
A scorecard as a markdown file: one section per area, every check with its verdict and deciding evidence, an overall ship, ship-with-controls, or do-not-ship verdict, and the blocking gaps ordered by severity.
